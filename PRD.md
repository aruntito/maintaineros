# MaintainerOS — Product Requirements Document

- Status: Draft for implementation
- Version: 0.1
- Product stage: Foundation
- License: Apache-2.0
- Primary integration: GitHub App

## 1. Product summary

MaintainerOS is a self-hostable, GitHub-native workspace for open-source project maintenance. It consolidates operational signals and helps maintainers move work through issue triage, pull request review, release preparation, contributor onboarding, and repository health workflows.

GitHub remains the source of truth for repository objects. MaintainerOS stores synchronized projections, derived metrics, recommendations, approvals, and audit records.

## 2. Problem

Maintainers coordinate recurring activities across multiple GitHub surfaces and external tools. Context is fragmented; queues become stale; new contributors struggle to understand conventions; release preparation is repetitive; and maintenance health is difficult to assess consistently.

The product must reduce coordination overhead without taking control away from maintainers.

## 3. Goals

1. Give maintainers one actionable view of selected repositories.
2. Synchronize GitHub issues and pull requests reliably.
3. Make issue and PR queues easier to prioritize.
4. Prepare release notes from merged work.
5. Make recommendations and external write actions auditable.
6. Support self-hosted operation.
7. Keep core functionality available without AI.
8. Make metrics explainable and reproducible.

## 4. Non-goals for the first public beta

- Replacing GitHub Issues, Pull Requests, Actions, or Discussions.
- Hosting Git repositories or CI runners.
- Autonomous code merging or release publishing.
- A general-purpose workflow automation builder.
- A social network or contributor marketplace.
- Enterprise billing, multi-region hosting, or complex SSO.
- Mandatory use of a paid AI provider.
- Claiming certifications or compliance not independently achieved.

## 5. Personas

**Solo maintainer:** Maintains one or more repositories with limited time. Needs clear priorities, stale-work visibility, and low setup overhead.

**Small project team:** Shares review and release responsibilities. Needs visibility, ownership, auditability, and consistent workflows.

**First-time contributor:** Needs clear contribution instructions, issue context, project conventions, and predictable feedback.

## 6. Core user journeys

### Connect a repository
1. User signs in.
2. User installs the MaintainerOS GitHub App on selected repositories.
3. MaintainerOS validates the installation and granted permissions.
4. A background sync imports minimum required metadata.
5. The dashboard displays synchronization status and actionable queues.

### Triage an issue
1. A webhook or reconciliation detects an issue.
2. MaintainerOS updates its local projection.
3. Deterministic rules identify missing information and possible labels.
4. Optional AI produces a structured summary or recommendation.
5. The maintainer approves or rejects the recommendation.
6. If approved, the application performs the authorized GitHub action and records its result.

### Review a pull request
1. A PR event updates the local record.
2. The review queue displays age, state, checks, and requested attention.
3. The maintainer views a summary and checklist.
4. Generated summaries are clearly marked as machine-generated.
5. The maintainer performs the review in GitHub or through an explicitly approved integration action.

### Prepare a release
1. Maintainer selects a tag or commit range.
2. MaintainerOS collects merged PRs and metadata.
3. Changes are grouped using transparent rules and optional draft assistance.
4. Maintainer edits and approves the release draft.
5. Publishing requires separate explicit confirmation.
6. The action and resulting URL are recorded.

## 7. Functional requirements

### P0 — Initial public beta

**Identity and workspaces**
- Authenticate users securely.
- Associate users with workspaces and roles.
- Enforce authorization server-side for every tenant-owned resource.

**GitHub integration**
- Install and validate a GitHub App.
- List accessible installations and repositories.
- Store installation and repository identifiers.
- Verify webhook signatures.
- Deduplicate webhook deliveries.
- Process webhook events asynchronously.
- Retry transient failures with bounded backoff.
- Reconcile missed events through scheduled synchronization.
- Display sync state and last successful sync.

