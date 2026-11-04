# MaintainerOS — Roadmap

This roadmap is an execution plan, not a promise that every milestone will ship on a fixed date. Milestones are relative to the start of active implementation. Scope may change based on maintainer feedback, security findings, and engineering evidence.

## Product direction

Build a GitHub-native, self-hostable maintenance workspace. GitHub remains the source of truth. Maintainers retain control over consequential actions. AI remains optional.

## Phase 0 — Foundation (Days 1–14)

**Goal:** Establish a trustworthy, runnable development foundation.

- [ ] Confirm product scope and architecture.
- [ ] Establish repository governance and contribution process.
- [ ] Add license, security policy, code of conduct, and issue templates.
- [ ] Scaffold Laravel API and Next.js application.
- [ ] Configure PostgreSQL and Redis.
- [ ] Add Docker Compose for local development.
- [ ] Add CI for formatting, static analysis, tests, and builds.
- [ ] Establish environment variable documentation.
- [ ] Add initial authentication and workspace model.

**Exit criteria:** A new developer can follow documented steps to run the foundation locally; CI is green; no production-readiness claim is made.

## Phase 1 — GitHub integration (Days 15–35)

**Goal:** Connect repositories and synchronize events safely.

- [ ] Create GitHub App manifest and setup documentation.
- [ ] Implement installation lifecycle.
- [ ] Implement repository selection.
- [ ] Verify webhook signatures.
- [ ] Persist and deduplicate webhook deliveries.
- [ ] Queue webhook processing.
- [ ] Synchronize repository, issue, and PR metadata.
- [ ] Implement retry and reconciliation.
- [ ] Add tenant isolation and permission tests.
- [ ] Expose sync status and failures.

**Exit criteria:** A test installation synchronizes selected repository data and recovers from duplicate, delayed, and retried events.

## Phase 2 — Maintainer workflows (Days 36–60)

**Goal:** Deliver useful, reviewable workflows.

- [ ] Build issue queue and filters.
- [ ] Implement deterministic triage suggestions.
- [ ] Display duplicate candidates without automatic closure.
- [ ] Build pull request review queue.
- [ ] Display available CI/check context.
- [ ] Implement release comparison and changelog drafts.
- [ ] Add explicit approval workflow for GitHub writes.
- [ ] Add audit records.
- [ ] Add rules-only mode and AI adapter contract.
- [ ] Add critical workflow tests.

**Exit criteria:** A maintainer can use issue triage and release preparation end-to-end with approval gates and audit history.

## Phase 3 — Public beta (Days 61–90)

**Goal:** Make the product installable and understandable by independent maintainers.

- [ ] Complete Docker Compose deployment.
- [ ] Publish installation and configuration guide.
- [ ] Publish GitHub App permission explanation.
- [ ] Add health checks and operational documentation.
- [ ] Add backup, restore, disconnect, and deletion guidance.
- [ ] Publish a demo using clearly labeled sample data.
- [ ] Run usability tests with independent maintainers.
- [ ] Fix onboarding and reliability problems.
- [ ] Publish a versioned beta release.
- [ ] Publish known limitations and security reporting instructions.

**Exit criteria:** An independent developer can deploy, connect a test repository, understand product limitations, and report a reproducible issue.

## Months 4–6 — Adoption and reliability

- Improve onboarding based on observed friction.
- Add contributor context and first-contribution workflows.
- Add explainable repository health snapshots.
- Improve accessibility and performance.
- Establish a predictable release cadence.
- Respond to issues and review external contributions.
- Document real installations and usage with consent.
- Evaluate additional integrations based on demand.

## Months 7–12 — Ecosystem maturity

- Expand integrations only where users demonstrate need.
- Improve governance as community participation grows.
- Strengthen security review and release provenance.
- Improve contributor retention and documentation.
- Evaluate package distribution if a stable reusable SDK emerges.
- Publish periodic project health and maintenance reports.
- Assess OpenSSF Criticality Score and other ecosystem indicators.
- Apply to open-source support programs only when current eligibility requirements are demonstrably met.

## Adoption goals (aspirational)

These are internal planning targets, not guarantees or program qualification claims.

| Metric | Day 30 | Day 60 | Day 90 | Month 12 |
|---|---:|---:|---:|---:|
| External contributors | 0–1 | 3 | 5 | 20+ |
| External merged PRs | 0 | 5 | 10 | 40+ |
| Independent installations | 1 | 3 | 10 | 100 |
| Integrations | 0 | 1 | 2 | 5 |

Stars and downloads are discovery signals, not substitutes for active usage or project dependency. Do not manufacture metrics.

## Release approach

- 0.1.0: functional alpha when core integration is usable.
- 0.2.0: external beta when maintainers can test workflows.
- 0.3.0: public beta when deployment and security documentation are ready.
- 1.0.0: only after stability, compatibility, upgrade, backup, and support expectations are met.

## Out of scope until validated

- Autonomous issue closure, PR merging, or release publication.
- A general workflow builder.
- A hosted enterprise SaaS offering.
- Billing and monetization.
- Broad integrations unrelated to maintainer workflows.

## How roadmap changes are made

Open an issue or discussion with the problem, user impact, proposed scope, and trade-offs. Significant changes should be recorded in an architecture decision record or roadmap update. Security fixes may be handled privately under the security policy.
