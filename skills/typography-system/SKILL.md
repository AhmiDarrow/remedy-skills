---
name: typography-system
version: 1.0.1
description: >
  Set up a type system with role-based styles, scale, line height, measure, font fallbacks and loading choices, tested with real content. Use when text styles are inconsistent or a product or publication needs them.
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
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: typography-system
  official: true
  domain: design
  security_flags: []
---

# Typography System

## When to use
Headings and body text vary from screen to screen, or typography is being established.

## Steps
1. `grep` current font families, sizes, weights, line heights and letter spacing. Note platform type styles or brand fonts already required.
2. Check each font's licence, language coverage, weights, italics, numerals and legibility of look-alikes such as I, l and 1.
3. Prefer one family with enough range. Add a second only for a clear contrast of role.
4. Set body size first by testing on target devices; 16 px is a common web starting point.
5. Define roles actually needed (display, headings, body, small, label, caption, code, numeric). A ratio can suggest sizes, but adjust by eye and merge steps that look alike.
6. For each role set size, line height, weight, tracking and paragraph spacing. Body line height around 1.4 to 1.6 is a usual start; large headings need less.
7. Keep reading measure near 45 to 75 characters, with density rules for tables and controls.
8. Use relative units on the web so user font settings apply, and platform text styles in native apps.
9. Choose fallbacks and a loading approach: only needed files and subsets, a visible-text `font-display` strategy and matched metrics to limit shifts.
10. Implement as tokens or styles, keeping heading levels based on document structure rather than appearance. Test long headings, translations, other scripts, tabular figures, 200% enlargement and user text-spacing overrides.

## Watch out for
- Synthetic bold or italic appearing because a weight file is missing.
- Viewport-only font sizing that ignores zoom.
- Subsetting that drops characters needed for names.
- Light grey thin text that looks elegant on one screen and vanishes on another.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each role has complete values and a usage rule, fonts and fallbacks are confirmed, real content renders at narrow, wide and enlarged settings, and untested languages or devices are listed.
