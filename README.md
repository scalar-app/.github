# scalar-app/.github

Organization-wide configuration for [Scalar](https://github.com/scalar-app). GitHub reads this repository specially: files here become defaults for every repo in the org that does not override them, and `profile/README.md` is the organization's public profile page.

## How it fits into Scalar

Scalar is split into one repository per concern (`web`, `api`, `sdk`, `ui`, ...). This repo holds the parts they all share so they do not drift: issue and PR templates, contribution and security policies, and a reusable CI workflow. It contains no application code.

## What to edit for what

| You want to change | Edit |
| --- | --- |
| The org profile page on github.com/scalar-app | `profile/README.md` |
| The org logo shown on the profile | Replace `profile/assets/scalar.png` |
| Issue forms offered in every repo | `ISSUE_TEMPLATE/*.yml` |
| Links shown on the "New issue" chooser, blank issues on or off | `ISSUE_TEMPLATE/config.yml` |
| Default pull request body | `PULL_REQUEST_TEMPLATE.md` |
| Contribution rules, labels, code standards | `CONTRIBUTING.md` |
| Code of conduct | `CODE_OF_CONDUCT.md` |
| Vulnerability reporting policy | `SECURITY.md` |
| Where users get help | `SUPPORT.md` |
| Sponsor button | `FUNDING.yml` |
| Dependabot for this repo's own actions | `.github/dependabot.yml` |
| Shared CI job used by other repos | `.github/workflows/reusable-node-ci.yml` |
| CI for this repo | `.github/workflows/ci.yml` |
| License | `LICENSE` |

A repo that has its own `SECURITY.md`, `CONTRIBUTING.md` or issue templates overrides the defaults here.

## Logo

`profile/README.md` shows `profile/assets/scalar.png`: the Scalar mark in `#FFD600` on dark, 512x512. The full resolution source lives in the `website` repository (`public/scalar.png`); regenerate this file from it when the logo changes.

## Reusable CI

Other repos call the shared workflow instead of maintaining their own steps:

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

Reusable workflows must live under `.github/workflows/` inside the repository, which is why this repo has a nested `.github/` directory. `dependabot.yml` lives there for the same reason.

## Layout

```
profile/README.md              org profile
profile/assets/                logo (scalar.png)
ISSUE_TEMPLATE/                issue forms and chooser config
PULL_REQUEST_TEMPLATE.md
CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
SUPPORT.md
FUNDING.yml
.github/dependabot.yml
.github/workflows/ci.yml                lint for this repo
.github/workflows/reusable-node-ci.yml  shared CI
LICENSE                        AGPL-3.0
```

## Status

- Templates, policies and workflows are complete.
- `FUNDING.yml` is commented out until sponsorship is configured.
- `CODE_OF_CONDUCT.md` has a placeholder contact address that maintainers must replace.
- Logo not yet added.

## License

AGPL-3.0, see [LICENSE](LICENSE).
