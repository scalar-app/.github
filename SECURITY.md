# Security Policy

This policy covers every repository in the [scalar-app](https://github.com/scalar-app) organization.

## Supported versions

Scalar is pre-1.0. Only the `main` branch of each repository receives security fixes. There are no maintained release branches yet; when tagged releases start, this table will list them.

| Version | Supported |
| --- | --- |
| `main` | Yes |
| Anything else | No |

## Reporting a vulnerability

Do not open a public issue, discussion or pull request for a security problem.

Report privately through GitHub Security Advisories on the affected repository: open the repo, go to the **Security** tab, then **Report a vulnerability**. If the issue spans several repos or you are not sure which one is affected, report it against [scalar-app/api](https://github.com/scalar-app/api/security/advisories/new) and say so.

Include what you can of: affected repo and commit, steps to reproduce or a proof of concept, impact, and any suggested fix. Encrypted email is not offered yet; the advisory form is the private channel.

## Response targets

| Step | Target |
| --- | --- |
| Acknowledge the report | 3 business days |
| Initial assessment and severity | 7 days |
| Fix or mitigation for high and critical issues | 30 days |
| Fix for lower severity issues | 90 days |
| Public disclosure | After a fix is on `main`, coordinated with the reporter |

Reporters are credited in the advisory unless they prefer otherwise.

## Scope

In scope, with particular interest:

- Authentication and sessions (magic links, session cookies, logout, token storage and hashing).
- OAuth flows and stored provider tokens for email, calendar, school and file integrations.
- Authorization: any way to read or modify data outside your workspace membership.
- AI action authorization: an AI-initiated action (send, delete, move, schedule, share) executing without the permission the user granted.
- Prompt injection: content from email, calendar, documents or provider APIs steering the AI into unintended actions or data disclosure.
- Encryption at rest and in transit, secret handling, dependency vulnerabilities with a demonstrated impact.
- The reusable CI workflow in this repo (supply chain, secret exposure).

Out of scope:

- Findings on third-party services (Google, Microsoft, Canvas and others). Report those to the provider.
- Denial of service through volume alone, rate-limit tuning, missing best-practice headers without demonstrated impact.
- Self-hosted deployments configured against the documented defaults.
- Social engineering of maintainers.

## Safe harbor

If you make a good-faith effort to follow this policy we consider your research authorized. We will not pursue or support legal action against you for it, and we will work with you to understand and resolve the issue. Good faith means: do not access, modify or destroy data that is not yours; do not degrade the service for others; use test accounts where possible; stop and report as soon as you have demonstrated the issue; and give us reasonable time to fix before disclosing.

## Security updates

Fixes ship on `main` and are announced through the GitHub Security Advisory for the affected repo. Watch releases or security advisories on the repos you deploy.
