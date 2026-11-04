# Contributing to MaintainerOS

Thank you for considering a contribution. MaintainerOS is at an early foundation stage, so clear feedback, documentation improvements, reproducible bug reports, and small focused pull requests are especially valuable.

## Before starting

1. Read the [README](README.md), [PRD](PRD.md), and [Architecture](ARCHITECTURE.md).
2. Search existing issues and pull requests before opening a new one.
3. For substantial changes, open an issue or discussion first so scope and direction can be agreed.
4. Do not start work on an issue marked as assigned or actively claimed without coordinating with its owner.

## Ways to contribute

- Report reproducible bugs.
- Improve setup and developer documentation.
- Add or improve tests.
- Propose accessible and understandable UX.
- Improve security, reliability, and performance.
- Implement a scoped feature aligned with product requirements.

## Development setup

The application scaffold and exact commands are being established. Until the setup guide is published:

- Check the repository README and current project files.
- Do not assume unimplemented services or commands exist.
- Ask for clarification in the relevant issue when setup instructions are incomplete.
- Never commit secrets, personal access tokens, private keys, or real customer data.

The project will publish verified environment and setup instructions before the first implementation beta.

## Pull request expectations

A good pull request should:
- Solve one focused problem.
- Explain the user impact and approach.
- Link the relevant issue where applicable.
- Include tests for changed behavior.
- Update documentation when behavior or setup changes.
- Pass formatting, lint, test, and build checks.
- Avoid unrelated formatting or generated-file churn.
- Identify security, migration, or compatibility implications.
- Include screenshots or recordings for meaningful UI changes when useful.

Do not include credentials, private repository content, or personal data in tests and fixtures.

## Branch and commit guidance

Use descriptive branch names such as:
- feat/issue-triage
- fix/webhook-deduplication
- docs/self-hosting-guide

Prefer clear commit messages. Conventional Commits are encouraged:
- feat: add issue queue filters
- fix: deduplicate webhook deliveries
- docs: clarify local setup

## Review process

Maintainers review contributions for correctness, security, maintainability, tests, scope, and consistency with project principles.

A review may request changes, ask questions, or close a contribution that is out of scope. No contribution is accepted until merged by an authorized maintainer.

## Security reports

Do not open a public issue for an undisclosed vulnerability. Follow [SECURITY.md](SECURITY.md).

## Code of conduct

Participation is subject to [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## Licensing

By submitting a contribution, you agree that it is provided under the repository's Apache-2.0 license. Do not submit code or assets you do not have the right to contribute.

## Current project stage

MaintainerOS is an early-stage project. Some modules described in the PRD and roadmap do not exist yet. Verify current implementation status before building on a planned interface.
