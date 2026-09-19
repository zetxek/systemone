# Theme specification: **INK / PAPER**

**Direction:** editorial neubrutalism, with restrained retro-computing details.

This is a design specification, not an implementation. The CSS declarations below are the requested token data; component styling, templates, and scripts are deliberately not written yet. Unless marked optional, every decision is the theme’s default.

**One factual correction:** openjev’s text is system-font-only; the measured TypeSafe font mix includes several non-system faces. System-only typography is therefore our deliberate synthesis, not a shared property of both references. Also, requesting Arial at `900` does not guarantee an actual black-weight font file: browsers commonly resolve it to the installed Arial Bold.

---

# 1. Style definition

## Client-ready description

> “The theme uses **editorial neubrutalism**: oversized, tightly tracked sans-serif headlines, monospace utility text, square geometry, thin ink rules, and occasional hard-offset shadows on warm paper. Retro-computing details—terminal panels, default-blue links, and a restrained desktop-dialog callout—add a lo-fi web attitude without compromising reading.”

Your taxonomy is sound. **Digital brutalism** is the umbrella; **neubrutalism** describes openjev’s component treatment; **retro-computing / lo-fi web with an anti-design attitude** describes TypeSafe’s additional vocabulary. Swiss typography is a useful formal influence, not a claim about either site’s documented historical lineage.

## Nine non-negotiable signatures

1. **Square boxes:** `0px` radius on every authored component and pseudo-element.
2. **Paper and ink:** large, quiet, nearly monochrome surfaces—not a collection of colored cards.
3. **Oversized display typography:** Arial-family, weight `900`, tracking down to `-.07em`.
4. **Monospace infrastructure:** navigation, labels, dates, tags, captions, controls, and code.
5. **Thin structural rules:** predominantly `1px` ink lines; pale lines are secondary separators only.
6. **Hard elevation:** exactly `2px` or `3px` offset shadows, with zero blur.
7. **Block highlights:** acid lime behind ink text, not a decorative underline.
8. **Explicit editorial organization:** visible section identifiers such as `00 / INDEX`, strong alignment, deliberate whitespace.
9. **One controlled retro layer:** terminal code panels and GUI-style admonitions; not an entire simulated operating system.

## What immediately breaks it

- Rounded cards, pill tags, circular avatar crops.
- Soft shadows, ambient glows, glassmorphism, backdrop blur.
- UI gradients, including gradient text and gradient buttons.
- A default `system-ui` interface applied uniformly to headings, body, labels, and controls.
- Uniformly medium-weight, comfortably spaced typography with no display contrast.
- Large pastel surfaces on every component.
- Thick borders everywhere: this direction is primarily **1px editorial structure**, not cartoon neubrutalism.
- Random font switching or casing changes inside real content.
- Animated “hacker” noise, typing effects, fake loading terminals, or inaccessible custom cursors.
- Distressed textures, torn-paper collage, and ransom-note lettering: those would move it toward punk.

Long-form prose **should** have comfortable leading. Readability does not break the style; removing its surrounding typographic and structural character does.

---

# 2. Token sheet

## Palette decision

Keep the reference **acid lime and pink**. They already express the intended relationship: lime is the principal signal, pink is the occasional editorial interruption.

There are **two expressive accent hues**, not five interchangeable brand colors:

- **Lime:** primary action, highlight, selected state; may reinforce an explicitly labeled success state.
- **Pink:** editorial emphasis and secondary interruption; never the sole signal for warning or error.
- **Red:** semantic error/destructive action only.
- **Blue:** functional link color, not a decorative accent.
- **Success:** ink text, a check symbol, and the word “Success”; an optional lime background. No additional green token.
- **Warning:** ink-on-panel with the word “Warning” and an icon. No additional orange token.

**Composition rule:** each section may contain one principal lime-filled device and one marked phrase. Pink is limited to one editorial callout per page. Selected controls and semantic feedback are exempt. Syntax highlighting follows its separate terminal palette.

This is more useful than a vague “use accents sparingly” instruction.

## Canonical tokens

Rem values below assume the browser’s default `16px` base. **Do not fix the root font size**; respect user font-size preferences.

```css
:root {
  /* Core palette: light appearance */
  --paper: #f7f6f0;
  --ink: #171715;
  --panel: #fffefa;
  --line: #c7c5bb;
  --muted: #66645e;

  --lime: #d4ff3f;
  --pink: #ee5ba6;
  --red: #b42318;
  --link: #0000ee;

  /* Foreground for lime/pink fills: invariant across appearances */
  --accent-ink: #171715;

  /* Semantic and interaction roles */
  --error: var(--red);
  --error-on-fill: #f7f6f0;
  --success-bg: var(--lime);
  --success-ink: var(--accent-ink);
  --selection-bg: var(--pink);
  --selection-ink: var(--accent-ink);
  --shadow-ink: #171715;

  /* Terminal palette: invariant across appearances */
  --code-bg: #171715;
  --code-fg: #f7f6f0;
  --code-muted: #b6b3a8;
  --code-key: #d4ff3f;
  --code-string: #ee5ba6;
  --code-number: #8fb3ff;
  --code-error: #ff8a80;
  --code-line-bg: #242420;

  /* Retro-GUI chrome */
  --gui-face: #c7c5bb;
  --gui-highlight: #fffefa;
  --gui-light: #f7f6f0;
  --gui-mid: #66645e;
  --gui-dark: #171715;

  /* System-only font stacks */
  --font-display: Arial, Helvetica, sans-serif;
  --font-prose: Arial, Helvetica, sans-serif;
  --font-mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas,
    "Liberation Mono", monospace;
  --font-serif: "Times New Roman", Times, serif;

  /* Type sizes */
  --text-display-xl: clamp(3rem, calc(1rem + 10vw), 9.375rem);
  --text-display: clamp(2.5rem, calc(1.5rem + 4vw), 5rem);
  --text-h2: clamp(1.75rem, calc(1.25rem + 1.5vw), 2.5rem);
  --text-h3: clamp(1.25rem, calc(1.0625rem + 0.75vw), 1.5rem);
  --text-h4: 1.125rem;
  --text-h5: 1rem;
  --text-h6: 0.875rem;

  --text-body: 1rem;
  --text-prose: 1.125rem;
  --text-prose-mono: 1rem;
  --text-small: 0.875rem;
  --text-meta: 0.8125rem;
  --text-label: 0.75rem;
  --text-code: 0.9375rem;
  --text-inline-code: 0.9em;
  --text-epigraph: 1.375rem;

  /* Weights */
  --weight-body: 400;
  --weight-strong: 700;
  --weight-display: 900;
  --weight-label: 900;

  /* Leading */
  --leading-display-xl: 1.02;
  --leading-display: 1.05;
  --leading-h2: 1.1;
  --leading-h3: 1.2;
  --leading-h4: 1.3;
  --leading-compact: 1.4;
  --leading-body: 1.5;
  --leading-prose: 1.65;
  --leading-prose-mono: 1.75;
  --leading-code: 1.6;
  --leading-label: 1.25;
  --leading-script-display: 1.2;

  /* Tracking */
  --tracking-display-xl: -0.07em;
  --tracking-display: -0.06em;
  --tracking-h2: -0.04em;
  --tracking-h3: -0.025em;
  --tracking-h4: -0.01em;
  --tracking-body: 0em;
  --tracking-label: 0.08em;
  --tracking-control: 0.04em;

  /* Spacing */
  --space-0: 0;
  --space-1: 0.125rem;
  --space-2: 0.25rem;
  --space-3: 0.5rem;
  --space-4: 0.75rem;
  --space-5: 1rem;
  --space-6: 1.5rem;
  --space-7: 2rem;
  --space-8: 3rem;
  --space-9: 4rem;
  --space-10: 6rem;

  /* Layout */
  --container-max: 1160px;
  --page-gutter: 16px;
  --page-width: min(var(--container-max), calc(100% - 32px));
  --grid-columns: 12;
  --grid-gap: 24px;
  --measure-prose: 68ch;
  --measure-deck: 42rem;
  --measure-hero: 18ch;
  --measure-title: 22ch;

  /* Structural lines */
  --border-width: 1px;
  --rule: 1px solid var(--ink);
  --rule-subtle: 1px solid var(--line);
  --rule-terminal: 1px solid var(--code-fg);
  --blockquote-rule-width: 3px;
  --bevel-layer-width: 1px;

  /* Hard shadows only */
  --shadow-hard: 3px 3px 0 0 var(--shadow-ink);
  --shadow-small: 2px 2px 0 0 var(--shadow-ink);
  --shadow-none: none;

  /* Focus: two contrasting, zero-blur bands */
  --focus-band-width: 2px;
  --focus-extent: 4px;
  --focus-ring:
    0 0 0 2px var(--paper),
    0 0 0 4px var(--ink);

  /* Geometry */
  --radius: 0px;
  --control-min-height: 44px;
  --input-min-height: 48px;
  --control-padding-inline: 16px;
  --input-padding-block: 12px;
  --input-padding-inline: 12px;
  --checkbox-size: 20px;
  --icon-size: 16px;
  --icon-size-large: 20px;
  --icon-stroke: 1.5px;
  --avatar-size: 48px;

  /* Component rhythm */
  --card-padding: 24px;
  --code-padding: 24px;
  --section-gap: 64px;
  --prose-block-gap: 24px;
  --mark-padding: 0 0.08em;
  --link-underline-width: 1px;
  --link-underline-hover-width: 2px;
  --link-underline-offset: 0.16em;

  /* Ornament */
  --ornament-edge-offset: 28px;
  --ornament-bracket-size: 24px;

  /* Motion */
  --motion-duration: 0ms;
}
```

