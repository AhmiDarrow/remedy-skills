---
name: fluid-type-clamp
version: 1.0.0
description: >
  Create fluid font sizes and spacing with CSS clamp that scale between two viewport widths and still respect user zoom. Use when type jumps at breakpoints or is too large on phones.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - css
  - typography
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: fluid-type-clamp
  official: true
  domain: design
  security_flags: []
---

# Fluid Type Clamp

## When to use
Headings overflow small screens, or a type scale is maintained through many breakpoint overrides.

## Steps
1. Choose two viewport widths, such as 360 and 1280 CSS pixels, and for each text style its size at both ends.
2. Compute the line: slope = (maxSize - minSize) / (maxWidth - minWidth); intercept = minSize - slope x minWidth, with all values in pixels.
3. Write `clamp(min, intercept + slope*100 vw, max)`, converting min, intercept and max to rem by dividing by the 16 px base. Example, 32 to 56 px over 360 to 1280: `clamp(2rem, 1.413rem + 2.609vw, 3.5rem)`.
4. Generate the values with a small script rather than by hand and keep its inputs beside the tokens.
5. Use a smaller scale ratio at the narrow end than the wide end, so headings do not dominate phones. Keep body text near constant.
6. Tie line height to the style: unitless, tighter for large headings, looser for body.
7. Limit prose measure to about 45 to 75 characters with a `max-width` in `ch`.
8. Test at both end widths, in between, with browser zoom at 200% and with a larger default font size.

## Watch out for
- A size made of `vw` alone does not grow with zoom. Always include a rem term, and be wary when max exceeds about 2.5 times min, which can prevent text from reaching 200% enlargement.
- `px` bounds inside clamp ignore the user's default font size.
- Setting `html { font-size: 62.5% }` changes every rem and breaks third-party components.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each style measures its stated size at both end widths, interpolates between them, and visibly enlarges at 200% zoom without clipping or horizontal scroll.
