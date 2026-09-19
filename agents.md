# Agent guidance for the Systemone Hugo theme

## What this repository is

A Hugo theme module implementing the "INK / PAPER" editorial-neubrutalism
design system documented in full at `docs/DESIGN-SYSTEM.md`. That document is
the source of truth for every color, size, weight, tracking, leading, radius,
border and shadow in the theme. Read it before changing CSS or templates.

## Non-negotiable constraints

- **Hand-written plain CSS only.** No Sass, PostCSS, Tailwind, or Node build
  step. Hugo Pipes (`resources.Concat`, `resources.Minify`,
  `resources.Fingerprint`) are the only build tooling, and Hugo is already
  running them — do not add a `package.json` build script that is required to
  view the site.
- **Zero runtime dependencies.** No JS framework, no webfonts, no icon fonts,
  no analytics or search dependency baked into the theme.
- **`--radius: 0px` everywhere, no authored exception.** Buttons, inputs,
  checkboxes, images, code, tags, menus, focus rings, avatars — all square.
- **Shadows are hard-offset with zero blur** (`2px 2px 0 0` or
  `3px 3px 0 0`), never a soft/glow shadow.
- **`assets/css/tokens.css` is the only file that defines baseline design
  values.** Component/base CSS files consume `var(--token)`, they don't
  reintroduce near-identical literal colors or spacing.
- **No JavaScript in Stage 1.** Later stages add a small progressive-enhancement
  script for code Copy buttons only — see `docs/DESIGN-SYSTEM.md` §7.
- Stylesheet concatenation order (§7 of the spec) matters: reset → tokens →
  base typography/layout → components → prose/syntax → accessibility/print →
  generated parameter overrides → optional user `assets/css/custom.css`.

## Project structure

- `assets/css/` — hand-written CSS, assembled by `layouts/partials/head.html`
  via Hugo Pipes.
- `layouts/` — base templates and partials.
- `exampleSite/` — a working demo site (own `hugo.toml`, `content/`,
  `config/_default/params.toml`) used to build/serve/screenshot the theme.
- `docs/DESIGN-SYSTEM.md` — the full design spec. Do not invent values that
  are already specified there.

## Testing changes

```bash
# from the theme root
hugo --source exampleSite --themesDir ../.. --minify --gc   # build
hugo server --source exampleSite --themesDir ../..          # serve
```

After any CSS change, re-check the build-verification checklist in
`docs/DESIGN-SYSTEM.md` §8: radius/shadow/font/gradient geometry audit, the
24 KiB uncompressed / 7 KiB gzip CSS budget, and the light/dark contrast
pairs.

## What NOT to do

- Do not relax or delete a spec rule to make a check pass; say so in your
  report instead.
- Do not add a webfont, icon font, or `@font-face`.
- Do not add a dependency required to build or view the site.
- Do not introduce rounded corners, soft shadows, gradients, or backdrop
  blur anywhere in theme-owned CSS.
