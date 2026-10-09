# Governance and Maintainers

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. This file says who owns what and how decisions get made. File level review rules are in [../CODEOWNERS](../CODEOWNERS).

## 1. Roles

| Role | Duties | Can merge | Can release |
|---|---|---|---|
| Project manager | Scope, schedule, priorities, stakeholders | No | Approves |
| Lead developer | Technical direction, final say on design disputes | Yes | Yes |
| Maintainer | Reviews and merges pull requests in own area | Yes | No |
| Contributor | Proposes changes through pull requests | No | No |
| QA lead | Test strategy, release go or no go | No | Signs off |
| Security lead | Security policy, reviews sensitive changes | Yes, in own area | Can block |
| Platform lead | Pipelines, infrastructure, environments | Yes, in own area | Runs deploys |

## 2. Maintainers by Area

| Area | Folders | Primary | Backup |
|---|---|---|---|
| API | `src/api`, `src/services` | [Name] | [Name] |
| Frontend | `src/web` | [Name] | [Name] |
| Database | `migrations`, `src/repositories` | [Name] | [Name] |
| Infrastructure | `infra`, `.github/workflows` | [Name] | [Name] |
| Tests and QA | `tests` | [Name] | [Name] |
| Documentation | `docs` | [Name] | [Name] |

Every area has at least 2 people. If one leaves, the lead developer names a new one within [2 weeks].

## 3. How Decisions Are Made

| Decision | Who decides | How | Written down in |
|---|---|---|---|
| Small code change | Author and reviewer | Pull request review | The pull request |
| Design or library choice | Lead developer, after input from maintainers | Discussion, then ADR | [adr/](adr/) |
| Roadmap priorities | Project manager, with lead developer | Quarterly planning | [ROADMAP.md](ROADMAP.md) |
| Release go or no go | Release manager with QA lead | Checklist | [RELEASE.md](RELEASE.md) |
| Security policy | Security lead | Review | [../SECURITY.md](../SECURITY.md) |
| Conduct reports | Conduct contact | Private process | [../CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md) |

**When people disagree:**
1. Each side writes its view in 3 to 5 lines with facts and numbers.
2. If not settled in 2 business days, the lead developer decides (technical) or the project manager decides (scope and schedule).
3. The decision and the reason are recorded. The group commits to it, and anyone may ask to reopen it when new facts appear.

## 4. Becoming a Maintainer

* Criteria: [N or more merged changes], [N reviews done], follows the guide, and is trusted by the team.
* Process: a current maintainer proposes. The lead developer approves. The change is made in this file and in `CODEOWNERS`.
* Stepping down: tell the lead developer. Handover notes are written first.

## 5. Meetings and Rhythm

| Meeting | When | Who | Output |
|---|---|---|---|
| Standup | [Daily, 15 minutes] | Team | Blockers |
| Planning | [Every N weeks] | Team | Sprint plan |
| Review or demo | [Every N weeks] | Team and stakeholders | Feedback |
| Retrospective | [Every N weeks] | Team | Action items |
| Docs review | Quarterly | Maintainers | Stale docs fixed or removed |
| Roadmap review | Monthly | Project manager, lead developer | Updated roadmap |

## 6. Documentation Ownership

| File | Owner |
|---|---|
| README, ROADMAP | Project manager |
| SETUP, CONTRIBUTING, ARCHITECTURE, API, DATABASE, ADRs | Lead developer |
| TESTING, RELEASE | QA lead |
| DEPLOYMENT, RUNBOOK, MONITORING, DISASTER_RECOVERY, ENVIRONMENT | Platform lead |
| SECURITY, PRIVACY | Security lead |
| INCIDENT_RESPONSE | Platform lead |
| ONBOARDING, GLOSSARY, TROUBLESHOOTING | Whole team, coordinated by [Name] |

An owner makes sure the file is correct and reviews it every quarter. Other people may edit it through pull requests.

## 7. Escalation

If a problem cannot be solved at team level, go to: lead developer, then project manager, then [executive sponsor].