## Type assignments

| Role | Font / size | Weight | Leading | Tracking |
|---|---|---:|---:|---:|
| Home display; 404 numeral | Display / display-xl | 900 | 1.02 | −.07em |
| Internal page H1 | Display / display | 900 | 1.05 | −.06em |
| Prose H2 | Display / h2 | 900 | 1.1 | −.04em |
| Prose H3; card/list titles | Display / h3 | 900 | 1.2 | −.025em |
| H4 | Display / h4 | 700 | 1.3 | −.01em |
| H5 | Display / h5 | 700 | 1.4 | 0 |
| H6 | Mono / h6 | 700 | 1.4 | 0 |
| Interface body | Mono / body | 400 | 1.5 | 0 |
| Article prose, default | Prose / prose | 400 | 1.65 | 0 |
| Article prose, mono option | Mono / prose-mono | 400 | 1.75 | 0 |
| Metadata/captions | Mono / meta | 400 | 1.4 | 0 |
| Section labels | Mono / label | 900 | 1.25 | .08em |
| Buttons/nav | Mono / small | 900 | 1.25 | .04em |
| Code blocks | Mono / code | 400 | 1.6 | 0 |
| Optional epigraph | Serif / epigraph, italic | 400 | 1.5 | 0 |

**The serif slot is only for an explicitly authored epigraph.** It is not randomly assigned to words, titles, or cards. Maximum one epigraph per page.

### Casing and language

- Uppercase only theme-owned utility labels and controls, where appropriate to the translation.
- Never automatically capitalize, lowercase, or uppercase titles, taxonomy names, author names, or prose.
- Use the correct document and content language.
- Display text in Arabic, Persian, Urdu, Hebrew, Indic, Southeast Asian, or CJK scripts uses **`0em` tracking and `1.2` leading**.
- Do not insert manual line breaks into content titles.
- Titles use normal word breaking with emergency wrapping for otherwise unbreakable strings; no clipping or line clamping.
- Article prose may use automatic hyphenation when its language is known. Code and identifiers must not be automatically hyphenated.

**Choice:** retain extreme Latin display tracking, but relax the reference’s `.92` leading because a theme must survive accents and multiline titles.

## Layout and responsive rules

Breakpoints are implementation constants, not CSS variables used inside media queries.

| Viewport | Grid | Gap | Section gap | Card/code padding |
|---|---:|---:|---:|---:|
| Below `40rem` / 640px | 4 columns | 16px | 48px | 16px |
| `40rem`–below `60rem` / 640–959px | 6 columns | 16px | 64px | 24px |
| `60rem` / 960px and above | 12 columns | 24px | 64px | 24px |

- Container: `min(1160px, calc(100% - 32px))`, centered.
- Minimum outer gutter: `16px` at every viewport.
- No full-bleed content that creates horizontal page scrolling.
- Default card grid: one column / two columns / three columns at the breakpoints above.
- Internal title measure: `22ch`, additionally constrained by its grid area.
- Hero title measure: `18ch`, constrained by the container.
- Prose measure: `68ch`, constrained by its grid area.
- Grid children must be allowed to shrink below their intrinsic content width.
- Desktop article: main content columns **1–8**, empty column **9**, TOC columns **10–12**.
- Below 960px: one reading column; TOC precedes the article body.

## Borders, shadows, and bevel

- Every normal structural/control border: `1px`.
- Prose blockquote left rule: `3px`.
- Focus bands: `2px` each.
- No `0.5px` rules.
- Shadows appear only on buttons, cards, and retro callouts—not every panel.
- No blur in any shadow, including focus and inset effects.

### Retro-GUI bevel recipe

Outside to inside:

1. `1px` solid ink perimeter.
2. First inset pixel: top/left `--gui-highlight`; bottom/right `--gui-dark`.
3. Second inset pixel: top/left `--gui-light`; bottom/right `--gui-mid`.
4. Remaining chrome face: `--gui-face`.
5. Content surface: `--panel`.
6. External elevation: `--shadow-hard`.

All strips are solid, square, and one pixel wide. No gradients simulate the bevel.

## Radius rule

**Zero everywhere. No authored exception.**

This includes buttons, inputs, checkboxes, images, code, tags, menus, focus rings, and avatars. Intrinsic shapes inside artwork and browser/OS-owned picker windows are not theme box geometry.

---

# 3. Accessibility and appearance

## Contrast contract

