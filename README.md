# Systemone

**Editorial neubrutalism for Hugo.** Oversized, tightly tracked display type,
monospace utility text, square geometry, thin ink rules, hard zero-blur offset
shadows, warm paper and near-black ink — with acid lime and pink as the only two
expressive accents.

Hand-written plain CSS. No Sass, PostCSS, Tailwind, or Node build step. No
webfonts, no icon fonts, no JavaScript required to read the site.

![Systemone — light appearance](https://raw.githubusercontent.com/zetxek/systemone/main/images/screenshot.png)

![Systemone — an article, light appearance](https://raw.githubusercontent.com/zetxek/systemone/main/images/post-light.png)

- **Demo:** [systemone-demo.vercel.app](https://systemone-demo.vercel.app)
- **Design system:** [`docs/DESIGN-SYSTEM.md`](docs/DESIGN-SYSTEM.md) — the full
  rationale and token reference. It is the source of truth for every colour,
  size, weight, tracking, leading, radius, border and shadow in the theme.

## Install

As a Hugo module — add to your site's `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/zetxek/systemone"
```

Or as a Git submodule under `themes/systemone`, then set `theme = "systemone"`.

No `npm install` is required — the theme ships zero runtime dependencies and no
build step. `exampleSite/` is a working demo site:

```bash
hugo server --source exampleSite --themesDir ../..
```

## Appearance

The theme ships a full dark appearance — an "ink paper" inversion of the
material relationship, not a dimmed light mode. Every text pair is verified
against WCAG AA in both appearances.

![Systemone — dark appearance](https://raw.githubusercontent.com/zetxek/systemone/main/images/home-dark.png)

Three ways to control it:

1. **The reader's control.** A button in the header cycles `auto → light → dark`
   and persists the choice in `localStorage`. Turn it off with
   `features.appearanceToggle = false`.
2. **Follow the operating system.** The default. Under `auto`, the theme
   responds to `prefers-color-scheme`.
3. **Pin it site-wide.** Set `design.appearance` to `light` or `dark` and the
   theme will ignore the OS.

The control is a progressive enhancement: with JavaScript disabled the button is
absent rather than dead, the site follows the OS, and everything stays fully
readable. There is no flash of the wrong appearance on load.

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
| `features.appearanceToggle` | `true` | Reader-facing header control that cycles auto → light → dark, persisted in `localStorage`. Progressive enhancement: absent (not a dead button) with JavaScript disabled. |
| `features.copyCode` | `true` | Progressive enhancement (later stage) |
| `features.postTOC` | `true` | Still subject to heading-count threshold |

Arbitrary accent overrides (`design.lime` / `design.pink`) sit outside the
spec's certified default contrast contract until independently rechecked — see
`docs/DESIGN-SYSTEM.md` §7.

## Inspiration

Systemone's visual language was developed by studying two sites and abstracting
their shared grammar, then writing an independent design system from it:

- **[typesafe.ai](https://typesafe.ai)** — home of TypeSafe AI's **Jev** /
  **System One** decision model.
- **[openjev.com](https://openjev.com)** — OpenJev, an independent browser
  experiment in the same spirit. It is a community project, explicitly not
  affiliated with TypeSafe AI.

The name is a nod to **System One** — the fast, associative half of Kahneman's
*Thinking, Fast and Slow*.

What was taken is the *look*: oversized tightly tracked display type, monospace
utility text, square geometry, thin ink rules, hard zero-blur shadows, warm
paper, and a small number of controlled accent colours. Both reference sites
were fingerprinted for measurable properties — border radius, border and shadow
geometry, type metrics, palette — and the resulting design system was authored
from scratch. No code, CSS, copy, imagery or other assets were copied from
either site.

**Systemone is not affiliated with, endorsed by, or connected to TypeSafe AI or
the OpenJev project.** It is an independent theme whose design ideas were
inspired by their public websites.

## Status

**Stage 2.** Working: repository skeleton, the full token set, base CSS,
templates for home / single / list / 404 / taxonomy / term, RSS, the light-dark
appearance system, and its reader-facing toggle.

Still to come, per `docs/DESIGN-SYSTEM.md`: post cards, table of contents,
code/terminal component, admonitions, tables, forms, shortcodes, markdown
render hooks, the image pipeline, the copy-button enhancement, and edge
ornaments. See [`CHANGELOG.md`](CHANGELOG.md).

## License

MIT, see [`LICENSE`](LICENSE).
