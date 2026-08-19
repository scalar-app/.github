# Releasing

How a release happens across Scalar's repositories.

## What a release is here

Scalar is not a monorepo, so there is no single version number. Each repository releases on its own when it has something worth releasing, and most of them do not release at all yet.

| Repository | Released as | Today |
| --- | --- | --- |
| `desktop` | Installers attached to a GitHub release | Tag driven, draft, unsigned |
| `sdk`, `ui` | npm packages | Not published; consumed with pnpm `link:` from a sibling checkout |
| `api`, `worker` | Container images | Not published; built from source |
| `web` | Static build | Not published; built from source |
| `website` | The public site | Deployed to GitHub Pages on every push to `main` |
| `docs`, `.github`, `infra` | The default branch is the release | Continuous |

Where a repository is not released, `main` is the release. That is a real answer for a project at this stage, not a gap to apologise for.

## Versioning

Semantic versioning, once a thing is published at all. Before 1.0, treat a minor bump as "this may break you" and read the notes.

Nothing is 1.0 yet, and nothing will be until the interfaces stop moving.

## Releasing the desktop app

The only automated release today.

1. Make sure `main` is green.
2. Set the version in `src-tauri/Cargo.toml` and `src-tauri/tauri.conf.json`. They must match.
3. Tag and push:

   ```bash
   git tag v0.1.0
   git push origin v0.1.0
   ```

4. The `Release` workflow builds a universal macOS `.dmg` and a Windows installer and attaches them to a **draft** release.
5. Read the draft. Check both artefacts are attached and the notes say what changed.
6. Publish it.

The draft step is the point. A tag is easy to push by accident; a published release is what people download.

Builds are unsigned, so macOS reports an unidentified developer and Windows SmartScreen warns. Signing certificates cost money and this project has none. The release notes say so.

## Release notes

Generated from merged pull request titles, grouped by the categories in `.github/release.yml`. That is why pull request titles are checked by CI: the title is the changelog entry.

Write titles for somebody reading the notes later, not for the reviewer reading the diff today.

## Publishing a package, when that day comes

Not set up. When `sdk` or `ui` is published to npm it needs an npm account, a token in repository secrets, and a workflow that publishes on a tag. None of that exists yet, and this file will say so until it does rather than describing a process nobody has run.

## Hotfixes

Same as anything else: fix on `main`, tag again. There are no release branches, because with one maintainer and no supported old versions there is nothing to branch from.

## Related

- [GOVERNANCE.md](GOVERNANCE.md)
- [MAINTAINERS.md](MAINTAINERS.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