Ratios below use the WCAG relative-luminance formula for opaque sRGB colors, rounded to two decimals. “Text” includes normal-size text; do not rely on the large-text exception.

### Light appearance

| Foreground | Background | Ratio | Permitted use |
|---|---|---:|---|
| Ink `#171715` | Paper `#f7f6f0` | **16.58:1** | All text, icons, strong rules |
| Ink | Panel `#fffefa` | **17.79:1** | All text and controls |
| Muted `#66645e` | Paper | **5.46:1** | Metadata and body-size secondary text |
| Muted | Panel | **5.86:1** | Help text, captions |
| Ink | Lime `#d4ff3f` | **15.54:1** | Mark, primary button, selected control |
| Ink | Pink `#ee5ba6` | **5.71:1** | Editorial fill, selection |
| Link `#0000ee` | Paper | **8.68:1** | Underlined content links |
| Link | Panel | **9.31:1** | Underlined content links |
| Red `#b42318` | Paper | **6.07:1** | Error text |
| Red | Panel | **6.51:1** | Error text and boundaries |
| Paper | Red | **6.07:1** | Destructive button label |
| Ink | GUI face `#c7c5bb` | **10.37:1** | GUI chrome text |

**The supplied muted color passes AA for body text. Keep it.** Darkening it would reduce the useful tonal separation without solving an actual contrast failure.

### Prohibited and restricted combinations

| Pair | Ratio | Decision |
|---|---:|---|
| Lime text on paper | **1.07:1** | Prohibited |
| Pink text on paper | **2.90:1** | Prohibited, including large text |
| Line `#c7c5bb` against paper | **1.60:1** | Decorative separators only |
| Paper text on pink | **2.90:1** | Prohibited |

- Lime and pink are **background-only accents on light reading surfaces**.
- Their foreground is always `--accent-ink`, not the appearance-dependent `--ink`.
- Links inside lime or pink highlights use **ink plus underline**, never blue.
- Controls are placed on paper, panel, or terminal surfaces—not arbitrary colored images.
- `--line` must not be the sole visible boundary of an input, button, checkbox, focus indicator, or meaningful diagram shape.

### Terminal palette, in both appearances

| Foreground | Terminal `#171715` | Highlighted line `#242420` |
|---|---:|---:|
| Text `#f7f6f0` | **16.58:1** | **14.39:1** |
| Comment `#b6b3a8` | **8.55:1** | **7.42:1** |
| Lime key/prompt | **15.54:1** | **13.48:1** |
| Pink string | **5.71:1** | **4.96:1** |
| Blue number `#8fb3ff` | **8.60:1** | **7.46:1** |
| Red error `#ff8a80` | **7.86:1** | **6.82:1** |

This terminal context is the explicit exception to the “accent text is prohibited” rule.

## Focus-visible

Use the tokenized **two-band, zero-blur focus ring**:

- Inner band: `2px` paper.
- Outer band: `2px` ink.
- Total outward extent: `4px`.
- Preserve the component’s structural border.
- Retain hard elevation behind the focus treatment; do not let a component shadow replace it.
- Reserve at least `4px` unobstructed space around focusable controls.
- Scroll containers receive `8px` scroll padding so focused children are not cut off.
- On inline links, use the same treatment; do not replace it with a color change alone.
- Focus is present for keyboard interaction and must not be removed when the pointer is used on a control that still requires focus indication.

The two contrasting bands work on paper, terminal panels, and accent fills. No glow is involved.

## Targets and semantics

- Navigation, buttons, chips, pagination, copy controls, and icon buttons: **minimum 44 × 44px**.
- Text inputs and selects: minimum `48px` high.
- Checkbox drawing: `20 × 20px`, within a clickable label row at least `44px` high.
- Ordinary inline prose links use the WCAG inline-text target exception; do not add overlapping invisible hit areas.
- Footnote references receive a `24 × 24px` inline target where layout permits.
- Never make a rule itself the clickable target.
- No nested interactive elements or stretched card links covering tag links.
- Information must not depend on color, hover, decorative icons, or uppercase styling.
- Every icon-only control has an accessible name.
- Use a visible skip link on focus, before the header.

## Motion

**Default motion is zero.**

- No animated background, typing simulation, marquee, orbit, parallax, or hover translation.
- State changes are immediate.
- No smooth scrolling.
- `prefers-reduced-motion: reduce` preserves this behavior and disables any optional author-supplied theme animation.
- Animated content provided by an author must have its own accessible alternative; the theme must not autoplay it.

Hard-shadow state changes are instantaneous, not animated.

## Dark appearance: ship it, as “ink paper”

A paper metaphor should not require readers to accept a bright screen at night. Ship an inversion of the material relationship, **not a generic blue-grey dark dashboard**.

Default behavior: follow `prefers-color-scheme`. A site-level parameter may pin light or dark. The default theme does not need a JavaScript appearance switch.

### Dark token overrides

All unspecified tokens remain unchanged.

| Token | Dark value |
|---|---|
| `--paper` | `#171715` |
| `--ink` | `#f7f6f0` |
| `--panel` | `#242420` |
| `--line` | `#53534b` |
| `--muted` | `#b6b3a8` |
| `--red` | `#ff8a80` |
| `--link` | `#8fb3ff` |
| `--error-on-fill` | `#171715` |
| `--shadow-ink` | `#000000` |
| `--gui-face` | `#242420` |
| `--gui-highlight` | `#b6b3a8` |
| `--gui-light` | `#53534b` |
| `--gui-mid` | `#000000` |
| `--gui-dark` | `#000000` |

Important invariants:

- `--accent-ink` remains `#171715`.
- Lime and pink remain unchanged.
- Terminal colors remain unchanged.
- Focus bands automatically invert through the paper/ink aliases.
- Set the browser’s color-scheme consistently so native controls and scrollbars match.

### Dark contrast

| Foreground | Dark paper | Dark panel |
|---|---:|---:|
| Ink `#f7f6f0` | **16.58:1** | **14.39:1** |
| Muted `#b6b3a8` | **8.55:1** | **7.42:1** |
| Link `#8fb3ff` | **8.60:1** | **7.46:1** |
| Error `#ff8a80` | **7.86:1** | **6.82:1** |

Ink-colored text on dark error fill is **7.86:1**. Dark `--line` is only **2.31:1** against dark paper, so it remains decorative.

Do not invert photographs, diagrams, or screenshots with filters. Support an explicitly supplied dark image variant where needed.

## Forced colors and print

- In forced-colors mode, use system text, surface, link, and highlight colors.
- Keep visible borders and a `2px` system-color focus outline; do not depend on shadows.
- Allow the user agent to replace decorative fills.
- Print uses white paper, black text, no shadows, no ornaments, no navigation controls, and white code panels with black text.
- Printed tables wrap rather than being clipped inside scrolling containers.

---

# 4. Component specifications

## Shared state contract

The following applies to every interactive component unless overridden below.

