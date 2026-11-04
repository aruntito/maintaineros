# Open-Source Program Readiness — MaintainerOS

- Owner: project maintainer
- Status: active strategy; application drafts are not claims of current eligibility
- Last criteria review: 2026-11-04
- Project stage at review: early foundation; no implemented product or verified adoption evidence recorded

## Executive decision

Do not submit an application claiming MaintainerOS is already widely adopted or actively used in production. The repository currently contains foundational documentation, not a shipped maintainer product. The strongest path is to build a working, safe GitHub-native maintainer workflow, recruit real maintainers as design partners, publish releases, and collect independently verifiable evidence.

Apply when the evidence is real. The programs allow applicants to explain ecosystem importance even when they do not match every listed signal, but this is not a substitute for an honest account of project maturity.

## Program facts checked against official pages

### OpenAI — Codex for Open Source

Official application: https://openai.com/form/codex-for-oss/

Official program information: https://developers.openai.com/community/codex-for-oss

The program is for maintainers of active open-source projects. OpenAI says it considers meaningful usage, broad adoption, ecosystem importance, and evidence of active maintenance. Examples include PR review, issue triage, release management, and ongoing responsibilities of primary or core maintainers.

The application currently asks for applicant name and ChatGPT account email, public GitHub username and repository URL, primary/core maintainer role, why the repository qualifies (500-character limit), interest in Codex Security and/or API credits, OpenAI Organization ID, API credit use (500-character limit), and additional context (500-character limit).

Potential benefits include six months of ChatGPT Pro with Codex, conditional Codex Security access, and API credits for eligible open-source maintainer workflows. Applications are reviewed on a rolling basis. Benefits are discretionary and not guaranteed.

Program terms: https://learn.chatgpt.com/docs/codex-for-oss-terms

### Anthropic — Claude for Open Source

Official application: https://claude.com/contact-sales/claude-for-oss

The current official page advertises six months of Claude Ultra. Published applicant signals include any of:
- Maintained packages with 500+ dependent repositories; or
- 100+ dependent packages; or
- 200,000+ combined monthly downloads across registries such as npm, PyPI, crates.io, RubyGems, or similar.
- Listed committer/maintainer on a recognized foundation or language project.
- 100+ authored PRs merged into repositories the applicant does not own in the last 12 months.
- 20+ unique external contributors with merged PRs to one of the applicant's repositories in the last 12 months.
- OpenSSF criticality score of 0.4 or above for a maintained repository.

The page explicitly invites applicants who do not fit neatly into those categories but maintain something the ecosystem depends on. That invitation is discretionary, not a waiver or guarantee.

Anthropic states that the complimentary subscription ends after six months; applicants should read the linked terms and understand any subscription-renewal implications before accepting.

## Current gap assessment

| Evidence area | Current known state | Required next proof |
|---|---|---|
| Working product | Not implemented; repository is foundation documentation | Public alpha with documented install and working core workflows |
| Active maintenance | Foundational commits exist; product maintenance history is not yet established | Consistent issue triage, reviewed PRs, changelog and tagged releases |
| Real users | No verified active installations or users recorded | Opt-in design partners and real usage feedback |
| Adoption | No verified stars, downloads, dependent repos or package downloads recorded | Public, timestamped evidence from relevant registries and GitHub |
| External contributors | No verified merged external contributors recorded | Welcoming contribution flow and merged contributions |
| Maintainer responsibility | Founding maintainer is documented as steward | Public evidence of ongoing review, triage, releases and security ownership |
| Security posture | Policy and design intentions documented; controls not yet verified | Implemented tests, dependency scanning, disclosure process and release hygiene |

Do not turn unknown values into zeroes or estimates. Record the date and source for every metric.

## Product strategy: build something maintainers return to

### Wedge

Win one painful recurring workflow before expanding scope:

**A reliable maintainer inbox for GitHub issues and pull requests**, with explainable prioritization, stale-work visibility, review context, and human-approved actions.

Why this wedge:
- It directly maps to the daily maintenance work cited by both programs.
- It can demonstrate value without requiring a large ecosystem or complex AI.
- It creates measurable before/after evidence such as time-to-triage and queue age.
- It gives maintainers a reason to install and use the product repeatedly.

### Release gates

1. **Foundation:** runnable local development, CI, threat model, GitHub App permission rationale, clear docs.
2. **Private alpha:** issue and PR synchronization; idempotent webhook handling; queue UI; no autonomous external writes.
3. **Design-partner beta:** 3–5 independent maintainer teams using it on real repositories, with consent to publish anonymized or attributed case studies.
4. **Public beta:** stable installation guide, privacy/data retention docs, uninstall and data deletion, release notes, support process.
5. **Adoption phase:** repeat usage, external contributions, integrations, reproducible performance and reliability evidence.

