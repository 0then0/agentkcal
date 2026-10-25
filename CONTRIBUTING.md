# Contributing to AgentKcal

Contributions can improve agent-format support, accounting correctness, translations, usability and estimation methodology. For changes to the event contract, data model, runtime dependencies or default energy assumptions, open an issue to discuss the proposed behavior first.

## Set up a development environment

Use Node.js 24.12+ and npm:

```sh
git clone https://github.com/0then0/AgentKcal.git
cd AgentKcal
npm ci
npm run build
npm run demo
```

The demo uses temporary synthetic data. For other experiments, select a disposable `--data-dir`; automated tests must not read personal agent logs.

## Project structure

- `src/adapters/`: source discovery and normalization into disjoint token buckets.
- `src/providers/`: energy estimation from normalized usage.
- `src/storage.ts`: SQLite persistence and record identity.
- `src/service.ts`: imports, aggregation, filters and exports.
- `src/integrations/`: compact summaries, host configuration and stdio MCP.
- `src/web/`: dashboard, translations, styles and original SVG assets.
- `integrations/`: distributable skills and command templates.
- `tests/`: Node test-runner tests and synthetic fixtures.
- `scripts/`: asset packaging and installed-package checks.
- `docs/`: user guides and technical references.

CLI, HTTP and MCP share accounting logic. Keep adapters independent of energy coefficients and providers independent of agent file formats. Prefer built-in APIs and existing modules before adding dependencies. [Adapter and provider extension guide](docs/extending.md).

## Checks

```sh
npm run check
npm run typecheck
npm test
npm run test:package
```

`check` runs Biome for linting, formatting and import organization. `typecheck` checks server code, browser code and tests. `test` builds dashboard assets and runs the TypeScript suite using Node's test runner. `test:package` packs the application, installs it without development dependencies in a temporary directory, and exercises its CLI, MCP and dashboard.

The root `.editorconfig` defines UTF-8, two-space indentation, a final newline and LF line endings. `.gitattributes` enforces LF in Git checkouts on every platform. Enable EditorConfig support in your editor; Biome remains the formatter and lint authority. Markdown trailing spaces are preserved because they can represent hard line breaks.

Run `npm run format` to apply formatting and safe lint fixes. Integration Markdown templates are kept verbatim to preserve their YAML front matter. CSS rules allow component-specific cascade ordering and documented accessibility exceptions.

CI runs the same checks on Linux, macOS and Windows, including the minimum supported Node.js version on Linux. Dependabot groups dependency updates monthly; review major upgrades separately.

## Tests and fixtures

Add regression tests for behavior that can change totals or data boundaries: bucket semantics, stable identities, streaming snapshots, cumulative counters, malformed files, rollback and privacy. Fixture records must be synthetic or fully redacted. Do not submit prompts, model responses, tool arguments, credentials, account IDs or identifying filesystem paths.

A source-format change should cite its schema or upstream implementation and explain whether cache and reasoning counters overlap other buckets. Verify repeat imports and updates, not just the first import.

For dashboard changes, inspect a populated view and an empty/error state at narrow and wide widths. Check keyboard access, both color themes and long translated labels. Preserve the distinction between estimated energy and measured usage.

## Translations

When adding a dashboard locale, update `src/web/browser.d.ts`, `preferences.ts`, `locales.ts`, food-unit forms and the language selector. Each catalog must cover every source message and preserve interpolation placeholders. Use `Intl` formatting and plural rules for numbers, dates and portion labels.

Compact CLI/MCP translations live in `src/integrations/languages.ts`. Keep their language codes aligned with the dashboard. Test browser-language detection, saved preferences and representative long labels. Screenshots in the READMEs should use the isolated demo; never capture personal logs.

## Pull requests

Explain the problem, the resulting behavior and relevant limitations. List the checks you ran and their outcomes. Update user-facing documentation when commands, source formats or configuration change. Add a concise entry under `Unreleased` in [CHANGELOG.md](CHANGELOG.md) for user-visible changes. Describe the effect on users rather than implementation steps.

The [pull-request template](https://github.com/0then0/AgentKcal/blob/main/.github/PULL_REQUEST_TEMPLATE.md) lists relevant validation and compatibility details. A missing check should have a reason, not a fabricated passing result.

Use Conventional Commits in English: `feat`, `fix`, `refactor`, `chore`, `docs` or `test`, for example `fix(adapters): deduplicate repeated usage snapshots`.

## Releases

Published versions and dates are listed in [CHANGELOG.md](CHANGELOG.md). Maintainers release a specific commit after its CI passes. Before publishing, ensure the package version, CLI version, installation examples and changelog agree; run the checks above, build with `npm pack`, and verify the installed archive. Attach the compiled archive and its SHA-256 checksum to a GitHub Release. Mark alpha releases as prereleases.

Do not move an existing release tag or replace an archive with different contents. Publish a new version for subsequent fixes. A GitHub Release does not imply publication to the npm registry.

## License and project assets

Contributions are distributed under [Apache-2.0](LICENSE). Keep attribution for third-party material. The project icon and food illustrations are original SVG assets; agent names remain the property of their respective owners.

Follow the [code of conduct](CODE_OF_CONDUCT.md). Report security issues through the [security policy](SECURITY.md).
