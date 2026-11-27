---
name: iconography-guide
version: 1.0.1
description: >
  Write icon rules covering grid, stroke, style, metaphors, naming, accessibility and SVG export, based on the existing set. Use when icons look mismatched or new ones are being drawn or added.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ui
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: iconography-guide
  official: true
  domain: design
  security_flags: []
---

# Iconography Guide

## When to use
A product mixes icon styles or contributors need a standard for adding more.

## Steps
1. `glob` icon files and `grep` usages. Note sources, licences, sizes, styles, duplicates, and one symbol used for several meanings or the reverse.
2. Decide whether to adopt or extend an existing licensed set before drawing a custom one.
3. Define the grid per delivered size (commonly 16, 20 or 24 px): live area, padding, keyline shapes. Compensate optically so circles, squares and triangles feel equal in weight.
4. Fix stroke width, caps, joins, corner radius, perspective and level of detail. Redraw or simplify for small sizes instead of only scaling down.
5. Say when filled and outlined styles appear, such as filled for selected, and never as the only state cue if the difference is subtle.
6. Keep a registry: name by meaning or object consistently, the approved meaning, search synonyms and banned uses.
7. Require visible text for unfamiliar or high-stakes actions. Icon-only buttons need an accessible name describing the action; decorative icons are hidden from assistive technology.
8. Check meaningful icons reach 3:1 against their background, and that the clickable target is large enough even when the glyph is small (at least 24 by 24 CSS px for WCAG 2.2 AA, with exceptions; larger is better for touch).
9. Specify export: correct `viewBox`, no fixed colours (use `currentColor` for single-colour icons), no editor metadata, embedded rasters or scripts, and unique IDs where gradients or masks exist.
10. Document how to request, review and deprecate icons, with good and bad examples.

## Watch out for
- Mirroring every icon for right-to-left; only directional ones should flip.
- SVG optimisers that remove `viewBox` or break shapes; compare before and after.
- Metaphors that depend on one culture or obsolete objects without testing recognition.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The guide states grid, stroke, style, naming, accessibility and export rules, includes a registry of current icons, and lists collisions, licence doubts and files needing redraw.
