# MaintainerOS — Architecture

- Status: Proposed architecture
- Version: 0.1
- Style: Modular monolith with asynchronous workers
- Source of truth for repository objects: GitHub

## 1. Architecture goals

- Keep domain logic in one authoritative backend.
- Make GitHub event ingestion reliable and idempotent.
- Separate read projections from external write actions.
- Enforce workspace and repository authorization centrally.
- Keep AI providers optional and replaceable.
- Make self-hosted deployment practical.
- Avoid premature microservices.

## 2. Proposed technology

| Layer | Technology | Responsibility |
|---|---|---|
| Web | Next.js, TypeScript, Tailwind CSS | User interface |
| API/domain | Laravel, PHP | Business rules, authorization, API |
| Database | PostgreSQL | Durable application state |
| Queue/cache | Redis, Laravel Horizon | Background processing |
| Integration | GitHub App | Repository access and webhooks |
| AI | Provider adapter interface | Optional recommendations |
| Deployment | Docker Compose | Self-hosted runtime |
| CI | GitHub Actions | Tests, analysis, build |

Versions must be pinned and supported versions documented when implementation begins.

## 3. Logical system

```text
Maintainer Browser
       |
       v
Next.js Web Application
       |
       v
Laravel API / Domain Layer -------- PostgreSQL
       |                                 ^
       v                                 |
Redis Queue --> Workers --> Sync / Projection Services
       ^                         |
       |                         v
GitHub Webhook Gateway <---- GitHub App / GitHub API
       |
       v
Signature Verification + Delivery Deduplication

Domain workflows:
  Issue Operations
  Pull Request Operations
  Release Preparation
  Repository Health
  Contributor Context
  Audit and Approval

Optional AI adapters:
  OpenAI | Anthropic | Google | Ollama | Rules-only
```

## 4. Backend organization

Use a modular monolith. Suggested domain boundaries:

- Identity: users, workspaces, memberships, roles.
- GitHub: installations, repositories, webhook deliveries, API client, sync.
- Issues: synchronized issue records, filters, triage recommendations.
- PullRequests: PR projections, checks, review queue.
- Releases: comparison ranges, collected changes, release drafts.
- Contributors: contributor identity mapping and contribution history.
- RepositoryHealth: metric definitions, snapshots, reports.
- AI: provider contracts, adapters, prompt/version registry, usage metadata.
- Governance: approvals, audit records, security events.

Modules may share infrastructure through explicit interfaces. Avoid circular domain dependencies.

## 5. Data ownership and synchronization

GitHub is authoritative for issues, PRs, labels, reviews, checks, commits, and releases. MaintainerOS stores local projections for search, aggregation, and workflow state.

Each synchronized object should retain:
- GitHub numeric or node identifier.
- Repository identity.
- Source URL.
- Source updated timestamp when available.
- Last synchronized timestamp.
- Projection schema/version where needed.

Webhook events are signals, not guaranteed complete state. Workers should fetch current authoritative objects when necessary. Scheduled reconciliation repairs missed or out-of-order events.

## 6. Webhook processing

1. Receive the raw request body.
2. Verify GitHub HMAC signature using constant-time comparison.
3. Validate event and delivery headers.
4. Persist a delivery record with a unique delivery identifier.
5. Enqueue processing and return promptly.
6. Process idempotently in a worker.
7. Fetch authoritative state if the event payload is incomplete or stale.
8. Update projections transactionally.
9. Record processing outcome and retry metadata.

Use bounded exponential backoff for transient failures. Permanently invalid events should be marked failed and inspectable without repeated retries. Do not perform long-running work in the webhook request.

## 7. External write workflow

All writes to GitHub must pass through a centralized action service:

1. Authenticate the user.
2. Authorize workspace and repository access.
3. Validate the requested action and current source state.
4. Require explicit approval for consequential actions.
5. Obtain a short-lived installation token with required permission.
6. Execute the GitHub API request.
7. Record actor, action, target, request correlation ID, and outcome.
8. Refresh the local projection.

AI-generated output cannot bypass this service or grant itself permissions.

## 8. Initial data model

Proposed tables:
- users
- workspaces
- workspace_memberships
- github_installations
- repositories
- repository_memberships, only if required by the authorization model
- webhook_deliveries
- issues
- pull_requests
- contributors
- triage_recommendations
- review_records
- release_drafts
- health_snapshots
- ai_runs
- approval_records
- audit_logs

Use UUIDs for internal identifiers and unique constraints for external GitHub identifiers. Define tenant ownership explicitly. Add indexes based on observed query patterns.

## 9. API conventions

- Prefix application endpoints with /api/v1.
- Use resource-oriented routes and consistent JSON envelopes.
- Validate request input at the boundary.
- Authorize every resource access server-side.
- Use pagination for collections.
- Return stable machine-readable error codes.
- Use idempotency keys for operations where retries could duplicate external effects.
- Document API changes and compatibility expectations.

## 10. AI adapter contract

The AI layer accepts a bounded task and sanitized context, then returns a typed result. It must not receive installation tokens or direct unrestricted database access.

Responsibilities:
- Select configured provider.
- Apply task-specific data minimization.
- Validate structured output.
- Enforce timeouts and usage limits.
- Record model and prompt version metadata.
- Handle unavailable providers gracefully.

Rules-only mode must remain available.

## 11. Deployment topology

The initial Docker Compose deployment is expected to include:
- web
- api
- worker
- scheduler
- postgres
- redis

A reverse proxy and TLS termination may be provided by the deployment environment. Production deployments must configure persistent volumes, backups, secrets, health checks, log rotation, and restore procedures.

Do not expose PostgreSQL or Redis publicly by default.

## 12. Observability

Use structured logs and correlation IDs across webhook delivery, queue job, domain action, and GitHub API request. Monitor:
- webhook verification failures,
- queue depth and age,
- job retry and failure rates,
- GitHub API rate-limit responses,
- sync lag,
- external action failures,
- AI provider errors and usage.

Never log tokens, private keys, or unnecessary issue/PR body content.

## 13. Testing strategy

- Unit tests for domain rules and metric calculations.
- Feature tests for authorization and API behavior.
- Integration tests for webhook verification and idempotency.
- Contract tests for GitHub API adapters.
- Queue retry and reconciliation tests.
- Tenant isolation tests.
- Frontend component and critical journey tests.
- Docker smoke tests.

Use mocked GitHub responses for deterministic CI. Run limited integration tests against a dedicated test installation when credentials are available.

## 14. Security boundaries

- GitHub App private key and encryption keys are deployment secrets.
- Installation tokens are short-lived and never sent to the browser.
- The browser receives only user-authorized application data.
- All tenant-owned queries must be scoped and authorized.
- Webhook payloads and AI output are untrusted input.
- Outbound URL fetching must be constrained to prevent SSRF.
- External write operations are centralized and audited.

## 15. Architecture decisions to revisit

- Whether a separate GitHub App service is necessary.
- Whether contributor identity needs a dedicated model.
- Whether health snapshots require a time-series extension.
- Whether a public hosted service is justified.
- Whether any domain needs extraction into a separate service.

Do not split the modular monolith until operational evidence justifies it.
