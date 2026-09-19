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

## [Unreleased] — Stage 2

### Added

- Reader-facing appearance toggle in the header: cycles auto → light → dark, persists to `localStorage`, no flash of the wrong appearance, hidden entirely (not a dead button) with JavaScript disabled. Gated behind `features.appearanceToggle` (default `true`).

### Changed

- `exampleSite`'s `baseURL` reverted to `https://example.com/` per Hugo Themes Showcase guidelines; the Vercel deploy still gets its real URL via `vercel.json`'s build-time `-b` override.

### Fixed

- Hugo Themes Showcase compliance audit: confirmed every page kind (home, single, list/section, taxonomy, term, 404, RSS) resolves to a template, with zero build warnings; theme builds cleanly with plain (non-extended) Hugo and degrades gracefully when built against content that supplies none of the theme's optional params (verified against `gohugoio/hugoBasicExample`).