Targets above are internal execution goals, not program eligibility thresholds or claims.

## Aggressive 90-day execution plan

### Days 1–14: make the repository contribution-ready
- Add issue forms, pull request template, labels, and a clear first-contribution path.
- Scaffold the proposed Laravel API and Next.js web app only after confirming current supported versions and deployment requirements.
- Add Docker Compose, environment example, CI, tests, formatting and static analysis.
- Publish a GitHub App permission matrix and webhook threat model.
- Add a public project board with scoped P0 issues.

**Exit gate:** a new contributor can run the project locally from a clean checkout; CI validates every PR.

### Days 15–35: ship the first complete workflow
- GitHub App installation and repository selection.
- Signature-verified webhook intake, delivery deduplication, queue processing, retries and reconciliation.
- Issue and PR projections with sync status.
- One useful maintainer inbox with filters and transparent prioritization.
- Audit log for recommendations and approved write actions.

**Exit gate:** a maintainer can connect a test repository and use the inbox without data loss or unsafe permission scope.

### Days 36–60: prove utility with maintainers
- Invite 3–5 maintainers from different project sizes and ecosystems.
- Conduct onboarding sessions and structured feedback interviews.
- Measure time-to-triage, stale issue age, review queue age, sync reliability, weekly active maintainers and repeat usage.
- Fix friction before adding more AI features.
- Publish demo video, setup guide, architecture decision records and first tagged beta.

**Exit gate:** at least three independent teams complete repeated workflows over multiple weeks, and each has a documented outcome. Do not count one-off demos as active use.

### Days 61–90: publish adoption evidence
- Public beta release with security and data handling documentation.
- Publish two or more permissioned case studies with clear methodology.
- Grow external contributor participation through scoped issues and responsive reviews.
- Publish monthly project reports and changelogs.
- Reassess both program applications against actual evidence.

**Exit gate:** application dossier contains current, verifiable metrics and truthful maintainer activity.

## Adoption strategy

### Positioning

"An open-source maintainer inbox that turns GitHub noise into a reviewable, human-controlled maintenance queue."

Avoid positioning MaintainerOS as a generic AI coding agent or a GitHub replacement. Its differentiated value is maintenance operations, transparent context and maintainer control.

### Acquisition channels
- Direct, respectful outreach to maintainers of active projects; ask for workflow feedback, not endorsements.
- Publish technical build notes, short demos and architecture decisions in the open.
- Participate helpfully in relevant open-source communities without spamming or mass-posting.
- Offer a low-friction self-hosted Docker setup.
- Create narrowly scoped first-contribution tasks with acceptance criteria.
- Publish integrations and examples only after they work.
- Ask design partners for permission before using names, logos, quotes or metrics.

### Activation and retention
- First value within 10 minutes of installation: show a useful issue/PR inbox.
- Explain every recommendation and link it to source GitHub data.
- Make disconnect, uninstall and data deletion straightforward.
- Keep core features useful without AI.
- Track repeat weekly use, not vanity signups.

### Metrics to publish monthly
- GitHub stars and forks (context only, not proof of usage).
- Releases and release cadence.
- External contributors with merged PRs, excluding the maintainer's own accounts.
- Issues opened, closed and median first-response time.
- PRs reviewed and merged; review turnaround.
- Verified installations and weekly active maintainer teams, with a clear counting method.
- Workflow outcomes: time-to-triage, stale queue reduction, review backlog reduction.
- Security reports and response status, without exposing sensitive details.

Never publish private repository names, user data, security details or customer metrics without permission.

## Evidence ledger

Maintain a dated record. Each entry must include metric, value, collection date, source URL or export, counting method, and limitations.

| Metric | Value | Date collected | Evidence source | Notes |
|---|---:|---|---|---|
| GitHub stars | TBD | TBD | Repository insights | Do not estimate |
| Monthly downloads | TBD / N/A until package exists | TBD | Registry analytics | Only relevant if published to a registry |
| Dependent repositories | TBD | TBD | Ecosystem/dependency evidence | Preserve query and date |
| External merged contributors (12 months) | TBD | TBD | GitHub PR history | Unique humans, exclude bots and project owners |
| Maintainer teams using beta | TBD | TBD | Opt-in product telemetry / confirmations | Define active usage |
| OpenSSF criticality score | TBD | TBD | OpenSSF project criticality service | Record exact score and date |
| Maintainer work evidence | TBD | TBD | Issues, PR reviews, releases | Link public examples |

