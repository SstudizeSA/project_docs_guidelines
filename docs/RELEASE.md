# Release Process

Owner: [Release manager]. Last reviewed: [YYYY-MM-DD]. Deploy mechanics are in [DEPLOYMENT.md](DEPLOYMENT.md). This file covers who decides and what must be true.

## 1. Release Types

| Type | Version change | Cadence | Approval needed | Example |
|---|---|---|---|---|
| Major | X.0.0 | [As needed, planned 4 weeks ahead] | Project manager, lead developer, QA lead | Removes an old API |
| Minor | x.Y.0 | [Every 2 weeks] | Lead developer, QA lead | New feature |
| Patch | x.y.Z | [As needed] | Lead developer | Bug fix |
| Hotfix | x.y.Z | Immediately | Lead developer (review follows within 1 business day) | Production crash |

## 2. Roles

| Role | Person | Duty |
|---|---|---|
| Release manager | [Name] | Owns the checklist and the timeline |
| Lead developer | [Name] | Confirms code is ready |
| QA lead | [Name] | Gives the written go or no go |
| Deployer | [Name] | Runs the production deploy |
| Communicator | [Name] | Sends release notes and notices |

## 3. Timeline for a Minor Release

| When | Step |
|---|---|
| T minus 3 business days | Code freeze. Only fixes for release blockers after this point. |
| T minus 2 days | Release branch or tag candidate built. Deployed to staging. |
| T minus 2 to 1 days | QA testing and regression pass ([TESTING.md](TESTING.md)). |
| T minus 1 day | Go or no go meeting (15 minutes). |
| T | Production deploy in the allowed window. Post deploy checks. |
| T plus 1 day | Review: any issues, user feedback, metrics. |

## 4. Release Checklist

**Code and tests**
* [ ] All planned items merged, nothing extra added after freeze
* [ ] CI green on the release candidate
* [ ] No open critical or high bugs
* [ ] Coverage at or above target
* [ ] Security scans clean (no high or critical findings)

**Documentation**
* [ ] [../CHANGELOG.md](../CHANGELOG.md) moved from Unreleased to the new version with the date
* [ ] Testing notes filled in for every entry
* [ ] API and setup docs updated
* [ ] Breaking changes and migration steps written in plain words

**Data and config**
* [ ] Migrations tested on staging, including rollback
* [ ] New environment variables added in every environment ([ENVIRONMENT.md](ENVIRONMENT.md))
* [ ] Feature flags set as planned
* [ ] Backup taken if data changes

**People**
* [ ] QA written go
* [ ] On call person informed
* [ ] Support team informed of changes users will see
* [ ] Rollback plan reviewed

## 5. Version Bump Steps

1. Choose the version number using the rules in [../CHANGELOG.md](../CHANGELOG.md).
2. Update the version in: `[file 1]`, `[file 2]`.
3. Update the CHANGELOG and the compare links.
4. Commit: `chore(release): vX.Y.Z`.
5. Tag: `git tag -a vX.Y.Z -m "Release X.Y.Z"` and push the tag.
6. The pipeline builds and publishes the artifacts for that tag.
7. Create the release notes on [GitHub Releases | other tool].

## 6. Go or No Go Rules

**No go if any is true:** open critical or high bug, failed regression test, migration not tested, missing rollback plan, QA lead not available to sign off.

**Record the decision:**

| Item | Value |
|---|---|
| Version | [x.y.z] |
| Date | [YYYY-MM-DD] |
| Decision | [Go | No go] |
| Signed off by | [Names] |
| Known issues shipped | [List with ticket numbers, or "none"] |

## 7. Release Notes Template

```text
# Release [x.y.z] ([YYYY-MM-DD])

Highlights
* [What users will notice, in plain words]

Added
* [Item]

Changed
* [Item]

Fixed
* [Item]

Upgrade notes
* [Steps users or operators must take, or "none"]

Known issues
* [Item, or "none"]
```

## 8. Release Notes Audience

| Audience | Where | Content |
|---|---|---|
| Developers and testers | CHANGELOG and release page | Technical detail |
| Support and sales | [Channel or email] | What changed for users, with screenshots |
| Customers | [Blog, in app notice, email] | Plain description of benefits |

## 9. Hotfix Release

Follow the hotfix steps in [DEPLOYMENT.md](DEPLOYMENT.md). After deploy, add the entry to the CHANGELOG and tell the team in [channel].

## 10. After the Release

* [ ] Watch dashboards for 30 minutes, then check again after 24 hours
* [ ] Close the release ticket and the issues it contains
* [ ] Note what went wrong or slowly, and fix this file
* [ ] Archive the release candidate branch
