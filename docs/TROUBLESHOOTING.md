# Troubleshooting

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. For problems on a developer or tester machine. For production problems use [RUNBOOK.md](RUNBOOK.md).

## How to Use This File

1. Find your error text in the tables below. Use your editor search.
2. Try the fix. If it works, you are done.
3. If it does not work, ask in [channel] with the details listed in [../SUPPORT.md](../SUPPORT.md).
4. When you solve a new problem, add it here in the same pull request. One line per problem is enough.

## 1. Setup and Install

| Symptom or error text | Likely cause | Fix |
|---|---|---|
| `[command not found: tool]` | Tool not installed or not on PATH | Install it. Open a new terminal. See [SETUP.md](SETUP.md). |
| `[Port 8000 already in use]` | Another process uses the port | Find it with `[command]` and stop it, or change `APP_PORT`. |
| `[Cannot connect to database]` | Database not running or wrong address | `docker compose up -d db`. Check `DATABASE_URL`. |
| `[ModuleNotFoundError | Cannot find module]` | Dependencies out of date | Re run `[install command]`. |
| `[Permission denied on registry]` | Missing token | Add your token as in [ONBOARDING.md](ONBOARDING.md). |
| `[Docker: no space left on device]` | Old images and volumes | `docker system prune`. Warning: removes unused data. |

## 2. Running the App

| Symptom | Likely cause | Fix |
|---|---|---|
| App starts, then stops at once | Missing environment variable | Read the first error line. Compare `.env` with [../.env.example](../.env.example). |
| Login fails for a test account | Seed data not loaded | Run `[seed command]`. |
| Changes do not show up | Old build or cache | Restart. Clear `[cache folder]`. Hard refresh the browser. |
| 401 or 403 from the API | Token expired or wrong role | Get a new token. Check the role in [API.md](API.md). |
| Slow on first request | Cold start | Normal. Check again. |

## 3. Database

| Symptom | Likely cause | Fix |
|---|---|---|
| Migration fails: "already exists" | Local data out of sync | Reset with [SETUP.md](SETUP.md), section 12. |
| Migration fails on a column | Merge conflict in migrations | Ask the author of the newer file to rebase and renumber. See [DATABASE.md](DATABASE.md). |
| Tests fail only with an old database | Stale schema | Run migrations on the test database. |

## 4. Tests

| Symptom | Likely cause | Fix |
|---|---|---|
| Test passes alone, fails in the full run | Shared state between tests | Isolate data. Do not rely on order. |
| Fails only in CI | Time zone, file path, or version difference | Run with the CI image: `[command]`. |
| Random failures | Flaky test | Label `flaky` and fix within 5 business days. See [TESTING.md](TESTING.md). |
| Coverage gate fails | New code without tests | Add tests. Do not lower the target. |

## 5. Git and Pull Requests

| Symptom | Likely cause | Fix |
|---|---|---|
| Push rejected | Branch behind remote | `git pull --rebase`, then push. |
| CI says commit message invalid | Wrong format | Amend using the format in [../CONTRIBUTING.md](../CONTRIBUTING.md). |
| Pull request cannot merge | Conflicts or missing approvals | Rebase on `[main]`. Ask a code owner. |
| Secret scan blocks my pull request | A key is in the diff | Remove it, rotate the key, then push again. |

## 6. Collect This Before Asking for Help

* Exact error text and the command you ran
* Your operating system and tool versions
* Output of `git status` and `git log -1`
* Logs with secrets removed
* What you already tried

## 7. Known Problems

| Problem | Workaround | Issue | Fixed in |
|---|---|---|---|
| [Text] | [Text] | [#] | [Version or "open"] |