| State | Required behavior |
|---|---|
| Default | Explicit affordance: underline, square boundary, or placement inside labeled navigation |
| Hover | Content-link underline increases from `1px` to `2px`; no movement |
| Focus-visible | Two-band focus treatment; never hover-only styling |
| Active/pressed | Immediate state change; no translation |
| Visited | Same link color as unvisited; no additional purple palette |
| Current/selected | Lime fill, accent-ink text, and the appropriate semantic state |
| Disabled | Panel fill, muted text, ink boundary, no shadow; no opacity reduction |
| Loading | Preserve control dimensions and focus; visible progress text and announced status |
| Error | Error text plus explicit message; red is reinforcement, not the message itself |

- Noninteractive components do not acquire hover, focus, pressed, or disabled states.
- Do not implement disabled anchors. Render unavailable pagination as text; use native disabled buttons where appropriate.
- For an asynchronous submit operation, preserve focus, block repeat activation, and expose busy state without removing the focused control.
- Links navigate. Buttons perform actions.
- All components must work without pointer hover.

## 4.1 Site header / masthead

**Anatomy**

1. Skip link.
2. Brand link, text or supplied square-format logo.
3. Primary navigation.
4. Optional RSS link.

**Geometry**

- Static—not sticky.
- Container-aligned.
- `16px` vertical padding.
- Brand: mono `16px`, weight `900`, tracking `-.02em`.
- Bottom border: `1px` ink.
- Desktop: brand left, navigation right, gap `24px`.
- Below 640px: brand row followed by wrapping navigation; row gap `8px`.
- Every link has a `44px` minimum hit height.

No decorative status such as “ONLINE” unless it reflects an actual meaningful state.

**Signature:** a printed masthead separated by a single ink rule, not a floating rounded app bar.

## 4.2 Primary navigation

- Semantic labeled navigation containing a list.
- Mono `14px/1.25`, weight `900`, tracking `.04em`.
- Horizontal padding `12px`; minimum height `44px`.
- Default: ink text, transparent surface.
- Hover: panel fill plus underline.
- Current: lime block, accent-ink text, `aria-current="page"`.
- Pressed: pink fill, accent-ink text.
- Focus: shared ring, including on the current item.
- Wrapping is the mobile behavior. **No hamburger menu by default.**

**Signature:** tab-like words on the page, not pills.

## 4.3 Acid `mark`

- Semantic highlight, not a button.
- Lime background; accent-ink foreground.
- Padding `0 .08em`.
- No border, shadow, radius, or text decoration supplied by the mark itself.
- Preserve the full background on each wrapped fragment.
- In a heading, mark at most one authored phrase; do not algorithmically color random words.
- If the highlighted phrase is a link, retain an ink underline.
- Pink is available only through the explicitly editorial highlight variant.

No extra ARIA role is needed. If the highlight conveys meaning beyond emphasis, explain that meaning in text.

**Signature:** the appearance of an acid marker dragged through large type.

## 4.4 Hero

- Eyebrow: `00 / INDEX` or the page-specific translated label.
- Eyebrow-to-title gap: `16px`.
- Title-to-deck gap: `24px`.
- Deck-to-actions gap: `24px`.
- Top and bottom padding: `48px` desktop, `32px` below 640px.
- Home title: display-xl; internal title: display.
- Deck: prose `18px/1.65`, maximum `42rem`.
- Actions wrap with `12px` gaps.
- Maximum two actions: one primary and one secondary.
- No required image and no fixed hero height.
- Optional hero image follows the text, separated by `32px`; it does not sit behind text.

Title text is never clipped to force a poster composition.

**Signature:** display typography is the hero image.

## 4.5 Truth strip

- A wrapping list of short factual site attributes.
- `1px` ink top and bottom rules.
- Mono label style.
- Items: `12px` vertical and `16px` horizontal padding.
- `1px` ink separators between adjacent items on a row.
- Mobile: items may occupy full rows; avoid doubled borders.
- No ticker, marquee, or fake telemetry.

If no attributes are supplied, omit it rather than inventing claims.

**Signature:** information presented like a technical specification strip.

## 4.6 Post list item

**Desktop anatomy**

- Date/index: columns 1–3.
- Title, excerpt, tags: columns 4–11.
- Arrow: column 12, included within the title link’s accessible interaction structure.

Below 640px: metadata, title, excerpt, and tags stack; arrow remains adjacent to the title.

**Geometry and content**

- `24px` vertical padding.
- Bottom `1px` ink rule.
- Metadata `13px`.
- Title uses h3 styling, regardless of the semantic heading level required by the page.
- Excerpt: prose `18px/1.65`, top margin `8px`.
- Tags: top margin `12px`.
- No fixed height or title clamp.
- Only the title/arrow link and tags are interactive; the whole row is not a hidden click target.

Hover changes the actual title link, not the entire row.

**Signature:** an editorial index ruled like a ledger.

## 4.7 Post card

- Panel fill, `1px` ink border, `3px` hard shadow.
- Padding `24px`; `16px` below 640px.
- Content order: optional thumbnail, metadata, title, excerpt, tags.
- Gaps: `16px` after image; `8px` metadata-to-title and title-to-excerpt; `16px` before tags.
- Title uses h3 styling.
- Optional thumbnail: `3:2`, square corners, cover crop; use author-supplied focal point or center.
- Body images are not subject to this crop.
- No whole-card link overlay.
- Card shadow remains fixed on hover; the title gets the link treatment.
- Grid cards stretch to the row height; tag rows align to the bottom where possible without truncation.

A missing thumbnail produces no empty placeholder.

**Signature:** a small printed panel physically offset from the page.

## 4.8 Post single: prose

**Reading surface**

- No enclosing card, border, or shadow.
- Default prose: Arial-family `18px/1.65`.
- Optional site-wide mono version: `16px/1.75`.
- Paragraph and standard block spacing: `24px`.
- First content block has no artificial top margin.
- No justified text.

**Headings**

- H2: `48px` above, `16px` below.
- H3: `32px` above, `12px` below.
- H4–H6: `24px` above, `8px` below.
- Heading anchor link: visible `#` in mono metadata size, with an accessible name identifying the heading.
- Anchor target scroll margin: `24px`.
- No skipped semantic levels introduced by the theme.

**Links**

- Blue on paper/panel.
- Always underlined: `1px`, offset `.16em`; `2px` on hover.
- External links do not open new tabs by default.
- Do not append decorative external-link icons to every sentence.

**Blockquotes**

- `3px` ink left rule.
- Left padding `24px`; no colored background.
- Prose styling retained; no automatic italicization.
- Citation: mono `13px`, top gap `12px`.
- Nested quote left padding becomes `16px`.

**Horizontal rules**

- `1px` ink.
- `48px` vertical margins.
- No centered stars, gradients, or ornamental dots.

**Lists**

- Indent `1.5em`.
- Item gap `8px`.
- Nested list margin `8px 0`.
- Native ordered numbering; no CSS-generated numbering that disappears from copying.
- Task lists use square checkboxes and retain meaningful checked state.

**Images and figures**

