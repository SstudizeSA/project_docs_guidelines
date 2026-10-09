# Onboarding

Welcome to [Project Name]. This plan takes a new developer, tester, or other team member from first day to first shipped change. Owner: [Name]. Ask your buddy for anything that is missing or wrong, and fix this file when you find a gap.

## 1. Who You Will Meet

| Role | Name | Ask them about |
|---|---|---|
| Your buddy | [Name] | Everything, especially small questions |
| Team lead | [Name] | Priorities, work assignments, feedback |
| Project manager | [Name] | Scope, dates, process |
| QA lead | [Name] | Test plans, release checks |
| Platform or DevOps | [Name] | Access, pipelines, environments |
| Security lead | [Name] | Access rules, security questions |

## 2. Before Day 1 (manager and buddy)

* [ ] Laptop ordered and shipped
* [ ] Accounts created (section 3)
* [ ] Buddy assigned
* [ ] Week 1 calendar invites sent
* [ ] First task chosen (a small, safe issue labeled `good first issue`)

## 3. Access Checklist

| System | What for | Request from | Done |
|---|---|---|---|
| Email and calendar | Communication | [IT] | [ ] |
| Chat | Daily talk | [IT] | [ ] |
| Source code host | Code and reviews | [Lead] | [ ] |
| Issue tracker | Tasks | [Lead] | [ ] |
| Password manager | Shared secrets | [IT] | [ ] |
| VPN | Private systems | [IT] | [ ] |
| Package registry | Dependencies | [Platform] | [ ] |
| Cloud console (read only first) | Environments | [Platform] | [ ] |
| Error tracking and dashboards | Monitoring | [Platform] | [ ] |
| Staging environment | Testing | [Platform] | [ ] |
| Documentation space | Reading and writing docs | [Lead] | [ ] |
| Production access | Only after 90 days and training | [Security lead] | [ ] |

Turn on two factor sign in for every account on day 1.

## 4. Day 1

* [ ] Meet your buddy and the team
* [ ] Get your laptop and sign in to the accounts
* [ ] Read [../README.md](../README.md)
* [ ] Read [../CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md)
* [ ] Follow [SETUP.md](SETUP.md) and get the app running (a buddy should help)
* [ ] Post a hello in [channel]

## 5. Week 1

| Day | Focus |
|---|---|
| 2 | Read [ARCHITECTURE.md](ARCHITECTURE.md) and [GLOSSARY.md](GLOSSARY.md). Walk through the code with your buddy for 1 hour. |
| 3 | Read [../CONTRIBUTING.md](../CONTRIBUTING.md) and [TESTING.md](TESTING.md). Run the full test suite. |
| 4 | Start your first task. Ask questions early. |
| 5 | Open your first pull request (draft is fine). Weekly check in with your lead. |

## 6. Month 1 Goals

| By | Goal |
|---|---|
| End of week 1 | App runs locally. First pull request open. |
| End of week 2 | First change merged and deployed to staging. |
| End of week 4 | 3 or more changes shipped. You can explain the main flows in [ARCHITECTURE.md](ARCHITECTURE.md). You have reviewed at least 2 pull requests. |
| Day 30 | Review with your lead: what worked, what was unclear, what to learn next. |

Next steps: by day 60 you work on a medium task alone. By day 90 you can join the on call rotation as a shadow ([RUNBOOK.md](RUNBOOK.md)).

## 7. Role Notes

**Developers:** learn the folder layout, the pull request flow, and how to read logs.
**Testers:** learn the test cases, the bug template, the smoke test, and how releases work ([RELEASE.md](RELEASE.md)).
**Project managers:** learn the roadmap ([ROADMAP.md](ROADMAP.md)), labels, and the release steps.

## 8. How We Work

| Practice | Details |
|---|---|
| Working hours and time zone | [Text] |
| Daily standup | [Time, channel or link] |
| Sprint length | [N weeks]. Planning on [day]. Demo on [day]. Retro on [day]. |
| Main chat channels | [#team, #incidents, #releases, #help] |
| Where decisions are written | ADRs in [adr/](adr/) |
| Time off and sick leave | [How to tell the team] |

## 9. Tools

| Tool | Purpose | Guide |
|---|---|---|
| [IDE] | Coding | [link] |
| [Git client] | Version control | [link] |
| [API client] | Calling the API | [link] |
| [Database client] | Reading data | [link] |

## 10. Reading List in Order

1. [../README.md](../README.md)
2. [SETUP.md](SETUP.md)
3. [ARCHITECTURE.md](ARCHITECTURE.md)
4. [GLOSSARY.md](GLOSSARY.md)
5. [../CONTRIBUTING.md](../CONTRIBUTING.md)
6. [TESTING.md](TESTING.md)
7. [adr/](adr/) (read at least the last 5)
8. [RUNBOOK.md](RUNBOOK.md) and [INCIDENT_RESPONSE.md](INCIDENT_RESPONSE.md)

## 11. Feedback on This Plan

At the end of month 1, tell your lead what was slow, missing, or confusing. Send fixes to this file as a pull request.
