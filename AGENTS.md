# AGENTS.md

Instructions for AI coding tools (Claude Code, Copilot, Cursor, and others) that work in this repository. Humans can read it too. If your tool looks for `CLAUDE.md`, make that file a one line pointer to this one.

> Guide: Keep this under 150 lines. Write rules a tool can follow exactly. Update it when a tool makes the same mistake twice.

## 1. Project in 3 Lines

* What it is: [one sentence]
* Main language and framework: [Python 3.12 and FastAPI]
* Where the code lives: `src/`. Tests live in `tests/`.

## 2. Commands

| Task | Command |
|---|---|
| Install | `[command]` |
| Run locally | `[command]` |
| Run all tests | `[command]` |
| Run one test file | `[command]` |
| Lint | `[command]` |
| Format | `[command]` |
| Type check | `[command]` |
| Run all checks before a commit | `[command]` |
| Create a database migration | `[command]` |

## 3. Code Rules

* Follow [CONTRIBUTING.md](CONTRIBUTING.md) for branches, commits, and pull requests.
* Match the style of nearby code.
* Add or update tests for every change.
* Keep changes small and focused. Do not refactor files you were not asked to touch.
* Use the shared logger. No print statements.
* [Add rules your team keeps repeating.]

## 4. Never Do These

* Never commit secrets or edit `.env`. Use `.env.example` for new variables.
* Never edit a database migration that is already merged. Add a new one.
* Never edit generated files in `[path]`.
* Never disable a test or a lint rule to make a check pass.
* Never add a dependency without saying why in the pull request.
* Never run destructive commands (drop table, force push, delete data) without asking.

## 5. Before You Say You Are Done

1. Run the full check command from section 2.
2. Update [CHANGELOG.md](CHANGELOG.md) and any docs the change affects.
3. List what you changed, what you tested, and anything you did not verify.

## 6. Where to Find Things

| Topic | File |
|---|---|
| System design | [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) |
| Data model | [docs/DATABASE.md](docs/DATABASE.md) |
| API rules | [docs/API.md](docs/API.md) |
| Environment variables | [docs/ENVIRONMENT.md](docs/ENVIRONMENT.md) |
| Past decisions | [docs/adr/](docs/adr/) |
| Prompts and model rules | [docs/ml/PROMPTS.md](docs/ml/PROMPTS.md) |
| Terms | [docs/GLOSSARY.md](docs/GLOSSARY.md) |
