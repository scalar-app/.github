# Maintainers

Who maintains Scalar, what that involves, and how somebody else could.

## Current maintainers

| Repository area | Maintainer |
| --- | --- |
| Everything | [@martin-k-m](https://github.com/martin-k-m) |

One person, all repositories. `CODEOWNERS` in this repository names that account directly rather than a team, because a team that does not exist is silently ignored by GitHub and would mean no review was requested at all.

## What a maintainer is expected to do

- **Reply.** Every issue and pull request gets a response. A quick no is better than silence for a month.
- **Say why.** Anything closed unmerged gets a reason.
- **Keep main releasable.** CI stays green. A red main branch gets fixed or reverted, not left.
- **Review for correctness first.** Then for scope, then for style. Style is what the formatter says; it is not worth a round trip.
- **Not merge your own risky work unreviewed.** With one maintainer that is unavoidable for most changes, so the substitute is tests: anything with real consequences is expected to arrive with them.

## What a maintainer is not expected to do

- Respond within any particular time. Nobody is paid for this.
- Support forks or deployments.
- Take on work because somebody asked loudly.
- Keep a feature nobody uses alive out of politeness.

## Becoming one

There is no application. The path is ordinary and slow:

1. Land a few changes that did not need much rework.
2. Review somebody else's pull request usefully.
3. Stay around long enough that handing you the keys is obviously less risky than not.

At that point you get commit access to a repository you have been working in, and `CODEOWNERS` names you for it. Access follows demonstrated care rather than a formal vote, because with a project this size a vote would be theatre.

## Standing down

Say so and remove yourself from `CODEOWNERS`. No notice period and no handover ritual. Everything is public, so nothing is lost when somebody leaves.

## If the maintainer disappears

This is worth writing down for an unpaid project, because it is a real risk rather than a hypothetical one.

Everything needed to continue Scalar is public: source, history, issues and documentation, under AGPL-3.0. If the maintainer stops responding for a long stretch, fork it. That is not a hostile act, it is what the licence is for. A fork that is actively maintained is more useful than an archive that is not.

## Related

- [GOVERNANCE.md](GOVERNANCE.md)
- [RELEASING.md](RELEASING.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
