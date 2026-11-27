---
name: screenshot-to-ui-build
version: 1.0.0
description: >
  Reproduce a design screenshot or mockup in code faithfully by extracting measurements and verifying with overlay comparison. Use when asked to build a screen that matches a picture.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - design
  - ui
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
  - edit
  - bash
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: screenshot-to-ui-build
  official: true
  domain: frontend
  security_flags: []
---

# Screenshot To Ui Build

## When to use
The input is an image, not a design file with specs, and the result should visibly match it.

## Steps
1. Look at the image closely and establish its pixel size and likely scale factor, so a 2x capture is not built at double size.
2. Ask for or find the source design, fonts and assets. State what is unavailable and which substitute you use.
3. Search the codebase for existing components and tokens that correspond, and use them; list places where the picture deviates from tokens and ask which wins.
4. Before coding, write an inventory top to bottom: regions, alignment edges, spacing values, type sizes and weights, colors, radii, borders, shadows, icons.
5. Snap near-equal measurements to the project's spacing and type scale.
6. Build structure first with real semantic elements, then spacing, then type, then color and effects.
7. Render at the same CSS width as the design, screenshot, and compare side by side or overlaid. Fix the largest differences first and repeat.
8. Then add what a still image cannot show: hover, focus, disabled, loading, empty, long text and narrower widths. Label these as your proposals.

## Watch out for
- Declaring a match from reading your own code without viewing the rendering.
- Absolute positioning to copy pixels, which collapses with real content.
- Colors sampled from a compressed screenshot are slightly off; prefer token values.
- Invented text, figures or logos filling unreadable areas must be marked as placeholders.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A same-width screenshot of the build has been compared with the source, remaining differences are listed with reasons, and the layout survives long text and a narrow viewport.
