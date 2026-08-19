# Contributing to Scalar

This guide applies to every repository under [github.com/scalar-app](https://github.com/scalar-app). Individual repos may add repo-specific notes in their own README.

## How the organization is organized

Scalar is not a monorepo. Each concern is its own repository:

| Repo | Concern |
| --- | --- |
| `web`, `mobile`, `desktop` | Clients |
| `api` | HTTP API, auth, data model |
| `worker` | Background jobs |
| `integrations` | Provider connectors |
| `ai` | Planning and triage models, prompts, evaluation |
| `sdk` | `@scalar/sdk`, typed API client |
| `ui` | `@scalar/ui`, design tokens and components |
| `website`, `docs` | Public site and documentation |
| `infra` | Deployment and infrastructure |
| `.github` | This repo: org profile, shared templates, reusable workflows |

Shared packages (`sdk`, `ui`) are consumed by other repos as npm packages. Before they are published, clients link them locally with pnpm's `link:` protocol; each consuming repo's README explains what to clone alongside it.

If you are not sure which repo a change belongs to, open a [Discussion](https://github.com/orgs/scalar-app/discussions) first.

## Local setup

Every Node repo expects:

- Node 24 (each repo has an `.nvmrc`).
- pnpm 11 (pinned through `packageManager` in `package.json`; `corepack enable` picks it up).
- Docker and `docker compose` for repos that need Postgres or other services (`api`, `worker`, `infra`). Those repos ship a `docker-compose.yml` and an `.env.example`.

Standard scripts in every package:

```
pnpm install
pnpm dev
pnpm lint
pnpm typecheck
pnpm test
pnpm build
pnpm format
```

CI runs install, lint, typecheck, test and build on every push to `main` and every pull request. Run the same locally before opening a PR.

## Branches and commits

Branch names: `feat/short-description`, `fix/short-description`, `refactor/...`, `docs/...`, `chore/...`.

Commits and PR titles follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(api): add cursor pagination to GET /tasks
fix(web): keep focus ring visible on keyboard navigation
docs: explain link: setup for sdk and ui
```

Scope is optional. Use `!` or a `BREAKING CHANGE:` footer for breaking changes.

## Pull request process

1. Open an issue or Discussion for anything larger than a small fix, so the approach is agreed before you write code.
2. Fork or branch, make the change, keep the PR focused on one thing.
3. Fill in the PR template (summary, why, changes, testing, risks).
4. CI must be green. Address review comments with new commits; maintainers squash on merge.
5. One maintainer approval is required. Changes touching auth, OAuth, tokens, email or file access, AI actions, permissions or encryption need a second review from someone on the security rotation.

Small documentation fixes can skip step 1.

## Code standards

- TypeScript strict mode with `noUncheckedIndexedAccess`. No `any`; use `unknown` and narrow.
- ESM only. ESLint 9 flat config and Prettier are the source of truth for style; do not argue formatting in review.
- Small files and small functions. Split when a file stops fitting on a screen or two.
- No filler comments. Comment why, not what. No TODO spam; open an issue instead.
- No placeholder implementations presented as finished. If something is not done, say so in the README under "Status".
- Authorization is enforced in the service layer, never only in the UI.
- Tests with Vitest. Playwright only where end-to-end coverage is required.
- Writing: no em dashes, no marketing language in READMEs.

## Labels

Every repo uses the same label set, defined in [`.github/labels.yml`](https://github.com/scalar-app/.github/blob/main/.github/labels.yml) and applied by the shared label sync workflow. Edit that file rather than creating labels in the GitHub UI.

Area (one per issue or PR):
`area:web`, `area:mobile`, `area:desktop`, `area:api`, `area:worker`, `area:integrations`, `area:ai`, `area:sdk`, `area:ui`, `area:website`, `area:docs`, `area:infra`

Type:
`type:bug`, `type:feature`, `type:refactor`, `type:docs`, `type:chore`, `type:security`

Priority:
`priority:p0` (drop everything, data loss or security), `priority:p1` (next release), `priority:p2` (planned), `priority:p3` (someday)

Plus `good first issue` and `help wanted` for onboarding.

## Discussions vs Issues

- Discussions: questions, ideas, design proposals, "how do I", show and tell.
- Issues: confirmed bugs and agreed feature work with a clear definition of done.

Maintainers convert Discussions into Issues once there is a decision.

## License and contribution terms

Scalar is licensed under AGPL-3.0. There is no CLA and no DCO sign-off requirement. By submitting a contribution you agree that it is licensed under the same AGPL-3.0 terms as the project (inbound = outbound), and that you have the right to submit it.

## Code of conduct

Everyone participating is expected to follow the [Code of Conduct](CODE_OF_CONDUCT.md).
