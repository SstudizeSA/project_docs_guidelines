# Changelog

All notable changes to this project are recorded here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versions follow [Semantic Versioning](https://semver.org/).

## How Versions Work

| Version change | Example | When to use it |
|---|---|---|
| PATCH | 2.4.0 to 2.4.1 | Bug fix. No behavior change for users. |
| MINOR | 2.4.1 to 2.5.0 | New feature that does not break existing use. |
| MAJOR | 2.5.0 to 3.0.0 | Change that breaks old behavior, such as a removed endpoint. |

## Rules for Writing Entries

1. Add an entry in the same pull request as the code change.
2. Write for the reader, not the author. Say what changed for the user, not which file you edited.
3. Start each line with a verb: "Add", "Fix", "Remove".
4. Link the issue or pull request number at the end of the line.
5. Use only these categories: **Added**, **Changed**, **Deprecated**, **Removed**, **Fixed**, **Security**.
6. Add a **Testing notes** line to each release so testers know what to verify.
7. Dates use the format YYYY-MM-DD.

## [Unreleased]

### Added
* [Describe new feature] ([#123])

### Changed
* [Describe changed behavior] ([#124])

### Deprecated
* [Describe what will be removed, and in which version] ([#125])

### Removed
* [Describe what was removed] ([#126])

### Fixed
* [Describe the bug that was fixed] ([#127])

### Security
* [Describe the security fix. Do not reveal details before users can patch] ([#128])

## [1.1.0] (2026-01-15)

### Added
* [Example: Add CSV export to the reports page] ([#201])

### Fixed
* [Example: Fix wrong total when an order has 0 items] ([#205])

### Testing notes
* Verify CSV export with 0 rows, 1 row, and 10,000 rows.
* Re run the order total regression checks.
* Needs a database migration: [yes or no]. Needs new environment variables: [yes or no].

## [1.0.0] (2025-12-01)

### Added
* Initial production release.

### Testing notes
* Full regression pass. See [docs/TESTING.md](docs/TESTING.md).

[Unreleased]: https://github.com/[org]/[repo]/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/[org]/[repo]/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/[org]/[repo]/releases/tag/v1.0.0
