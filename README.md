# [Project Name]

> One sentence that says what this project does and for whom. Example: "A REST service that lets [users] do [task] in [time or number]."

![Build](https://img.shields.io/badge/build-[status]-lightgrey)
![Coverage](https://img.shields.io/badge/coverage-[xx]%25-lightgrey)
![Version](https://img.shields.io/badge/version-[x.y.z]-blue)

**Status:** [Active | Maintenance only | Paused]
**Current version:** [x.y.z] (see [CHANGELOG.md](CHANGELOG.md))

> Guide: Replace each badge link with the real CI, coverage, and release badge from your tools. Badges that are not wired up should be removed, not left grey.

## 1. Overview

**What it does:** [2 to 3 sentences.]

**Problem it solves:** [Who has the problem, how big it is, and what happens without this project. Use a number if you have one, for example "Support staff spend 6 hours a week on this task."]

**Who uses it:** [End users, internal teams, other services.]

## 2. Key Features

* [Feature 1]
* [Feature 2]
* [Feature 3]

> Guide: Keep this to 3 to 7 items. Details belong in other docs.

## 3. Tech Stack

| Layer | Technology | Version |
|---|---|---|
| Language | [Python / Node / Java / Go] | [x.y] |
| Framework | [FastAPI / Express / Spring] | [x.y] |
| Database | [PostgreSQL / MongoDB / MySQL] | [x.y] |
| Cache or queue | [Redis / RabbitMQ / None] | [x.y] |
| Infrastructure | [Docker / Kubernetes / Cloud provider] | [x.y] |
| CI and CD | [GitHub Actions / GitLab CI / Jenkins] | N/A |

## 4. Quick Start

> Guide: A new person should see the app run in under 10 minutes using 5 commands or fewer. Full steps live in [docs/SETUP.md](docs/SETUP.md).

```bash
git clone [repo url]
cd [repo name]
cp .env.example .env
[install command]
[start command]
```

Open [http://localhost:PORT](http://localhost:PORT) and check that [expected result].

## 5. Documentation Map

| I want to... | Read this |
|---|---|
| Run the project on my machine | [docs/SETUP.md](docs/SETUP.md) |
| Understand how the system is built | [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) |
| Make a code change | [CONTRIBUTING.md](CONTRIBUTING.md) |
| Use or extend the API | [docs/API.md](docs/API.md) |
| Understand the data | [docs/DATABASE.md](docs/DATABASE.md) |
| Test a change or report a bug | [docs/TESTING.md](docs/TESTING.md) |
| See what changed in each version | [CHANGELOG.md](CHANGELOG.md) |
| Ship a release | [docs/RELEASE.md](docs/RELEASE.md) and [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) |
| Fix a production problem | [docs/RUNBOOK.md](docs/RUNBOOK.md) and [docs/INCIDENT_RESPONSE.md](docs/INCIDENT_RESPONSE.md) |
| Join the team | [docs/ONBOARDING.md](docs/ONBOARDING.md) |
| Look up a term | [docs/GLOSSARY.md](docs/GLOSSARY.md) |
| See what is planned | [docs/ROADMAP.md](docs/ROADMAP.md) |
| Report a security problem | [SECURITY.md](SECURITY.md) |
| Ask for help | [SUPPORT.md](SUPPORT.md) |
| Know who decides what | [docs/GOVERNANCE.md](docs/GOVERNANCE.md) |
| Work with AI coding tools | [AGENTS.md](AGENTS.md) |

## 6. Project Layout

```text
[repo name]/
├── src/            [application code]
├── tests/          [unit, integration, end to end tests]
├── docs/           [all long form documentation]
├── scripts/        [helper scripts]
└── .github/        [PR template, issue templates, CI workflows]
```

> Guide: Keep this short. The full explanation of each folder goes in [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## 7. Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) before you open a pull request. All participants follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## 8. Support and Security

* Questions and bugs: [SUPPORT.md](SUPPORT.md)
* Security reports: [SECURITY.md](SECURITY.md). Do not open a public issue for a security problem.

## 9. License

[MIT] License. See [LICENSE](LICENSE). Third party licenses are listed in [docs/THIRD_PARTY_LICENSES.md](docs/THIRD_PARTY_LICENSES.md).

## 10. Contact

| Role | Name | Contact | Ask them about |
|---|---|---|---|
| Project manager | [Name] | [email or chat handle] | Scope, dates, priorities |
| Lead developer | [Name] | [email or chat handle] | Code, design, reviews |
| QA lead | [Name] | [email or chat handle] | Test plans, release sign off |
| On call channel | N/A | [#channel] | Production problems |