- Maximum width `100%`; height automatic.
- Preserve intrinsic aspect ratio; do not upscale beyond source width by default.
- Figure block margin `32px 0`.
- Caption top gap `8px`, mono `13px/1.4`, muted.
- Author-supplied alt text is separate from the caption.
- Decorative images have empty alt text.
- Screenshots may use a `1px` ink frame; ordinary photographs have no mandatory frame.
- No lightbox by default.

**Signature:** calm reading typography inside a visibly uncompromising editorial frame.

## 4.9 Code blocks

**Anatomy**

1. Terminal header: language or authored filename.
2. Optional progressively enhanced Copy button.
3. Horizontally scrollable code region.

**Geometry**

- Background `--code-bg`, text `--code-fg`.
- `1px` ink outer boundary.
- Header/body separator: `1px --code-muted`.
- Header minimum height `44px`, horizontal padding `16px`.
- Header label: mono `12px`, weight `900`, tracking `.08em`.
- Code padding: `24px`, reduced to `16px` below 640px.
- Code size `15px/1.6`.
- No shadow, rounding, faux traffic-light dots, or blinking cursor.
- Whitespace preserved; tabs display at four spaces.
- No wrapping by default. Horizontal scrolling stays inside the block.
- Code scroll region is keyboard-focusable and has a unique accessible label such as “Code sample 2, Go.”
- No line numbers by default.

**Syntax roles**

- Plain text, names, operators, punctuation: code foreground.
- Keywords and terminal prompts: lime.
- Strings and literal text: pink.
- Numbers: terminal blue.
- Comments: code muted; not italic.
- Errors: terminal red, never flashing.
- Highlighted lines: `--code-line-bg`; no opacity overlays.

**Copy states**

- Default: “COPY”, square `44px` control, terminal foreground border.
- Hover: lime fill, accent ink.
- Focus: shared focus ring.
- Success: “COPIED”, announced politely.
- Failure: “COPY FAILED”, with selectable code still available.
- Copy source excludes interface labels and any decorative prompt text not part of the original snippet.
- Without JavaScript, the Copy button is absent; code remains fully usable.

**Signature:** a real reading surface for code that resembles a terminal, not a screenshot of one.

## 4.10 Inline code

- Mono, `.9em`, inherited line-height.
- Panel fill; ink text.
- `1px` line border.
- Padding `.08em .24em`.
- Radius `0`.
- Long tokens may emergency-wrap; no hyphen insertion.
- Inline code inside links keeps the link underline and uses the appropriate readable link foreground.
- Inside terminal blocks, inline-code decoration is reset to the surrounding terminal treatment.

**Signature:** a small rectangular specimen label, not a rounded grey lozenge.

## 4.11 Footnotes

- Footnotes section follows a `1px` ink rule with `32px` spacing.
- Heading: `NOTES`, utility-label styling; semantic heading level follows the article.
- Notes: `16px/1.5`, not tiny metadata.
- Reference: mono `13px`, visibly bracketed, for example `[3]`.
- Backlink: visible “RETURN ↑”, minimum `44px` target.
- Native fragment links connect references and definitions; target focus must be verified in supported browsers.
- Footnote links use normal link/focus states.
- Long URLs and code wrap within the note column.

**Signature:** technical annotations, not faint superscripts relegated to illegibility.

## 4.12 Table of contents

- Labeled navigation: `ON THIS PAGE`.
- `1px` ink top border; `12px` top padding.
- Mono `14px/1.4`.
- Entries use minimum `44px` row height.
- H3 entries indent `16px`.
- Include H2 and H3 only.
- Display automatically on posts with at least three eligible headings.
- Desktop: sticky at `24px`; maximum height viewport minus `48px`; internal vertical scrolling when necessary.
- Below 960px: static, expanded, before article content.
- No scrollspy or claimed current section without actual behavior.
- Hover/focus follow normal link states.

**Signature:** a compact document index, not a floating rounded navigation widget.

## 4.13 Tag/category chips

- Mono `12px/1.25`, weight `900`, tracking `.04em`.
- Taxonomy text retains its authored casing.
- Minimum height `44px`; horizontal padding `12px`.
- `1px` ink boundary; transparent background; no shadow.
- Gap `8px`, wrapping.
- Hover: panel fill.
- Current term: lime fill, accent ink, semantic current state.
- Pressed: pink fill.
- Counts appear as plain metadata separated by `8px`.
- Noninteractive tags render as text labels, not disabled links.

**Signature:** square catalog labels rather than pills.

## 4.14 Pagination

- `1px` ink top rule; top padding `24px`.
- Flex layout: previous at start, page status in the middle, next at end.
- Previous/next controls: secondary button geometry, `44px` minimum.
- Status: mono `13px`, “Page 2 of 8”.
- Below 640px: controls form a two-column row; status occupies a separate centered row.
- Unavailable previous/next controls are plain muted text in the same allocated area, without borders or keyboard stops.
- Pagination container has an accessible navigation label.

**Signature:** document navigation with explicit position, not a row of rounded numbered dots.

## 4.15 Author / byline

- Byline: author name, publication date, optional updated date, optional reading time.
- Mono `13px/1.4`; wrap with `8px` horizontal gaps.
- Use semantic dates with machine-readable values.
- Updated date appears only when meaningfully different from publication.
- Author card at article end: `1px` ink top rule, `24px` top padding.
- Optional avatar: `48 × 48px`, square, no shadow.
- Avatar-to-text gap `16px`.
- Name: `16px`, weight `700`; biography: prose `16px/1.5`.
- Omit missing fields. Do not generate fake reading-time precision or placeholder avatars.

**Signature:** a colophon, not a social-profile bubble.

## 4.16 Callout / admonition: retro-GUI dialog

This is a **static content aside**, not an ARIA dialog. It must not trap focus or imply modality.

**Anatomy**

1. Beveled chrome.
2. Title bar.
3. Type icon and explicit type label.
4. Optional authored title.
5. Content body.
6. Optional genuine action link/button.

**Geometry**

- Use the exact bevel recipe.
- `3px` hard external shadow.
- Title bar: invariant terminal background/foreground, minimum height `36px`, padding `8px 12px`.
- Title typography: mono `12px`, weight `900`, tracking `.08em`.
- Icon: `16px`, square-ended, pixel-like geometry.
- Body: panel fill, padding `16px`, normal prose size.
- Outer block margin `32px 0`.

**Variants**

- Note/info: label “NOTE”; otherwise neutral.
- Tip/success: “TIP” or “SUCCESS”; lime label block with accent ink.
- Warning: “WARNING” plus warning icon; neutral panel.
- Error: “ERROR”; red text/rule on panel.
- Editorial: pink label block with accent ink; maximum once per page.

No fake close, minimize, or maximize buttons. A dismiss button is allowed only if dismissal is implemented and has a meaningful purpose; it is not part of the default component.

Static admonitions do not use `role="alert"`. Dynamically inserted submission errors may.

**Signature:** a small desktop dialog repurposed as editorial furniture.

## 4.17 Buttons

Common geometry:

