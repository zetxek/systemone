# Changelog

All notable changes to this theme are documented in this file.

## [0.1.0] — Stage 1 — Unreleased

Initial skeleton, per `docs/DESIGN-SYSTEM.md`.

### Added

- Repository skeleton (`theme.toml`, `hugo.toml`, `go.mod`, `LICENSE`, `exampleSite`).
- `assets/css/tokens.css`: canonical light token sheet plus dark "ink paper" overrides.
- Base stylesheets: reset, typography/layout, accessibility/print rules.
- Base templates: `baseof`, `home`, `single`, `list`, `404`, and the shared head/header/nav/footer partials.
- Generated parameter-override stylesheet wiring `design.appearance`, `design.lime`, `design.pink`, `design.containerMax`.

### Not yet implemented (later stages)

Post cards, truth strip, table of contents rendering, pagination, footnotes styling, code/terminal component, admonitions, tables, forms, taxonomies, shortcodes, markdown render hooks, image pipeline, copy-button JS, edge ornaments.
