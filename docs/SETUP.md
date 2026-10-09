# Setup Guide

Goal: a working local copy of [Project Name] in under 30 minutes. If a step fails, check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) before asking for help.

Owner: [Name]. Last tested on a clean machine: [YYYY-MM-DD].

## 1. Prerequisites

| Tool | Required version | Check with | Install from |
|---|---|---|---|
| Git | [2.40 or newer] | `git --version` | [link] |
| [Python / Node / Java / Go] | [x.y or newer] | `[command] --version` | [link] |
| Docker and Docker Compose | [x.y or newer] | `docker --version` | [link] |
| [Database, if not run in Docker] | [x.y] | `[command]` | [link] |
| [Package manager: pip, poetry, npm, pnpm] | [x.y] | `[command]` | [link] |
| [Make or task runner] | [x.y] | `make --version` | [link] |

**Supported operating systems:** macOS [version], Ubuntu [version], Windows 11 with WSL2.

**Hardware:** At least [8 GB] RAM and [10 GB] free disk space.

**Access you need first:** [repo access, package registry token, cloud account, VPN]. See [ONBOARDING.md](ONBOARDING.md).

## 2. Get the Code

```bash
git clone [repo url]
cd [repo name]
git checkout [main]
```

## 3. Environment Variables

```bash
cp .env.example .env
```

Then edit `.env`. These values must be set before the app will start:

| Variable | What to put | Where to get it |
|---|---|---|
| `SECRET_KEY` | Any random string, 32 or more characters | `[command to generate]` |
| `DATABASE_URL` | Your local database address | Default in `.env.example` works with Docker |
| `[SERVICE]_API_KEY` | Sandbox key | [Team password manager, path] |

The full list is in [ENVIRONMENT.md](ENVIRONMENT.md). Never commit `.env`.

## 4. Install

### Option A: Docker (recommended)

```bash
docker compose build
docker compose up -d
```

### Option B: Without Docker

```bash
[create virtual environment or install runtime]
[install dependencies command]
[start database and cache services]
```

## 5. Prepare the Database

```bash
[run migrations command]
[load seed data command]
```

Seed data creates: [N test users, N sample records, test accounts with these roles]. Test logins are listed in [section 9](#9-test-accounts).

## 6. Run the App

| Part | Command | URL or port |
|---|---|---|
| API | `[command]` | http://localhost:[8000] |
| Web | `[command]` | http://localhost:[3000] |
| Worker | `[command]` | N/A |
| API docs | Start the API | http://localhost:[8000]/docs |

## 7. Run the Tests

```bash
[unit tests command]
[integration tests command]
[all checks command]
```

Expected result: [N] tests pass in about [N] minutes. Details are in [TESTING.md](TESTING.md).

## 8. Check That It Works

* [ ] Health check returns OK: `curl http://localhost:[8000]/health`
* [ ] You can log in with a test account
* [ ] You can [perform one key action]
* [ ] Tests pass

## 9. Test Accounts

| Role | Email | Password | Use for |
|---|---|---|---|
| Admin | [admin@example.com] | [Stored in password manager] | Admin features |
| Regular user | [user@example.com] | [Stored in password manager] | Normal flows |

> Guide: Never write real passwords in this file. Local seed passwords are acceptable only if they work on local data alone.

## 10. Editor Setup

* Recommended editor: [VS Code]. Install the extensions in `.vscode/extensions.json`.
* Turn on format on save.
* Install the pre commit hooks: `[command]`.

## 11. Common Setup Errors

| Error | Cause | Fix |
|---|---|---|
| [Port already in use] | Another app uses the port | Change `APP_PORT` or stop the other app |
| [Cannot connect to database] | Database is not running | `docker compose up -d db` |
| [Module not found] | Dependencies not installed | Re run the install command |
| [Migration fails] | Old local data | Reset with section 12 |
| [Permission denied on package registry] | Missing token | See [ONBOARDING.md](ONBOARDING.md) |

## 12. Reset Everything

```bash
docker compose down -v
[remove local build files command]
[run section 4 and 5 again]
```

This deletes all local data.
