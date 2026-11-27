---
name: color-system
version: 1.0.1
description: >
  Define or repair a UI colour system with role-based colours, state variants, light and dark pairs and measured contrast. Use when a product has ad hoc colours, unreadable text or a new brand palette.
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
  - bash
metadata:
  source: library
  library_id: color-system
  official: true
  domain: design
  security_flags: []
---

# Color System

## When to use
Colours need to become a coherent, accessible set of roles. Token file structure and build pipeline are a separate concern.

## Steps
1. `grep` styles for hex, `rgb`, `hsl`, `oklch` and named colours. Note brand colours that are fixed and the themes required.
2. List the roles the interface really uses: page and raised surfaces, primary and muted text, borders, accent and text on accent, focus indicator, selection, and danger, warning, success and info, each with foreground, background and border where needed.
3. Build neutral and hue ramps with even perceived lightness steps. A perceptual space such as OKLCH helps, but check results are within the target gamut and have fallbacks if needed.
4. Assign ramp steps to roles, then define hover, pressed, disabled and selected deliberately.
5. Tune dark values separately instead of inverting; saturation and surface steps usually need adjustment.
6. Write the required pairs and compute contrast with a short script. WCAG AA: 4.5:1 for normal text, 3:1 for large text, and 3:1 for meaningful graphics and the visual cues needed to identify controls and states. Disabled controls are exempt but should stay discernible.
7. Composite translucent colours over each real background before measuring, including hover rows and tinted alerts.
8. Pair every status colour with text or an icon, and check chart or status sets under colour-vision simulation.
9. Document each role with do and don't examples, map to the project's existing variables or theme, and migrate usages in reviewable steps.

## Watch out for
- A brand colour that fails as text may need a darker text variant while the original stays decorative.
- Reusing the danger red as a brand accent removes its warning meaning.
- Rounding 4.49 up to a pass.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each role has values for every theme, a table shows measured ratios for all required pairs with failures fixed or listed, colour is never the sole signal, and usage is documented.
