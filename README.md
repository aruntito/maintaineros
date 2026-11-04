# MaintainerOS

**The operating system for open-source maintainers.**

MaintainerOS is an open-source, GitHub-native workspace for the operational work of maintaining software: issue triage, pull request coordination, release preparation, contributor onboarding, and repository health.

> **Status: early foundation.** This repository is being established. Capabilities described below are planned unless explicitly marked as implemented. Do not rely on MaintainerOS in production yet.

## Why MaintainerOS?

Maintainers coordinate work across issues, pull requests, CI checks, releases, documentation, and community conversations. These workflows are fragmented, and the operational burden grows as a project attracts users and contributors.

MaintainerOS aims to provide one maintainer-controlled view of that work while keeping GitHub as the source of truth.

## Principles

- **Maintainer control:** recommendations never silently merge code, close issues, or publish releases.
- **AI optional:** core workflows remain useful without a model provider or paid AI service.
- **Self-hostable:** container-based deployment is a first-class goal.
- **Provider-neutral:** optional AI capabilities use replaceable adapters.
- **Least privilege:** request only GitHub permissions required by shipped features.
- **Transparent:** health metrics expose definitions, sources, and limitations.
- **Open development:** decisions, roadmap, issues, and contributions are handled in the open.

## Planned capabilities

| Area | Intended capability | Priority |
|---|---|---|
| GitHub integration | App installation, repository selection, webhooks, synchronization | P0 |
| Issue operations | Actionable queue, classification suggestions, duplicate candidates | P0 |
| Pull request operations | Review queue, CI context, review checklist | P0 |
| Release preparation | Collect merged changes and draft release notes | P0 |
| Auditability | Record recommendations, approvals, and external write actions | P0 |
| Repository health | Explainable maintenance indicators and historical snapshots | P1 |
| Contributor experience | First-contribution context and onboarding | P1 |
| AI assistance | Optional summaries and recommendations | P1 |

Read [PRD.md](PRD.md), [ARCHITECTURE.md](ARCHITECTURE.md), and [ROADMAP.md](ROADMAP.md) for details.

## Intended technology

- Backend: Laravel / PHP
- Web application: Next.js / TypeScript
- Database: PostgreSQL
- Queue and cache: Redis
- Integration: GitHub App and webhooks
- Deployment: Docker Compose

These are proposed implementation choices, not a claim that the components are already present.

## Development status

The repository is at the project-foundation stage. Initial work covers requirements, architecture, and repository practices. Implementation milestones will be tracked in [ROADMAP.md](ROADMAP.md) and GitHub Issues.

## Contributing

Bug reports, design feedback, documentation improvements, and focused pull requests are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md).

## Security

Do not report undisclosed vulnerabilities in public issues. Follow [SECURITY.md](SECURITY.md).

## Governance

The project is currently stewarded by its founding maintainer. See [GOVERNANCE.md](GOVERNANCE.md).

## License

MaintainerOS is distributed under the Apache License 2.0. See [LICENSE](LICENSE).

---

MaintainerOS is independent community software. It is not affiliated with, endorsed by, or an official product of GitHub, OpenAI, Anthropic, or another platform.
