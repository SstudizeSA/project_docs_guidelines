# Environment Variables

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. The sample file is [../.env.example](../.env.example). Every variable in the code must appear in both files.

## 1. Rules

1. Real secrets never go in Git, chat, tickets, or screenshots.
2. `.env` is local only and is listed in `.gitignore`.
3. Staging and production values live in [secret manager name]. Local values come from `.env.example`.
4. Use different secrets in every environment. Never reuse a production secret elsewhere.
5. The app must fail at startup with a clear message if a required variable is missing.
6. Add a variable: update the code, `.env.example`, this file, and the deploy config in the same pull request.
7. Rotate secrets every [90 days] and right away if one may have leaked ([RUNBOOK.md](RUNBOOK.md)).

## 2. Variable Reference

| Variable | Required | Type | Default | Secret | Used by | Description | Example (safe) |
|---|---|---|---|---|---|---|---|
| `APP_ENV` | Yes | string | `development` | No | All | Environment name | `staging` |
| `APP_PORT` | No | integer | `8000` | No | API | Port to listen on | `8000` |
| `APP_DEBUG` | No | boolean | `false` | No | API | Extra error detail. Must be `false` outside local. | `true` |
| `LOG_LEVEL` | No | string | `INFO` | No | All | Log detail | `DEBUG` |
| `SECRET_KEY` | Yes | string | none | Yes | API | Signing key, at least 32 random characters | `change_me` |
| `DATABASE_URL` | Yes | string | none | Yes | API, worker | Database connection string | `postgresql://user:password@localhost:5432/app` |
| `REDIS_URL` | Yes | string | none | Yes | API, worker | Cache and queue address | `redis://localhost:6379/0` |
| `[SERVICE]_API_KEY` | Yes | string | none | Yes | API | Key for [service] | `change_me` |
| `SENTRY_DSN` | No | string | empty | Yes | All | Error tracking address | empty |
| `FEATURE_[NAME]_ENABLED` | No | boolean | `false` | No | API | Turns a feature on | `true` |

> Guide: Keep this table in the same order as `.env.example`. Add one row per variable.

## 3. Values per Environment

| Variable | Local | Staging | Production |
|---|---|---|---|
| `APP_ENV` | `development` | `staging` | `production` |
| `APP_DEBUG` | `true` | `false` | `false` |
| `LOG_LEVEL` | `DEBUG` | `INFO` | `INFO` |
| `DATABASE_URL` | Docker database | Managed staging database | Managed production database |
| `[SERVICE]_API_KEY` | Sandbox key | Sandbox key | Live key |

## 4. Where Secrets Live and Who Can Read Them

| Environment | Store | Read access | Write access |
|---|---|---|---|
| Local | Your own `.env` | You | You |
| Staging | [Secret manager path] | Developers, QA | Platform team |
| Production | [Secret manager path] | Platform team, on call (logged) | Platform team with 2 approvals |

## 5. How to Add or Change a Variable

1. Add it to the code with a clear name. Use upper case with underscores.
2. Add it to `.env.example` with a safe sample value and a comment.
3. Add a row to the table in section 2.
4. Add it to the deploy config for each environment.
5. Mention it under "Deployment Notes" in the pull request.
6. Set the value in staging first. Test. Then production.

## 6. Checking Your Setup

```bash
[command that validates required variables, for example: python -m app.check_env]
```

## 7. If a Secret Leaks

1. Rotate it now. Do not wait to investigate.
2. Remove it from Git history if it was committed (ask the platform team).
3. Check logs for use of the old value.
4. Report to the security lead. See [../SECURITY.md](../SECURITY.md).