- Minimum height `44px`.
- Horizontal padding `16px`.
- Mono `14px/1.25`, weight `900`, tracking `.04em`.
- `1px` ink border except ghost.
- Icon gap `8px`.
- Text may wrap; no fixed height.
- Square corners.

| Variant | Default | Hover | Pressed |
|---|---|---|---|
| Primary | Lime, accent ink, 3px shadow | Pink, accent ink, 2px shadow | Pink, no shadow |
| Secondary | Panel, ink, 2px shadow | Lime, accent ink, 2px shadow | Lime, no shadow |
| Ghost | Transparent, ink, no border/shadow | Panel, underline | Pink, accent ink |
| Destructive | Error fill, error-on-fill, 3px shadow | Same colors, 2px shadow | Same colors, no shadow |

Focus always adds the shared ring. Disabled uses the shared disabled contract. Loading changes the visible label and announces status; no spinner is required.

**Signature:** rigid mechanical controls with hard, shallow depth.

## 4.18 Forms and inputs

- Form maximum width: `42rem`.
- Field groups separated by `24px`.
- Labels above fields: mono `14px`, weight `700`, gap `8px`.
- Help text: mono `13px/1.4`, muted, gap `8px`.
- Input surface: panel.
- Boundary: `1px` ink.
- Minimum height `48px`; padding `12px`.
- Input text: mono `16px/1.5`, including on mobile to avoid browser auto-zoom behavior associated with smaller fields.
- Textarea: minimum height `160px`, vertical resize enabled.
- Placeholder: muted; never substitutes for a label.
- Required fields use visible “(required)” text.
- Checkbox: square `20px`, ink boundary, ink check on lime when checked; retain native input semantics.
- Select: square authored field with a simple down-chevron; browser-owned option picker is outside the theme’s geometry.

**States**

- Hover: boundary unchanged; no pale-border ambiguity.
- Focus: shared ring.
- Invalid: `1px` error boundary, visible error message, programmatic association, invalid state.
- Read-only: paper surface and a visible “Read-only” label; selectable text.
- Disabled: shared disabled treatment.
- Success: explicit status message, optionally lime-backed.
- Submission failure: error summary before the form, linked to relevant fields; preserve user input.

A contact form is shipped only when an action endpoint is configured. Do not ship a fake form that pretends to send messages.

**Signature:** labeled technical fields, not floating-label SaaS inputs.

## 4.19 Tables

Same component for article tables and theme-owned data tables.

- Wrapper maximum width `100%`; horizontal scrolling when needed.
- Wrapper is keyboard-focusable and accessibly labeled if it scrolls.
- Table text: `16px/1.5`.
- Cells: `12px 16px`; below 640px, `12px`.
- Header: mono `13px`, weight `900`, authored casing retained.
- Header bottom rule: `1px` ink.
- Body row separators: `1px` line.
- Outer top and bottom rules: `1px` ink.
- No vertical grid by default.
- No zebra stripes or noninteractive hover fills.
- Numeric columns align to the end; text aligns to the start.
- Captions precede the table, mono `13px`, gap `8px`.
- Use proper header associations; complex tables require explicit row/column relationships.
- Sorting controls are not included unless actual sorting is implemented.

**Signature:** a typeset specification table rather than a dashboard data grid.

## 4.20 404

- Utility label: `04 / NOT FOUND`.
- H1: literal `404`, display-xl.
- Following text: “Page not found.” using h3 styling.
- Explanation: one short prose paragraph.
- Two actions: Home primary; Posts secondary when a posts section exists.
- No animation, fake terminal stack trace, or automatic timed redirect.
- Document title: “Page not found — [site name]”.

**Signature:** one oversized number carries the page.

## 4.21 Footer

- Top `1px` ink rule.
- Margin above: `64px`, reduced to `48px` below 640px.
- Padding: `24px 0 32px`.
- Label: `99 / END`.
- Copyright/site attribution: mono `13px`, muted.
- Utility links: mono `13px`, normal link treatment, `44px` hit height.
- Desktop two columns; mobile stacked with `16px` gap.
- No obligatory promotional paragraph or giant second hero.

**Signature:** a compact printer’s colophon.

## 4.22 Edge text and corner brackets

Default placement: **home page only**.

### Vertical Base64 strip

- Static value: `SGVsbG8sIHdvcmxkIQ==` — “Hello, world!”
- Mono `12px/1.25`, tracking `.08em`, muted.
- Vertical right-to-left writing mode; the encoded string itself retains left-to-right character order.
- Absolute placement at the container’s inline end, `28px` outside the content edge, aligned `16px` below the hero top.
- Only visible from `80rem` / 1280px upward.
- Hidden from assistive technology, excluded from focus and pointer interaction.
- Never encode secrets, user data, or a changing tracking identifier.

### Corner brackets

- `Γ` at the hero’s upper-start corner; `¬` at upper-end.
- Serif stack, `24px/1`, ink.
- Hero reserves `24px` top clearance for the glyphs.
- Decorative and hidden from assistive technology.
- No orbit animation, rotation, or following the cursor.

**Signature:** a small authored joke at the page edge, not a background of hacker theater.

---

# 5. Page recipes

## Home

1. Header.
2. Hero: `00 / INDEX`, site title or explicit home headline, optional description, maximum two actions.
3. Optional factual truth strip.
4. `01 / LATEST`: six newest posts as ruled list items.
5. Optional `02 / WORK`: up to three project cards.
6. Footer.

- Home hero uses the 150px-cap display token.
- Latest posts sort by publication date descending; ties resolve by permalink ascending.
- Missing optional sections disappear completely.
- Base64 strip and bracket pair appear here only.

**Carrying device:** the oversized headline with one optional lime-marked phrase.

## Section list

1. Header.
2. Internal hero: section title, description, item count.
3. `01 / ENTRIES`.
4. Ten entries per page.
5. Pagination.
6. Footer.

- Posts section: ruled list.
- Projects section: card grid.
- Other sections default to ruled list.
- Posts sort by publication date descending.
- Projects sort by weight ascending, then title ascending.
- Other sections sort by date descending, then permalink ascending.

**Carrying device:** the ruled editorial index.

## Single post

1. Header.
2. Breadcrumbs, mono `13px`, with current page rendered as text.
3. `00 / ARTICLE`.
4. Title, optional deck, byline, tags.
5. Optional lead figure.
6. Main/TOC grid.
7. Footnotes when present.
8. Author card.
9. Older/newer article navigation.
10. Footer.

- Title occupies up to desktop columns 1–10.
- Body occupies columns 1–8; TOC occupies 10–12.
- If no TOC exists, prose remains at its reading measure; do not expand text to 1160px.
- Older/newer links include destination titles, not arrows alone.

**Carrying device:** the tight display headline over an unboxed reading column; terminal panels carry code-heavy articles.

## Taxonomy list

Example: all tags.

1. Header.
2. Hero: `00 / TAXONOMY`, title “Tags”.
3. Alphabetically sorted terms as full-width ruled rows.
4. Each row: term link and post count.
5. Footer.

All terms appear; no pagination by default. Respect localized display names and do not uppercase them.

