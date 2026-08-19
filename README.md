# scalar-app/.github

Organization-wide configuration for [Scalar](https://github.com/scalar-app). GitHub reads this repository specially: files here become defaults for every repo in the org that does not override them, and `profile/README.md` is the organization's public profile page.

## How it fits into Scalar

Scalar is split into one repository per concern (`web`, `api`, `sdk`, `ui`, ...). This repo holds the parts they all share so they do not drift: issue and PR templates, contribution and security policies, the shared label set, and reusable CI workflows. It contains no application code.

## What to edit for what

| You want to change | Edit |
| --- | --- |
| The org profile page on github.com/scalar-app | `profile/README.md` |
| The org logo shown on the profile | Replace `profile/assets/scalar.png` |
| Issue forms offered in every repo | `ISSUE_TEMPLATE/*.yml` |
| Links shown on the "New issue" chooser, blank issues on or off | `ISSUE_TEMPLATE/config.yml` |
| Default pull request body | `PULL_REQUEST_TEMPLATE.md` |
| Contribution rules, code standards | `CONTRIBUTING.md` |
| The label set used by every repo | `.github/labels.yml` |
| Release note categories | `.github/release.yml` |
| Review requirements for this repo | `CODEOWNERS` |
| Code of conduct | `CODE_OF_CONDUCT.md` |
| How decisions get made | `GOVERNANCE.md` |
| What maintaining involves | `MAINTAINERS.md` |
| How a release happens | `RELEASING.md` |
| Vulnerability reporting policy | `SECURITY.md` |
| Where users get help | `SUPPORT.md` |
| Sponsor button | `FUNDING.yml` |
| Dependabot for this repo's own actions | `.github/dependabot.yml` |
| Shared workflows used by other repos | `.github/workflows/reusable-*.yml` |
| CI for this repo | `.github/workflows/ci.yml` |
| License | `LICENSE` |

A repo that has its own `SECURITY.md`, `CONTRIBUTING.md` or issue templates overrides the defaults here.

## Logo

`profile/README.md` shows `profile/assets/scalar.png`: the Scalar mark in `#FFD600` on a transparent background, 512x512. The full resolution source lives in the `website` repository (`public/scalar.png`); regenerate this file from it when the logo changes.

## Reusable workflows

Other repos call these instead of maintaining their own copies. Pin to `@main`; Dependabot in each repo keeps the actions inside them current.

### Node CI

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
jobs:
  ci:
    uses: scalar-app/.github/.github/workflows/reusable-node-ci.yml@main
    with:
      node-version: '24'
      pnpm-version: '11.17.0'
      working-directory: '.'
```

Inputs: `node-version` (default `24`), `pnpm-version` (default `11.17.0`), `working-directory` (default `.`), `run-build` (default `true`). It runs `pnpm install --frozen-lockfile`, `pnpm lint`, `pnpm typecheck`, `pnpm test`, `pnpm build`.

### PR title check

Enforces the Conventional Commits titles that `CONTRIBUTING.md` requires. Maintainers squash on merge, so the PR title becomes the commit message.

```yaml
name: PR title
on:
  pull_request_target:
    types: [opened, edited, reopened, synchronize]
jobs:
  title:
    uses: scalar-app/.github/.github/workflows/reusable-pr-title.yml@main
```

Input: `scopes`, a newline separated allowlist. Empty (the default) allows any scope.

### Label sync

Applies `.github/labels.yml` to the calling repository, so every repo shares one label set.

```yaml
name: Labels
on:
  schedule:
    - cron: '0 6 * * 1'
  workflow_dispatch:
jobs:
  sync:
    uses: scalar-app/.github/.github/workflows/reusable-label-sync.yml@main
```

Inputs: `delete-other-labels` (default `false`, set it to `true` only after checking a `dry-run`), `dry-run` (default `false`). Run it once with `workflow_dispatch` after adding it.

Reusable workflows must live under `.github/workflows/` inside the repository, which is why this repo has a nested `.github/` directory. `dependabot.yml`, `labels.yml` and `release.yml` live there for the same reason.

## Layout

```
profile/README.md              org profile
profile/assets/                logo (scalar.png)
ISSUE_TEMPLATE/                issue forms and chooser config
PULL_REQUEST_TEMPLATE.md
CODEOWNERS                     review requirements for this repo
CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
SUPPORT.md
FUNDING.yml
.github/dependabot.yml
.github/labels.yml                      shared label set
.github/release.yml                     release note categories
.github/workflows/ci.yml                lint for this repo
.github/workflows/pr-title.yml          caller: PR title check
.github/workflows/labels.yml            caller: label sync
.github/workflows/reusable-node-ci.yml      shared CI
.github/workflows/reusable-pr-title.yml     shared PR title check
.github/workflows/reusable-label-sync.yml   shared label sync
LICENSE                        AGPL-3.0
```

## Status

- Templates, policies, labels and workflows are complete.
- `FUNDING.yml` is commented out until sponsorship is configured.
- `CODE_OF_CONDUCT.md` has a placeholder contact address that maintainers must replace.
- `CODEOWNERS` references `@scalar-app/maintainers`, which must exist as an org team before GitHub will honor it.
- This repo calls its own shared workflows through `.github/workflows/pr-title.yml` and `.github/workflows/labels.yml`. Other repos still need the equivalent callers added, using the `uses: scalar-app/.github/...@main` form shown above.
- `labels.yml` runs weekly and on demand. Trigger it once with `workflow_dispatch` and `dry-run` enabled before relying on it.

## License

AGPL-3.0, see [LICENSE](LICENSE).
