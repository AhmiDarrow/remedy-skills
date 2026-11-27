---
name: dark-mode-implement
version: 1.0.0
description: >
  Add a dark theme with semantic color tokens, system preference, a persisted override and no flash on load. Use when adding dark mode or fixing one that was made by inverting colors.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - theming
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: dark-mode-implement
  official: true
  domain: frontend
  security_flags: []
---

# Dark Mode Implement

## When to use
A product needs light, dark and follow-system choices, or an existing dark theme has unreadable patches.

## Steps
1. `grep` for hex, `rgb(`, `hsl(` and named colors in styles, SVGs, canvas code and chart configs. This is the real work list.
2. Replace them with semantic tokens named by role (surface, raised surface, text, muted text, border, accent, on-accent, danger), not by shade.
3. Define dark values deliberately. Use a very dark neutral rather than pure black unless targeting power saving, make raised surfaces lighter than the page since shadows barely read, and reduce saturation of large accent areas.
4. Set `color-scheme: light dark` (or the chosen one per theme) so native controls and scrollbars follow.
5. Offer System, Light and Dark. Follow `prefers-color-scheme` when System is chosen and react to changes while the page is open.
6. Apply the stored override with a small blocking script in `head`, wrapping storage access in try/catch, or render it server-side from a cookie.
7. Handle assets: logos with dark text, screenshots, illustrations with white backgrounds, favicons and `meta name="theme-color"` with media queries.
8. Measure contrast in both themes for text, borders of inputs, focus rings and disabled states.
9. Walk every route, including email-style previews, third-party embeds, loading skeletons and printing.

## Watch out for
- Storing only a boolean loses the difference between chose light and follows system.
- Overlay colors made from black at low opacity vanish on dark surfaces.
- Theme transitions applied to every element animate the whole page on load.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All three choices work, reload shows no flash, the hard-coded color search is clean apart from documented exceptions, and measured text contrast meets the project target in both themes.
