<div align="center">

<img src="assets/scalar.png" alt="Scalar" width="112" />

# Scalar

**Your entire life has an inbox. Scalar turns it into a plan.**

Open-source productivity infrastructure for email, calendar, school, projects
and everything else demanding your attention.

<br />

[![License](https://img.shields.io/badge/license-AGPL--3.0-FFD600?style=for-the-badge&labelColor=0d1117)](https://github.com/scalar-app/.github/blob/main/LICENSE)
[![Self-hosted](https://img.shields.io/badge/hosting-self--hosted%20only-FFD600?style=for-the-badge&labelColor=0d1117)](#no-hosted-version)
[![Node](https://img.shields.io/badge/node-24-FFD600?style=for-the-badge&labelColor=0d1117)](https://nodejs.org)
[![TypeScript](https://img.shields.io/badge/typescript-strict-FFD600?style=for-the-badge&labelColor=0d1117)](https://www.typescriptlang.org)

[Website](https://scalar-app.github.io/) &nbsp;·&nbsp;
[Docs](https://github.com/scalar-app/docs) &nbsp;·&nbsp;
[Discussions](https://github.com/orgs/scalar-app/discussions) &nbsp;·&nbsp;
[Roadmap](https://github.com/scalar-app/docs/blob/main/roadmap.md) &nbsp;·&nbsp;
[Contributing](https://github.com/scalar-app/.github/blob/main/CONTRIBUTING.md) &nbsp;·&nbsp;
[Security](https://github.com/scalar-app/.github/blob/main/SECURITY.md)

</div>

---

## What it does

Scalar connects the systems you already use into one action layer, so what needs
doing shows up as a plan instead of a pile.

```
  email     calendar     Canvas      files      tasks
    │          │           │           │          │
    └──────────┴─────┬─────┴───────────┴──────────┘
                     ▼
              integrations
                     ▼
             api  ·  worker            normalize, schedule, sync
                     ▼
                   today               one ordered plan
                     ▼
          web  ·  desktop  ·  mobile
```

Everything above runs on your machine or a server you already have. The
assistant layer (`ai`) uses your own model key and is entirely optional. Without
one, the rest of Scalar works unchanged and the Ask page says so.

## No hosted version

There is no hosted Scalar and none is planned. You run it, your data stays where
you put it. AGPL-3.0, cross platform, no telemetry, no account with us because
there is no us to have an account with.

## Repositories

<table>
<tr><th align="left">Repository</th><th align="left">Purpose</th><th align="left">Ships as</th></tr>

<tr><td><a href="https://github.com/scalar-app/web"><b>web</b></a></td>
<td>Web application, browser client.</td><td>app</td></tr>

<tr><td><a href="https://github.com/scalar-app/desktop"><b>desktop</b></a></td>
<td>Native shell for macOS, Windows, Linux, iOS and Android.</td><td>app</td></tr>

<tr><td><a href="https://github.com/scalar-app/api"><b>api</b></a></td>
<td>HTTP API, auth, workspaces, tasks, events, today view, Command.</td><td>service</td></tr>

<tr><td><a href="https://github.com/scalar-app/worker"><b>worker</b></a></td>
<td>Background jobs: sync, scheduling, notifications.</td><td>service</td></tr>

<tr><td><a href="https://github.com/scalar-app/integrations"><b>integrations</b></a></td>
<td>Provider connectors for email, calendar, Canvas and files.</td><td>service</td></tr>

<tr><td><a href="https://github.com/scalar-app/ai"><b>ai</b></a></td>
<td>The Command loop, tools and model providers.</td><td><code>@scalar/ai</code></td></tr>

<tr><td><a href="https://github.com/scalar-app/sdk"><b>sdk</b></a></td>
<td>Typed client for the API.</td><td><code>@scalar/sdk</code></td></tr>

<tr><td><a href="https://github.com/scalar-app/ui"><b>ui</b></a></td>
<td>Design tokens and components.</td><td><code>@scalar/ui</code></td></tr>

<tr><td><a href="https://github.com/scalar-app/website"><b>website</b></a></td>
<td>Public website.</td><td>site</td></tr>

<tr><td><a href="https://github.com/scalar-app/docs"><b>docs</b></a></td>
<td>Product and developer documentation.</td><td>site</td></tr>

<tr><td><a href="https://github.com/scalar-app/infra"><b>infra</b></a></td>
<td>Deployment, docker compose, infrastructure as code.</td><td>config</td></tr>

<tr><td><a href="https://github.com/scalar-app/.github"><b>.github</b></a></td>
<td>This profile, shared templates, reusable workflows.</td><td>config</td></tr>
</table>

Scalar is not a monorepo. Each repository is independent and each README says
what to clone alongside it.

## Run it

```bash
git clone https://github.com/scalar-app/infra
cd infra
cp .env.example .env
docker compose up
```

Full instructions, including running the clients from source, live in
[docs](https://github.com/scalar-app/docs).

## Contributing

Every repo takes issues and pull requests.

| If you want to | Start at |
| --- | --- |
| Fix or build something | [Contributing guide](https://github.com/scalar-app/.github/blob/main/CONTRIBUTING.md) |
| Find a first task | Issues labeled [`good first issue`](https://github.com/search?q=org%3Ascalar-app+label%3A%22good+first+issue%22+state%3Aopen&type=issues) |
| Ask where a change belongs | [Discussions](https://github.com/orgs/scalar-app/discussions) |
| Understand who decides what | [Governance](https://github.com/scalar-app/.github/blob/main/GOVERNANCE.md) |
| Report a vulnerability | [Security policy](https://github.com/scalar-app/.github/blob/main/SECURITY.md), never a public issue |

<div align="center">
<br />
<sub>AGPL-3.0. Built in the open.</sub>
</div>
