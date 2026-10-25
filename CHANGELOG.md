# Changelog

User-facing changes are recorded here. Dates use YYYY-MM-DD. Versions before 1.0 may change public contracts; release notes describe compatibility and installation requirements.

## [Unreleased]

### Added

- EditorConfig settings aligned with Biome and Git's LF line endings.
- This changelog, with the initial release history and links to release assets.
- Issue-routing links for documentation and private vulnerability reporting guidance.

### Changed

- Contribution, conduct, security and pull-request guidance for public contributors.
- CI job names, a 20-minute job timeout, and checkout without persisted credentials.
- Installation documentation now includes the prebuilt GitHub release archive.
- Package archives include the changelog, contribution guidelines, code of conduct and security policy.

## [0.1.0] - 2026-10-23

Initial alpha release. Requires Node.js 24.12 or later; distributed as a compiled npm archive through GitHub Releases.

### Added

- Local SQLite usage ledger, CLI summaries, CSV/JSON exports and a loopback dashboard.
- Adapters for Claude Code, Codex, Gemini CLI, Cursor CSV, OpenCode exports, Cline task journals and normalized JSONL.
- Configurable token-based energy scenarios, optional supplied GPU telemetry, Wh-to-kcal conversion and eight food-energy comparisons.
- Claude Code status line, local stdio MCP, and host command/skill templates.
- English, Russian, Spanish, German, French, Japanese and Brazilian Portuguese for the dashboard and compact summaries; system, light and dark themes.
- Documentation, original SVG assets, high-resolution demo screenshots, grouped monthly dependency updates and CI for Linux, macOS and Windows.

### Fixed

- Concurrent source imports could replace newer counters with an older snapshot.
- A dangling discovered link could prevent valid files from importing.
- Dashboard exports could use previous filters while a new report was loading.
- Windows checkout line endings could fail Biome checks.

Energy values are illustrative scenarios rather than measured consumption. Source-format and accounting limitations are described in the [adapter guide](docs/adapters.md) and [methodology](docs/methodology.md).

[Unreleased]: https://github.com/0then0/AgentKcal/compare/v0.1.0...main
[0.1.0]: https://github.com/0then0/AgentKcal/releases/tag/v0.1.0