**Carrying device:** a catalog of names and counts, not a cloud of differently sized words.

## Taxonomy term

Example: posts tagged Hugo.

1. Header.
2. Small taxonomy name above the term H1.
3. Current term shown as a lime-backed square label.
4. Count and optional term description.
5. Ten matching posts per page in the ruled list.
6. Pagination.
7. Footer.

**Carrying device:** the selected catalog label followed by the editorial index.

## 404

Use the component composition specified above, vertically placed with `64px` top spacing below the header—not artificially centered in a fixed-height viewport.

**Carrying device:** `404` at the display-xl scale.

## Standalone page

1. Header.
2. `00 / PAGE`.
3. Internal H1 and optional description.
4. Prose at `68ch`.
5. Optional TOC only when explicitly enabled.
6. Footer.

No dates, reading time, tags, or author card unless the page explicitly requests them.

**Carrying device:** an oversized title followed by restrained editorial typography.

---

# 6. What this theme does better

| Reference tendency or risk | Theme improvement |
|---|---|
| TypeSafe’s measured 12px body is unsuitable for sustained reading | `18px` prose; `16px` mono option; utility labels never below `12px` |
| Multiple expressive fonts can make content and fallback behavior fragile | Three system-font roles, with serif restricted to explicit epigraphs |
| Arial `900` can be mistaken for a guaranteed black font | Acknowledge real font substitution; test representative platform stacks |
| Ultra-tight heading leading can collide on multiline or accented content | `1.02–1.05` Latin display leading; `1.2` for scripts needing more room |
| Decorative acid colors can be misused as low-contrast text | Explicit foreground/background contracts and verified ratios |
| Thin, pale rules may be mistaken for adequate control boundaries | Ink borders on all operable controls; pale rules remain decorative |
| Deliberate casing inconsistency fights real titles and localization | Preserve authored casing; style theme-owned labels only |
| Novelty typography can overwhelm code and long-form prose | Stable reading measures, terminal contrast, wrapping and scroll rules |
| A fixed visual composition can fail with long multilingual titles | No fixed title heights, forced breaks, clipping, or line clamping |
| Retro devices can imply fake interactivity | No fake dialog buttons, status claims, modal roles, or nonfunctional forms |
| Card-heavy themes can turn every article into a boxed dashboard | Ruled lists are the default; cards are primarily for selected work |
| Appearance behavior is not established by the supplied measurements | Ship and test explicit light, ink-paper dark, forced-colors, and print modes |

We should not infer unmeasured accessibility failures or the absence of dark mode on either reference. The point is to make the theme’s own behavior explicit and testable.

**The central improvement:** borrow the visual grammar, not the reference sites’ content-specific tricks.

---

# 7. Hugo implementation map

## Architecture decision

**Use hand-written plain CSS and custom properties. No framework, Tailwind, Sass, PostCSS, or Node build dependency.**

Use **Hugo Pipes only for concatenation, minification, fingerprinting, and processing the small parameter stylesheet**. Hugo is already building the site; these operations do not justify a separate frontend toolchain.

Authoring remains build-tool-free CSS. A user can understand and edit the theme without package installation.

## Token ownership and overrides

### Source of truth

`assets/css/tokens.css`

- Contains the canonical light `:root` token sheet.
- Contains documented appearance overrides and responsive token changes.
- Only this file defines baseline design values.
- Component files consume tokens rather than reintroducing near-identical colors or spacing values.

### User configuration

Support the normal Hugo configuration locations, including:

`config/_default/params.toml`

Expose a deliberately small API:

| Parameter | Default | Allowed values / purpose |
|---|---|---|
| `design.appearance` | `auto` | `auto`, `light`, `dark` |
| `design.prose` | `sans` | `sans`, `mono` |
| `design.ornaments` | `true` | Home-only decorative devices |
| `design.lime` | `#d4ff3f` | Optional accent override |
| `design.pink` | `#ee5ba6` | Optional accent override |
| `design.containerMax` | `1160px` | Advanced layout override |
| `features.copyCode` | `true` | Progressive enhancement |
| `features.postTOC` | `true` | Still subject to heading-count threshold |

- Generate a small token-override stylesheet from these validated parameters.
- Do not expose separate colors for every component.
- Arbitrary palette overrides are explicitly **outside the certified default contrast contract** until rechecked.
- Advanced users may append `assets/css/custom.css`.
- Do not generate inline style attributes throughout templates.

### Stylesheet order

1. Minimal reset.
2. Tokens and appearance rules.
3. Base typography and layout.
4. Components.
5. Prose and syntax styles.
6. Accessibility/print rules.
7. Generated parameter overrides.
8. Optional user stylesheet.

Document that user overrides can invalidate accessibility and visual guarantees.

## Template and partial inventory

Use the corresponding lookup names for the supported Hugo version; organize responsibilities as follows.

### Base and page templates

- Base layout.
- Home.
- Section list.
- Single post.
- Standalone page.
- Taxonomy list.
- Taxonomy term.
- 404.
- Projects section/list variant.

### Shared partials

- Document head: metadata, title, CSS, color-scheme.
- Skip link.
- Header/masthead.
- Primary navigation.
- Breadcrumbs.
- Hero.
- Section label.
- Truth strip.
- Post list item.
- Post card.
- Byline.
- Author card.
- Taxonomy chips.
- TOC.
- Pagination.
- Previous/next article navigation.
- Figure.
- Admonition.
- Footer.
- Ornaments.
- Inline SVG icon dispatcher.

No icon font. Use a small, theme-owned inline SVG set with square-ended `1.5px` strokes, plus a few simple pixel-style decorative symbols for GUI callouts.

## Markdown render hooks

Provide hooks for:

- Links: normal semantics, safe external handling, no forced new tab.
- Images: responsive figures where supported by page resources.
- Headings: stable IDs and accessible anchor links.
- Fenced code: terminal wrapper, syntax classes, optional Copy enhancement.

Use Hugo’s Markdown footnotes and table output, with the required surrounding styling and semantics. Complex authored tables may need a dedicated shortcode rather than pretending every Markdown table has sufficient associations.

## Shortcode inventory

| Shortcode | Purpose | Required behavior |
|---|---|---|
| `mark` | Lime or explicit pink highlight | Semantic mark, fixed accent foreground |
| `callout` | Note/tip/success/warning/error/editorial | Static aside, explicit type label |
| `figure` | Caption, credit, alt, optional dark source | No forced crop in prose |
| `epigraph` | Controlled serif contrast | Optional attribution |
| `button` | Styled navigation link | Must have a destination; not fake action semantics |
| `codefile` | Code with filename/label/highlighted lines | Uses terminal component |
| `table` | Complex captioned data table wrapper | Requires accessible caption and headers |
| `contact` | Configured contact form | Refuse/omit output without a real endpoint |

Do not create a shortcode for ordinary headings, paragraphs, lists, or standard code fences.

## Content contracts

### Site-level

- Site title.
- Description, optional.
- Main menu.
- Author data, optional.
- Truth-strip items, optional.
- Home headline override, optional.
- Home highlighted phrase, optional exact substring of the headline.
- Home actions, maximum two.
- Social/utility links.

