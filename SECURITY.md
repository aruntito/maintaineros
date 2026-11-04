# Security Policy

## Project status

MaintainerOS is in its early foundation stage and is not yet recommended for production use. Security controls described in project documentation are requirements and design intentions until implemented and verified.

## Reporting a vulnerability

Please do not disclose an undisclosed vulnerability in a public GitHub issue, discussion, or pull request.

Use GitHub's **Report a vulnerability** feature in the repository's Security tab when it is enabled. If private vulnerability reporting is not available, contact the repository owner through the private contact channel listed on the GitHub profile and request a secure reporting method. Do not include exploit details in a public message.

A report is most useful when it includes:
- A concise description of the affected component.
- Impact and realistic attack scenario.
- Affected version, commit, or deployment configuration.
- Reproduction steps or a proof of concept that does not access third-party data.
- Suggested mitigation, if known.

Please allow maintainers reasonable time to investigate and coordinate a fix before public disclosure.

## Scope

Potentially relevant issues include:
- Authentication or authorization bypass.
- Cross-workspace or cross-repository data access.
- GitHub token or secret exposure.
- Webhook signature or replay validation failures.
- Unsafe external network requests or SSRF.
- Injection vulnerabilities.
- Unsafe handling of untrusted webhook or AI-generated content.
- Data deletion, retention, or export failures that expose user data.
- Dependency or deployment vulnerabilities affecting MaintainerOS.

## Security design requirements

The project intends to:
- Use least-privilege GitHub App permissions.
- Verify webhook signatures.
- Keep installation tokens and private keys server-side.
- Avoid logging credentials.
- Enforce authorization at the backend.
- Validate untrusted inputs and model outputs.
- Require explicit approval for consequential external actions.
- Support installation revocation and workspace data deletion.

These are target requirements, not a statement that every control is already implemented.

## Supported versions

No production release is currently designated as security-supported. Supported release and patch windows will be documented when versioned releases begin.

## Disclosure

Please do not publish vulnerability details until a coordinated disclosure plan has been agreed with the maintainer. The project will aim to acknowledge reports, communicate status, and publish fixes and advisories when appropriate.
