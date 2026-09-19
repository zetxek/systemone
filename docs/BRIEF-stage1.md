You are implementing STAGE 1 of a new Hugo theme. Work ONLY in /home/zetxek/git/systemone (already created and git-initialised, with the spec in place).

## THE SPEC IS THE SOURCE OF TRUTH

`/home/zetxek/git/systemone/docs/DESIGN-SYSTEM.md` — 1402 lines. **Read it first, in full.** It is precise and complete. Do not invent values: every colour, size, weight, tracking, leading, radius, border and shadow you need is specified there. Where the spec gives an exact value, use that exact value.

The theme's design direction is "editorial neubrutalism": oversized tightly-tracked Arial-family display type, monospace utility text, square geometry (radius 0 everywhere, no exceptions), thin 1px ink rules, hard zero-blur offset shadows, warm paper + near-black ink, with acid lime `#d4ff3f` and pink `#ee5ba6` as the only two expressive accents, plus restrained retro-computing details.

**STAGE 1 SCOPE — build only this, and make it genuinely work:**

1. **Repository skeleton** mirroring the conventions of the author's existing theme at `/home/zetxek/git/adritian-free-hugo-theme` (read its `theme.toml`, `package.json`, `hugo.toml`, and `exampleSite` layout to match conventions):
   - `theme.toml` (name `Systemone`, MIT licence, description, homepage, demosite placeholder, `min_version`, `tags`, `features`, `[author]` = Adrián Moreno Peña)
   - `hugo.toml` with `[module.hugoVersion]` and the base mounts pattern
   - `LICENSE` (MIT), `README.md` (concise: what it is, install, the params API), `agents.md` (agent guidance for the repo), `CHANGELOG.md` stub
   - `package.json` — **no build step and no runtime dependencies.** Only optional dev/test scripts. The spec forbids a Node/Sass/PostCSS build; the theme must be usable with zero install.
   - `exampleSite/` — a working demo site with `hugo.toml`, a couple of markdown posts (one code-heavy, one with headings for TOC), and a standalone page, plus the site params that exercise the params API.

2. **`assets/css/tokens.css`** — the canonical token sheet, transcribed EXACTLY from section 2 of the spec (the full `:root` block), plus the dark "ink paper" overrides from section 3 exactly as tabulated. Respect the spec's own rule: **do not fix the root font size** (all sizing in rem so user font preferences win).

3. **Base CSS** (separate files, in the spec's stylesheet order from section 7):
   - a minimal reset
   - base typography + layout (container `min(1160px, calc(100% - 32px))`, the 4/6/12-column responsive rules and breakpoints from section 2)
   - Implement the full type scale and the type-role assignments table from section 2.
   - Include the `prefers-color-scheme` handling, `forced-colors`, print rules, and `prefers-reduced-motion` per section 3. Default motion is **zero**.
   - Include the tokenized two-band focus ring (`0 0 0 2px paper, 0 0 0 4px ink` — zero blur).

4. **Minimal but real layouts** so the example site renders end to end:
   - `layouts/_default/baseof.html`, `home.html`, `single.html`, `list.html`, `404.html`
   - partials: document head (incl. `color-scheme`, CSS assembled via Hugo Pipes `resources.Concat` + `minify` + `fingerprint`), skip link, header/masthead, primary navigation, footer
   - No icon font. If you need icons, inline SVG only.
   - **No JavaScript at all in Stage 1.** The spec ships JS only for optional copy buttons; leave that for a later stage.

5. **A generated parameter-override stylesheet.** Implement the small params API from section 7 (`design.appearance`, `design.prose`, `design.ornaments`, `design.lime`, `design.pink`, `design.containerMax`, `features.copyCode`, `features.postTOC`) by generating a small CSS file from validated params and appending it LAST in the concatenation order. Stage 1 only needs to actually wire `design.appearance`, `design.lime`, `design.pink`, `design.containerMax`; the rest can be read and passed through for later stages.

**OUT OF SCOPE for Stage 1** (do NOT build these yet): post cards, truth strip, table of contents, pagination, footnotes styling, code/terminal component, admonition/GUI callout, tables, forms, taxonomies, shortcodes, markdown render hooks, image pipeline, copy-button JS, edge ornaments. Just leave the CSS/layout structure ready for them.

## VERIFY BEFORE REPORTING (required — this is the deliverable, not the file count)

1. **Build the example site clean:**
   `cd /home/zetxek/git/systemone && hugo --source exampleSite --themesDir ../.. --minify --gc 2>&1 | tail -20` — expect **0 ERROR** lines and a successful build. Report the exact command and output summary. Note: the theme dir is the module itself, so adjust `--themesDir`/module config as needed to make it build; if you must use a different invocation, document it.
2. **Geometry audit — assert from the BUILT CSS, not the source.** Grep the emitted stylesheet and prove:
   - no `border-radius` other than `0` / `0px` (report any exception explicitly)
   - every `box-shadow` has a **zero blur radius** (i.e. matches `2px 2px 0 0` or `3px 3px 0 0`, never a third length that is non-zero)
   - no `@font-face`, no `url(` referencing a font, no `woff`/`ttf`/`otf`
   - no `linear-gradient` / `radial-gradient` / `backdrop-filter`
3. **Size budget** from the spec's checklist C: main CSS **≤ 24 KiB uncompressed and ≤ 7 KiB gzip**; JS ≤ 4 KiB (there is none in Stage 1). Report the actual byte counts of the final emitted CSS (uncompressed and gzip).
4. **Contrast spot-check** — the spec's ratios are already verified correct (I re-derived all 22 independently, zero mismatches), so do NOT re-derive them. Instead confirm the emitted CSS contains the specified hex values verbatim for `--paper`, `--ink`, `--lime`, `--pink`, `--link` in both appearances.
5. **Serve it and confirm it renders:** start `hugo server --source exampleSite` on a free port, `curl -s` the home page and one post, and confirm both return HTTP 200 with real markup (not an error page). Screenshot the home page with Playwright to `/tmp/systemone-home.png` and view it — it should already read as "big tight display type on warm paper with 1px ink rules", even without the later components.

## HARD RULES

- **Do NOT run any git command beyond what exists** — no commit, no push, no checkout/reset/stash. I will handle git.
- Do NOT create a GitHub repository or any remote.
- Do NOT modify anything outside `/home/zetxek/git/systemone`.
- Do NOT add dependencies to `package.json` that are required to build or view the site.
- Do not delete or water down any rule from the spec to make a check pass. If a spec rule cannot be met, say so explicitly in your report rather than silently relaxing it.
- Never leave stray background servers running when you finish.

## FINAL REPORT

(a) Every file created, one line each.
(b) The exact build command and its output (0 errors proof).
(c) The geometry audit results — radius, shadow blur, fonts, gradients — with the actual grep output.
(d) CSS byte counts (uncompressed + gzip) against the budget.
(e) Confirmation the home page and a post return 200, plus what `/tmp/systemone-home.png` shows.
(f) Anything in the spec you could not satisfy, and why.