Hero highlight handling must safely identify and mark the supplied substring; do not require arbitrary HTML in a title.

### Page-level

- Title.
- Description, optional.
- Publication and modification dates.
- Tags/categories.
- Author reference.
- Lead image with alt/caption/credit.
- Card image and optional focal point.
- TOC override.
- Project weight.
- Draft and publish-state metadata.

### Image pipeline

- Local page-bundle resources preferred.
- Generate responsive widths at `480`, `800`, and `1160px`, never larger than the source.
- Produce WebP plus an appropriate original-format fallback where Hugo supports the operation.
- Set intrinsic dimensions to prevent layout shift.
- Lazy-load below-the-fold images; do not lazy-load the principal above-the-fold lead image.
- External images are not silently fetched and transformed.
- Do not use CSS filters to simulate dark variants.

## JavaScript

Default content, navigation, TOC, and appearance require **no JavaScript**.

The optional script handles Copy buttons and any necessary accessible enhancement around that feature.

- No client-side framework.
- No hydration.
- No client-side syntax highlighter.
- No scrollspy by default.
- No analytics dependency.
- No animation library.

## Versioning and documentation

- Version the token API and theme releases.
- Changing default colors, display scale, layout breakpoints, or token meaning is a documented visual-system change.
- Include a component specimen page and content stress-test fixtures.
- Document system-font variation: the design can be exact in rules without promising identical Arial metrics on every operating system.

---

# 8. Build-verification checklist

## A. Palette and contrast

- [ ] Calculate contrast from actual computed foreground/background colors, not token names.
- [ ] Verify every permitted pair in the contrast tables within rounding tolerance of `±0.02`.
- [ ] Normal text meets `4.5:1`; meaningful non-text boundaries/indicators meet `3:1`.
- [ ] Muted text remains at least `5.46:1` on default light paper.
- [ ] No lime or pink foreground text appears on light paper/panel.
- [ ] Highlighted links use accent ink and an underline.
- [ ] Pink syntax strings remain at least `4.96:1` on highlighted code lines.
- [ ] Error states contain text/icon information, not color alone.
- [ ] Parameter-based accent overrides trigger the same checks.

## B. Geometry audit

- [ ] Computed border radius is `0px` on every theme-owned element and pseudo-element.
- [ ] There are no declared radius exceptions.
- [ ] All standard authored structural borders are `1px`.
- [ ] The only thicker standard lines are the `3px` blockquote rule and the specified focus/bevel layers.
- [ ] Every shadow has a blur radius of zero.
- [ ] Elevation shadows are exactly `2px 2px` or `3px 3px`.
- [ ] No UI gradients, backdrop blur, text glow, or filter-based soft elevation exist.
- [ ] No rounded image crops or circular avatar masks exist.

## C. Font and asset audit

- [ ] No `@font-face`.
- [ ] No WOFF, WOFF2, TTF, OTF, font data URI, remote font stylesheet, or icon-font request.
- [ ] No script-created webfonts.
- [ ] Network log reports zero downloaded font resources.
- [ ] Fonts resolve through the declared system stacks.
- [ ] Main CSS, including syntax and default generated overrides: **maximum 24 KiB uncompressed and 7 KiB gzip**.
- [ ] Optional JavaScript: **maximum 4 KiB uncompressed and 2 KiB gzip**.
- [ ] No runtime framework or external dependency is required to read the site.
- [ ] Images have intrinsic dimensions and responsive sources where applicable.

## D. Keyboard and semantics

- [ ] Skip link is first and visibly usable.
- [ ] Traverse header, nav, title links, card links, tags, TOC, code, footnotes, pagination, forms, and footer using only the keyboard.
- [ ] Focus is always visible and never obscured by a sticky region or clipped scrolling container.
- [ ] No hover-only controls.
- [ ] No card contains nested links or a link overlay intercepting child actions.
- [ ] All standalone controls meet `44 × 44px`.
- [ ] Inline-link exceptions do not create overlapping hit areas.
- [ ] Code and wide tables can be horizontally scrolled by keyboard.
- [ ] Footnote and heading fragment navigation is tested with screen readers.
- [ ] Static GUI callouts are not exposed as modal dialogs or live alerts.
- [ ] Invalid form fields have associated messages; submission errors preserve data.
- [ ] Copy success/failure is announced without moving focus.

## E. Responsive and content stress tests

Test at **320, 375, 768, 1024, and 1440 CSS pixels**, in both appearances.

Fixtures must include:

- [ ] A 160-character title.
- [ ] An 80-character unbroken identifier.
- [ ] Latin diacritics, German compounds, Arabic, Hindi, Japanese, and mixed-direction inline code.
- [ ] A post without an image, description, tags, or author.
- [ ] A post with at least 20 H2/H3 headings.
- [ ] Nested lists, long footnotes, and long URLs.
- [ ] A 12-column table.
- [ ] Code containing 200-character lines.
- [ ] Portrait, landscape, transparent, and very small images.
- [ ] Ten long taxonomy names.
- [ ] Browser zoom to 400%, including a 1280px viewport yielding approximately 320 CSS pixels.
- [ ] User text enlargement without loss of content or functionality.
- [ ] No horizontal **page** scrolling; scrolling remains confined to legitimate code/table regions.
- [ ] No fixed-height title clipping, unintended line clamping, or overlapping display text.

## F. Appearance and motion

- [ ] OS light/dark changes update appearance correctly in auto mode.
- [ ] Site-pinned light/dark ignores OS preference predictably.
- [ ] Accent text remains dark on lime/pink in dark appearance.
- [ ] Terminal syntax colors remain unchanged across appearances.
- [ ] Forced-colors mode retains boundaries, links, and focus.
- [ ] Reduced-motion mode contains no animation or smooth scroll.
- [ ] Print output contains readable code and tables, not dark ink slabs or clipped scrollports.
- [ ] Photographs and screenshots are not automatically inverted.

## G. “Does it still read as this style?” acceptance gate

A screenshot cannot objectively certify a style name, but the visual test can still be repeatable.

Maintain approved home, list, and single-post screenshots for each appearance and canonical font environment. A release fails art-direction review if any of these disappear:

- [ ] Warm paper / near-black ink in light mode.
- [ ] At least one unmistakably oversized, tightly tracked display heading.
- [ ] Mono utility typography visibly distinct from prose.
- [ ] Thin ruled editorial organization.
- [ ] Square, hard-shadowed controls or cards where the recipe calls for them.
- [ ] A genuine lime block highlight or selected/action surface—not merely a colored word.
- [ ] Blue underlined prose links.
- [ ] Terminal treatment for code.
- [ ] Restraint: no extra palette, random type mixing, or decorative effects added to compensate for weak layout.

**Final art-direction test:** remove the lime and pink temporarily. The page should still read as a forceful editorial system because of its type, rules, spacing, and geometry. Restore the accents, and it should read unmistakably as **INK / PAPER’s editorial neubrutalism**, not as a generic blog with a bright button.