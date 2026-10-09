# Contributing

Thank you for helping build [Project Name]. This guide explains how to get a change from idea to production. Everyone who contributes follows the [Code of Conduct](CODE_OF_CONDUCT.md).

## 1. Before You Start

1. Set up your machine with [docs/SETUP.md](docs/SETUP.md).
2. Find or create an issue for your work. Every change needs an issue.
3. Comment on the issue to claim it. One person per issue.
4. For changes that touch design, data, or public APIs, agree on the approach first. Write an ADR in [docs/adr/](docs/adr/) if the decision is big.

## 2. Workflow in 8 Steps

1. Create a branch from `[main | develop]`.
2. Make small, focused commits.
3. Run lint, format, and tests locally.
4. Update docs and [CHANGELOG.md](CHANGELOG.md).
5. Open a pull request using the template.
6. Fix review comments.
7. Get the required approvals and a green CI run.
8. The merger squashes and merges. Delete the branch.

## 3. Branch Naming

Pattern: `[type]/[issue number]_[short_description]`

| Type | Use for | Example | Branch from | Merge into |
|---|---|---|---|---|
| `feature` | New behavior | `feature/142_export_reports` | `[main]` | `[main]` |
| `bugfix` | Fix for a bug | `bugfix/188_wrong_total` | `[main]` | `[main]` |
| `hotfix` | Urgent production fix | `hotfix/201_login_crash` | latest release tag | `[main]` and release branch |
| `release` | Release preparation | `release/1.2.0` | `[main]` | `[main]` |
| `chore` | Build, tools, dependencies | `chore/150_upgrade_lint` | `[main]` | `[main]` |
| `docs` | Documentation only | `docs/160_update_setup` | `[main]` | `[main]` |

Rules:
* Use lowercase letters, numbers, and underscores in the description.
* Keep the whole name under 50 characters.
* Never commit directly to `[main]`. It is protected.

## 4. Commit Messages

Format (Conventional Commits):

```text
type(scope): short summary in the imperative

Optional body: explain why the change was made, not what the code does.

Refs: #142
```

| Type | Meaning |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no code change |
| `refactor` | Code change that is not a fix or feature |
| `perf` | Speed improvement |
| `test` | Add or fix tests |
| `build` | Build system or dependencies |
| `ci` | CI configuration |
| `chore` | Other maintenance |
| `revert` | Undo an earlier commit |

Rules:
* Summary: 72 characters or fewer, no period, imperative ("add", not "added").
* Body lines wrap at 100 characters.
* Mark breaking changes with `!` after the type (`feat!: remove v1 endpoint`) and a `BREAKING CHANGE:` line in the body.
* One logical change per commit.

## 5. Pull Requests

**Size:** Keep a pull request under about 400 changed lines. Larger changes are split into steps that each work on their own.

**Title:** Same format as a commit summary, for example `feat(reports): add CSV export`.

**Checklist before you request review:**
* [ ] Linked issue
* [ ] Lint and format pass
* [ ] Tests added or updated, and all pass
* [ ] Coverage did not drop
* [ ] Docs updated (README, API, SETUP, or other files that apply)
* [ ] CHANGELOG entry added
* [ ] No secrets, tokens, or personal data in the diff
* [ ] Database migration included and reversible, if the schema changed
* [ ] Screenshots attached for visual changes

**Approvals and merging:**

| Change type | Approvals needed | Who can merge |
|---|---|---|
| Normal change | 1 | Any maintainer |
| Auth, payments, database migrations, infrastructure | 2, one from a code owner | Code owner |
| Docs only | 1 | Any maintainer |
| Hotfix | 1, can follow after merge within 1 business day | Lead developer |

* Merge method: [squash and merge | rebase | merge commit]. Pick one and use it always.
* CI must be green. Do not bypass failed checks.
* Authors do not approve their own pull requests.

## 6. Code Review Rules

**Authors:**
* Reply to every comment, even if only "done".
* Do not push unrelated changes into a review.

**Reviewers:**
* Start the first review within 24 hours (1 business day).
* Check in this order: correctness, tests, security, readability, style.
* Mark small style points as "nit" so the author knows they are optional.
* Approve when the code is good enough to ship, not when it matches your own style.

## 7. Coding Standards

| Area | Rule |
|---|---|
| Language version | [Python 3.12 / Node 20 / other] |
| Formatter | [Black / Prettier / gofmt], run on save and in CI |
| Linter | [Ruff / ESLint / golangci lint], zero warnings allowed in CI |
| Type checks | [mypy / TypeScript strict], required for new code |
| Naming | [snake_case for functions, PascalCase for classes] |
| Function size | Aim for under 40 lines. Split larger ones. |
| File size | Aim for under 400 lines. |
| Errors | Never swallow errors silently. Log with context or raise. |
| Logging | Use the shared logger. No print statements. Never log secrets or personal data. |
| Secrets | Read from environment variables only. See [docs/ENVIRONMENT.md](docs/ENVIRONMENT.md). |
| Dependencies | Add new ones only with a reason in the pull request. Check the license. |
| Comments | Explain why, not what. Remove dead code instead of commenting it out. |

Run all checks with one command: `[make check | npm run check]`.

## 8. Testing Rules

* New code needs tests. A bug fix needs a test that failed before the fix.
* Coverage target: 80% overall, 90% for critical modules. See [docs/TESTING.md](docs/TESTING.md).
* Do not skip or delete tests to get a green build.

## 9. Definition of Done

A task is done only when all items are true:
* [ ] Code reviewed and approved
* [ ] Tests written and passing in CI
* [ ] Lint and format clean
* [ ] Docs and CHANGELOG updated
* [ ] Works on staging
* [ ] QA verified against the acceptance criteria
* [ ] No new known critical or high bugs

## 10. Issues and Labels

| Label | Meaning |
|---|---|
| `bug` | Something is broken |
| `feature` | New capability |
| `chore` | Maintenance |
| `docs` | Documentation |
| `good first issue` | Small task for new contributors |
| `needs triage` | New, not yet reviewed |
| `blocked` | Waiting on something else |
| `priority: critical` | Production is down or data is at risk. Start now. |
| `priority: high` | Fix this sprint |
| `priority: medium` | Plan within a month |
| `priority: low` | When time allows |

**Triage:** [Role] reviews new issues every [weekday or daily]. Each issue gets a type, a priority, and an owner within 2 business days.

## 11. Getting Help

* Questions: see [SUPPORT.md](SUPPORT.md)
* Process problems or review disputes: ask the lead developer, [Name].