## Application readiness scorecard

Use this before applying. A "yes" requires a public link or export.

- [ ] Public repository and clear license.
- [ ] Product is implemented and installable.
- [ ] Maintainer role and repository control are verifiable.
- [ ] Recent issues are triaged and PRs are reviewed consistently.
- [ ] At least one tagged release and changelog exist.
- [ ] Real users or ecosystem impact can be demonstrated.
- [ ] All metrics are dated, sourced and reproducible.
- [ ] Security and privacy documentation matches actual implementation.
- [ ] Requested AI benefit has a specific, bounded project use case.
- [ ] Applicant has reviewed the program's current terms and eligibility requirements.

**Decision rule:** If the product is still docs-only, do not submit an application that implies operational adoption. An exploratory application is only appropriate if it accurately describes the early stage and makes a strong, specific ecosystem-importance case.

## Draft application — OpenAI Codex for Open Source

Application form: https://openai.com/form/codex-for-oss/

These are editable drafts, not a submitted application. Replace every bracketed field with verified information. Keep the form's character limits.

**Maintainer role**
Primary maintainer (only select if accurate and the GitHub repository permissions/activity support it).

**Why does this repository qualify? (max 500 characters)**

> I am the [primary/core] maintainer of MaintainerOS, an open-source GitHub-native workspace focused on reducing maintainer workload across issue triage, pull request coordination and release preparation. The project is currently at [accurate stage]. Evidence: [verified users/installs], [verified activity], and [specific maintainer workflow outcome]. We are addressing [clearly evidenced ecosystem problem] with a self-hostable, human-controlled approach.

**How will you use API credits? (max 500 characters)**

> Credits would support optional, auditable maintainer workflows in MaintainerOS: summarizing issue and PR context, drafting release notes, and generating review checklists. Model output will remain advisory, be validated against structured schemas, and require maintainer approval before any GitHub write. We will measure usefulness and cost against a rules-only baseline and publish reproducible results.

**Anything else? (max 500 characters)**

> GitHub remains the source of truth. MaintainerOS is designed for least-privilege GitHub App access, self-hosting, provider-neutral AI, and explicit human approval for consequential actions. Current maturity: [accurate stage]. Public roadmap, security policy, architecture and contribution process: [links]. We can provide further evidence of maintainer activity and product usage.

**Required private form data:** applicant identity, account email, public GitHub username, repository URL, and OpenAI Organization ID. Enter these directly on the official form; do not publish them in this repository or issue tracker.

## Draft application — Anthropic Claude for Open Source

Application form: https://claude.com/contact-sales/claude-for-oss

The current page lists six months of Claude Ultra and publishes the thresholds above. It also invites maintainers who do not fit the thresholds to explain their ecosystem importance.

**Project reach and impact**

> MaintainerOS is an open-source, self-hostable workspace for the recurring operational work of maintaining GitHub projects: issue triage, pull request coordination, release preparation and contributor onboarding. It is designed to keep GitHub as the source of truth and keep maintainers in control of external actions. Current stage: [accurate stage]. Verified reach: [dependent repos/packages/downloads OR external contributors OR maintainer teams], measured on [date] using [sources]. The gap we address is [specific evidence-backed problem].

**How will you use the subscription for your project?**

> I would use Claude to accelerate implementation and maintenance of MaintainerOS: analyze code changes, draft and improve tests, review security-sensitive webhook and authorization paths, improve documentation, and prototype optional maintainer-assistance workflows. Any model-generated recommendation that affects GitHub state will require human review. I will validate changes with automated tests and publish the resulting improvements openly.

**Other information**

> Public roadmap: [link]. Architecture: [link]. Security policy: [link]. Contribution guide: [link]. Maintainer role: [accurate role]. Recent releases and external contribution activity: [links]. All adoption figures are dated and independently verifiable.

## Application integrity rules

- Never invent stars, downloads, dependent repositories, active users, PRs, contributors, impact metrics or maintainer roles.
- Do not imply that a planned feature is already implemented.
- Do not buy stars, downloads, testimonials or artificial engagement.
- Do not create fake contributors or merge low-value PRs to reach a threshold.
- Do not claim an OpenSSF score or certification without a verifiable result.
- Do not submit confidential user or repository data without authorization.
- Recheck official pages and terms immediately before applying; program benefits and criteria can change.
- Submission is not acceptance. Selection and benefits are discretionary.
