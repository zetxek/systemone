# Systemone

**Editorial neubrutalism for Hugo.** Oversized, tightly tracked Arial-family
display type, monospace utility text, square geometry, thin 1px ink rules,
hard zero-blur offset shadows, warm paper and near-black ink, with acid lime
and pink as the only two expressive accents.

Hand-written plain CSS. No Sass, PostCSS, Tailwind, or Node build step. No
webfonts, no icon fonts, no JavaScript required to read the site. Full design
rationale and token reference: [`docs/DESIGN-SYSTEM.md`](docs/DESIGN-SYSTEM.md).

## Install

Add the module to your site's `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/zetxek/systemone"
```

Or as a Git submodule under `themes/systemone`, then set `theme = "systemone"`.

No `npm install` is required — the theme ships zero runtime dependencies and
no build step. See `exampleSite/` for a working demo site.

```bash
# run the bundled example site
hugo server --source exampleSite --themesDir ../..
```

## Params API

Configure these under `[params]` (see `exampleSite/config/_default/params.toml`
for a complete example):

| Parameter | Default | Allowed values / purpose |
|---|---|---|
| `design.appearance` | `auto` | `auto`, `light`, `dark` |
| `design.prose` | `sans` | `sans`, `mono` |
| `design.ornaments` | `true` | Home-only decorative devices |
| `design.lime` | `#d4ff3f` | Optional accent override |
| `design.pink` | `#ee5ba6` | Optional accent override |
| `design.containerMax` | `1160px` | Advanced layout override |
| `features.copyCode` | `true` | Progressive enhancement (later stage) |
| `features.postTOC` | `true` | Still subject to heading-count threshold |
| `features.appearanceToggle` | `true` | Reader-facing header control that cycles auto → light → dark, persisted in `localStorage`. Progressive enhancement: absent (not a dead button) with JavaScript disabled. |

Arbitrary accent overrides (`design.lime` / `design.pink`) sit outside the
spec's certified default contrast contract until independently rechecked —
see `docs/DESIGN-SYSTEM.md` §7.

## Status

This is **Stage 1**: repository skeleton, tokens, base CSS, and minimal
working templates (home/single/list/404). Components documented in the spec
(post cards, TOC, code/terminal blocks, admonitions, tables, forms,
shortcodes, image pipeline, copy-button JS, edge ornaments) are not yet
implemented — see `CHANGELOG.md`.

## License

MIT, see [`LICENSE`](LICENSE).
