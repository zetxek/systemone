---
title: "Notes on editorial neubrutalism"
date: 2026-02-03
description: "Nine signatures, and what immediately breaks the style — a heading-heavy post for testing the table of contents in a later stage."
tags: ["design-system", "typography"]
---

Editorial neubrutalism is the umbrella term Systemone's design spec uses for
its own visual grammar: oversized display type, monospace utility text,
square geometry, thin ink rules, and occasional hard-offset shadows on warm
paper. This post walks through the nine signatures and a few of the things
that break them, mostly as a fixture for headings — this page has enough
`h2`/`h3` structure to be a realistic candidate for a future table of
contents component.

## Square boxes

Zero radius on every authored component and pseudo-element. Buttons, inputs,
checkboxes, images, code, tags, menus, focus rings, and avatars are all
square. There is no authored exception.

### Where this shows up

Every interactive control in the theme inherits `--radius: 0px` from the
token sheet, rather than each component declaring its own value.

### What it rules out

Rounded cards, pill tags, and circular avatar crops are all explicitly out
of bounds.

## Paper and ink

Large, quiet, nearly monochrome surfaces — not a collection of colored
cards. Lime and pink are reserved for principal signals and editorial
interruptions, not decoration.

### Contrast discipline

Every permitted foreground/background pair in the spec is independently
verified against the WCAG relative-luminance formula, rounded to two
decimals.

## Oversized display typography

Arial-family, weight 900, tracking down to `-.07em` on the largest sizes.
Long multilingual titles are never clipped to preserve a poster composition.

### Leading, relaxed on purpose

The reference material this style borrows from uses very tight leading —
Systemone relaxes it slightly so multiline and accented titles survive.

## Monospace infrastructure

Navigation, labels, dates, tags, captions, controls, and code all use the
same monospace stack, so interface chrome reads as distinct from article
prose at a glance.

## Thin structural rules

Predominantly `1px` ink lines. Pale lines are secondary separators only —
never the sole visible boundary of an input, button, checkbox, or focus
indicator.

## Hard elevation

Exactly `2px` or `3px` offset shadows, with zero blur, on buttons, cards,
and retro callouts — not on every panel.

## Block highlights

Acid lime behind ink text works as a highlighter mark, not a decorative
underline. At most one authored phrase per heading.

## Explicit editorial organization

Visible section identifiers such as `00 / INDEX`, strong alignment, and
deliberate whitespace carry a lot of the visual identity on their own.

## One controlled retro layer

Terminal code panels and GUI-style admonitions, not an entire simulated
operating system.
