# Task: appearance toggle + Hugo Themes Showcase compliance

You are working in the `systemone` Hugo theme repo at `~/git/systemone`
(branch `main`, clean). Read `agents.md` and `docs/DESIGN-SYSTEM.md` FIRST —
the design system is the source of truth and its constraints are binding.

## Part 1 — user-facing light/dark appearance toggle

**Current state.** Dark mode already works: `assets/css/tokens.css` defines an
"ink paper" inversion under `@media (prefers-color-scheme: dark)` (guarded by
`:root:not([data-appearance="light"])`), plus explicit `[data-appearance="dark"]`
/ `[data-appearance="light"]` pinning. A site author can pin the appearance
server-side via the `design.appearance` param (`auto|light|dark`), which the
theme already honours by emitting `data-appearance` on the root element.

**What's missing** is a control so a *reader* can change it at runtime.

**Build this:**

1. A single square `<button>` in the header, placed after the nav and before
   the RSS link (`layouts/partials/header.html`).
2. It **cycles** `auto → light → dark → auto`. Visible label is the current
   mode as plain text (`AUTO` / `LIGHT` / `DARK`) — mono, uppercase, tracked,
   matching the site's utility-text idiom. Do NOT use an icon font or an SVG
   sun/moon; a text label is correct for this design language and the theme
   forbids icon fonts.
3. Choosing `auto` must **remove** the `data-appearance` attribute entirely so
   `prefers-color-scheme` governs again (do not set `data-appearance="auto"`).
4. Persist the choice in `localStorage` under key `systemone-appearance`.
5. **No flash of wrong appearance**: a tiny inline script in `<head>` (before
   any stylesheet-dependent paint) must read the stored value and apply it. It
   must also un-hide the button, so that with JavaScript disabled the control
   is simply absent rather than a dead button. Render the button with the
   `hidden` attribute and let that inline script reveal it.
6. Accessibility: real `<button type="button">`; accessible name conveying both
   state and action (e.g. "Appearance: auto. Activate to change."); keyboard
   operable; uses the existing focus-ring token; no motion (the system is
   motion-zero). The visible label alone is not a sufficient accessible name.
7. Style the control with `var(--token)` values only, `--radius: 0px`, zero-blur
   shadows, 1px `var(--line)` border. Its active/current state should be
   visually distinct (lime fill with `var(--accent-ink)` text is idiomatic).
   Do not add new literal colors.
8. Consider `color-scheme` on the root so form controls and scrollbars match
   the active appearance; check the spec before adding, and keep the pinned
   cases consistent.

Gate it behind a param `features.appearanceToggle` (default `true`) and document
it in the params tables in `README.md` and `exampleSite/config/_default/params.toml`.

**Script constraints (non-negotiable):** plain hand-written JS, no framework, no
npm/Node build step, no dependency. Total added JS ≤ ~1 KB unminified. It must
be a progressive enhancement — the site must remain fully readable and correct
with JavaScript disabled, and the inline head script must never throw if
`localStorage` is unavailable (Safari private mode etc. — guard it).

## Part 2 — Hugo Themes Showcase compliance

We are submitting this theme to the official directory
(themes.gohugo.io). Their requirements, and where we stand:

1. **`exampleSite` baseURL must be `https://example.com/`.**
   REQUIRED by their guidelines ("to avoid the abuse of unused domains").
   I recently changed it to `https://systemone-beta.vercel.app/` — change it
   BACK to `https://example.com/`. This does NOT break our Vercel deploy,
   because `vercel.json` overrides the base URL at build time with `-b`.
   Verify that claim: run the build with and without `-b` and show both base
   URLs in the output.
2. **`images/screenshot.png` (exactly 1500×1000) and `images/tn.png` (exactly
   900×600)** must exist. I will produce these; just create the `images/`
   directory with a short `images/README.md` saying what belongs there and the
   required dimensions. Do not invent or commit placeholder images.
3. **No page may lack a layout.** Their build logs are polluted by missing
   layouts. Audit for every page kind the theme emits (home, single, list,
   section, taxonomy, term, 404, RSS) and make sure each resolves. If a kind is
   intentionally unsupported, declare it with `disableKinds` rather than
   leaving it layout-less. Show me the evidence.
4. **No deprecated Hugo features / no console warnings.** Run the build and
   show that it emits zero warnings.
5. **Must work with the plain (non-extended) Hugo and with the content from
   `gohugoio/hugoBasicExample`** — the showcase builds our demo against THAT
   content repo, not our exampleSite. Clone it to a temp dir and build our
   theme against its `content/`. Report anything that breaks; if the theme
   requires something our own exampleSite supplies (e.g. specific params), make
   the theme degrade gracefully with sensible defaults instead.
6. **`theme.toml` completeness.** It already has name/license/licenselink/
   description/homepage/tags/features/min_version/[author]. Double-check the
   required field set and `min_version` as a full semver.

## Verification you must run and report

- `hugo --gc --minify` from `exampleSite` — zero errors, zero warnings.
- The CSS budget re-check: ≤24 KiB uncompressed and ≤7 KiB gzip (do not regress
  it; the toggle will add some CSS).
- The geometry audit from `docs/DESIGN-SYSTEM.md` §8: `--radius: 0px` with no
  literal non-zero radius; every shadow zero-blur; no `@font-face`, no font
  `url()`, no gradients, no `backdrop-filter`.
- The light AND dark contrast pairs for any new text/background combination you
  introduce (the toggle's own label states included). Report the computed
  ratios and confirm WCAG AA.
- Drive the toggle in a headless browser: click through all three states,
  reload and confirm persistence, and confirm `prefers-color-scheme` still wins
  when the stored value is `auto`. Report the observed `data-appearance` and
  computed body colors at each step.
- Confirm the site still renders and reads correctly with JavaScript disabled.

## Rules

- Do NOT relax or delete a spec rule to make a check pass. If something can't
  be satisfied, say so in your report instead of silently changing the spec.
- Do NOT commit any image binaries.
- Do NOT touch `vercel.json`.
- Do NOT add a build step, webfont, icon font, or runtime dependency.
- Keep the diff focused: the toggle, the compliance fixes, and their docs.
- Commit nothing — leave the work in the working tree and report the diffstat.