**Issue operations**
- Synchronize issue title, body, state, labels, author, timestamps, and URLs as needed.
- Provide filters for state, labels, age, and assignment.
- Generate rule-based triage suggestions.
- Display duplicate candidates as suggestions, never automatic closures.
- Require maintainer approval before writing labels or comments.

**Pull request operations**
- Synchronize PR metadata and review/check status where permitted.
- Display an actionable review queue.
- Identify stale or waiting PRs using transparent rules.
- Provide a review checklist and links to GitHub.
- Do not submit reviews or merge PRs autonomously.

**Release preparation**
- Select a comparison range.
- Collect merged PR metadata.
- Generate an editable changelog draft.
- Require explicit confirmation before publishing.

**Audit**
- Record recommendations, approvals, rejections, and attempted external writes.
- Record actor, target, timestamp, action, and outcome.
- Avoid storing secrets or unnecessary sensitive payloads.

### P1 — After initial beta
- Contributor onboarding and first-contribution context.
- Repository health snapshots and historical trends.
- Explainable response-time and queue-age metrics.
- Optional AI summaries and recommendations.
- Additional integrations based on user demand.

## 8. AI requirements

- AI is optional and disabled unless configured.
- Provider adapters must be replaceable.
- Core workflows must have deterministic or manual fallbacks.
- Model outputs must be schema-validated and treated as untrusted input.
- AI output is a draft or recommendation, not an authorization.
- Models must not receive unrestricted GitHub credentials.
- External write actions require application-level authorization and maintainer approval.
- Record provider, model identifier, task type, timestamp, and relevant usage metadata without logging secrets.
- Provide controls for disabling AI and limiting data sent to providers.

## 9. Security and privacy requirements

- Use GitHub App installation tokens with short lifetimes.
- Request minimum necessary permissions.
- Verify webhook HMAC signatures and delivery identifiers.
- Encrypt sensitive credentials at rest using deployment-appropriate key management.
- Redact credentials and sensitive payloads from logs.
- Protect against cross-tenant access and insecure direct object references.
- Validate and constrain outbound network requests.
- Rate-limit sensitive endpoints.
- Support disconnecting GitHub installations and deleting workspace data.
- Document data collected, retention, export, and deletion behavior.
- Provide a responsible vulnerability disclosure process.

## 10. UX requirements

- Make queue state and next action obvious.
- Explain why a recommendation or health indicator exists.
- Show source links to GitHub records.
- Distinguish synchronized facts from derived metrics and AI suggestions.
- Provide empty, loading, error, stale-sync, and permission-denied states.
- Keep maintainer approval explicit.
- Make self-hosted setup understandable to developers familiar with Docker.

## 11. Success metrics

Initial metrics are hypotheses to validate, not claims:
- Time from installation to first useful repository view.
- Percentage of connected repositories completing initial sync.
- Webhook processing success and retry rates.
- Time required to triage an issue.
- Time required to prepare a release draft.
- Weekly active maintainers and connected repositories.
- Recommendations accepted, edited, or rejected.
- External contributor retention.
- Successful self-hosted installations.

Do not optimize for stars or downloads at the expense of actual user value.

## 12. MVP acceptance criteria

1. A developer can install and run the documented stack locally.
2. A user can connect a GitHub App installation with least-privilege permissions.
3. Webhooks are authenticated, deduplicated, queued, and observable.
4. Selected repository issues and PRs synchronize correctly.
5. A maintainer can review a triage suggestion without triggering an external write.
6. A release draft can be generated from a selected range and edited.
7. Every external write action requires explicit authorization and is audited.
8. Tenant isolation and critical authorization paths have automated tests.
9. A maintainer can disconnect an installation and initiate data deletion.
10. Documentation clearly identifies limitations and unsupported workflows.

## 13. Open questions

- Should the first release support GitHub-only login or email-based identity too?
- Which GitHub App permissions are strictly necessary after P0 implementation is finalized?
- Which health metrics are useful across different project types?
- What are the minimum supported PostgreSQL and Redis versions?
- Which AI adapters should ship first beyond rules-only mode and Ollama?

Resolve these through implementation evidence and maintainer feedback rather than premature complexity.
