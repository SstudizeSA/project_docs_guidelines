# Testing Guide

Owner: [QA lead]. Last reviewed: [YYYY-MM-DD]. For developers and testers.

## 1. Goals

* Catch bugs before users do.
* Make every release safe to ship.
* Keep the test suite fast and trusted.

## 2. Test Types

| Type | What it checks | Tool | Share of tests | Speed target | Who writes it |
|---|---|---|---|---|---|
| Unit | One function or class alone | [pytest / Jest / JUnit] | About 70% | Under 5 minutes in total | Developers |
| Integration | Parts working together (API with database) | [Tool] | About 20% | Under 5 minutes in total | Developers |
| End to end | Full user paths in a real browser or client | [Playwright / Cypress] | About 10% | Under 15 minutes in total | QA and developers |
| Manual and exploratory | Things people notice and tools miss | Test cases and notes | As needed | N/A | QA |
| Performance | Speed and load limits | [k6 / Locust] | Before big releases | N/A | QA and developers |
| Security | Common attacks and weak settings | [SAST, dependency scan, DAST] | Every build and before releases | N/A | Developers and security |
| Accessibility (if UI) | Keyboard use, contrast, screen readers | [axe] | Every UI release | N/A | QA |

## 3. Targets

| Measure | Target |
|---|---|
| Line coverage, whole project | 80% or higher |
| Line coverage, critical modules ([auth, payments, billing]) | 90% or higher |
| Coverage change in a pull request | Must not go down |
| CI run time (lint, unit, integration) | Under 10 minutes |
| Flaky tests | 0 allowed on the main branch |
| Open critical or high bugs at release | 0 |

## 4. How to Run Tests

| Goal | Command |
|---|---|
| All unit tests | `[command]` |
| All integration tests | `[command]` |
| End to end tests | `[command]` |
| One file | `[command] [path]` |
| With coverage report | `[command]` |
| Everything CI runs | `[command]` |

## 5. Writing Good Tests

* Name tests by behavior: `test_[thing]_[condition]_[result]`.
* Follow Arrange, Act, Assert. One main reason to fail per test.
* Tests must not depend on order or on each other.
* Do not use real clocks, random values, or the network without control. Freeze time and seed randomness.
* Mock only things you do not own (external services). Do not mock your own database in integration tests.
* A bug fix starts with a test that fails, then the fix.

## 6. Test Data

* Fixtures live in `[tests/fixtures]`. Factories live in `[tests/factories]`.
* Never use real customer data. Use generated or anonymized data.
* Shared test accounts: see [SETUP.md](SETUP.md), section 9.
* Each test creates what it needs and cleans up after.

## 7. Environments

| Environment | Used for | Data | Who deploys |
|---|---|---|---|
| Local | Developer checks | Seed data | Developer |
| CI | Automatic checks on every push | Fresh, empty | CI |
| Staging | QA and release testing | Safe copy of production shape | Pipeline |
| Production | Smoke checks only | Real | Pipeline |

## 8. CI Pipeline

| Stage | Runs | Fails the build when |
|---|---|---|
| 1. Lint and format | [Tools] | Any warning |
| 2. Type check | [Tool] | Any error |
| 3. Unit tests | [Tool] | Any failure |
| 4. Integration tests | [Tool] | Any failure |
| 5. Security scans | Secrets, dependencies, code | High or critical finding |
| 6. Coverage gate | [Tool] | Below target or lower than main |
| 7. Build | Docker image | Build error |
| 8. End to end (on staging deploy) | [Tool] | Any failure |

## 9. Manual Testing

### Test case format

| Field | Content |
|---|---|
| ID | `TC_[area]_[number]` |
| Title | [Action and expected result] |
| Preconditions | [Account, data, settings] |
| Steps | 1. [Step] 2. [Step] |
| Expected result | [What should happen] |
| Priority | [High, Medium, Low] |

### Smoke test (run after every deploy, 15 minutes or less)

* [ ] App loads and health check passes
* [ ] Sign in works
* [ ] [Key action 1] works
* [ ] [Key action 2] works
* [ ] No new errors in logs for 10 minutes

### Regression checklist

Full list: [link or section]. Run before every minor and major release.

## 10. Reporting Bugs (for testers)

Use the **Bug report** template in GitHub. A good report has: version, environment, steps, expected result, actual result, evidence (logs, screenshot, request ID), and impact.

| Severity | Meaning | Example | Fix target |
|---|---|---|---|
| Critical | System down, data loss, security hole | Cannot sign in | Same day |
| High | Main feature broken, no workaround | Orders cannot be saved | Within 3 days |
| Medium | Feature broken, workaround exists | Filter returns wrong order | Within the sprint |
| Low | Cosmetic or rare | Typo, small layout issue | When time allows |

Developers reply within 1 business day. A bug is closed only after the tester confirms the fix.

## 11. Release Testing

1. Read [../CHANGELOG.md](../CHANGELOG.md) for the release. Each entry has Testing notes.
2. Check every Added, Changed, and Fixed item on staging.
3. Run the regression checklist and the smoke test.
4. If the release has a database migration, test the upgrade and the rollback on staging.
5. Record the result in the release ticket. QA gives a written go or no go. See [RELEASE.md](RELEASE.md).

## 12. Flaky Tests

* A test that fails and passes with no code change is flaky.
* Open an issue with label `flaky` at once.
* Fix it or quarantine it within 5 business days. Do not leave it ignored.

## 13. Performance and Load Tests

* Run before releases that change data access or add a major feature.
* Targets: p95 under 300 ms, error rate under 0.5% at [N] requests per second for [N] minutes.
* Results are saved in [location].

## 14. Definition of Tested

A change is tested when: unit and integration tests pass, new behavior has tests, QA checked the acceptance criteria on staging, and no new critical or high bugs are open.
