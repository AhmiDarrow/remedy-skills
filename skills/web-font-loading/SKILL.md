---
name: web-font-loading
version: 1.0.0
description: >
  Load web fonts without invisible text or layout jumps through subsetting, preload and metric-matched fallbacks. Use when text flashes, shifts on font swap or font files are heavy.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - performance
  - typography
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
metadata:
  source: library
  library_id: web-font-loading
  official: true
  domain: frontend
  security_flags: []
---

# Web Font Loading

## When to use
Headlines reflow after load, text is blank on slow networks, or many font files download on every page.

## Steps
1. List requested font files with size and which text on first view needs each. Remove unused weights and styles.
2. Check the font licence permits self-hosting, conversion and subsetting before doing any of them.
3. Serve WOFF2. Consider a variable font only if its size beats the static weights you really use.
4. Subset by script with `unicode-range` blocks, keeping the characters every supported locale and user-entered names need.
5. Choose `font-display` per role: `swap` for brand text that must appear, `optional` where avoiding a late swap matters more than using the font.
6. Build a fallback `@font-face` from a local system font with `size-adjust`, `ascent-override`, `descent-override` and `line-gap-override` tuned to the web font, and put it next in the stack.
7. Preload only the one or two files needed for first paint, with `as="font"`, `type="font/woff2"` and `crossorigin`.
8. Give hashed font files long immutable caching.
9. Test with cache off and throttling; compare line breaks and measured layout shift before and after the swap.

## Watch out for
- Omitting `crossorigin` on a font preload makes the browser fetch the file twice, even on the same origin.
- Declaring only the regular face lets the browser synthesise fake bold and italic.
- Over-tight subsetting makes single accented letters render in the fallback font mid-word.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
First-view fonts are the listed few, text is readable throughout loading, no duplicate font requests appear, and the shift caused by the swap is measured and within the target.
