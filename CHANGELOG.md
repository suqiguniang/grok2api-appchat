# Changelog

All notable changes to this project will be documented in this file.

## [0.2.1] - 2026-03-24

### Added

- Added a sanitized public release layout for GitHub publishing.
- Added `.gitignore` rules to avoid leaking runtime config and token files.
- Added `NOTICE.md` for upstream attribution.
- Added this `CHANGELOG.md`.
- Added `CONTRIBUTING.md`.

### Changed

- Renamed the public package to `grok2api-appchat`.
- Renamed Docker image/container defaults to `grok2api-appchat`.
- Reworked the README for public distribution.
- Replaced UI branding with neutral public-build branding.
- Changed default admin password placeholder from `grok2api` to `change-me`.

### Security

- Removed deployment-specific project branding and repository links.
- Verified that no private domain, token, proxy, server IP, or API key remained in the public source tree.

## [0.2.0]

- Imported from a running Rust-based Grok gateway codebase snapshot for further cleanup and public packaging.
