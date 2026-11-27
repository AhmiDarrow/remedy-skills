---
name: css-cascade-layers-adopt
version: 1.0.0
description: >
  Introduce CSS cascade layers to end specificity wars between resets, third-party styles, components and utilities. Use when a stylesheet depends on important flags and ever longer selectors.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - architecture
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: css-cascade-layers-adopt
  official: true
  domain: frontend
  security_flags: []
---

# Css Cascade Layers Adopt

## When to use
Overriding library styles requires `!important`, or the load order of CSS files silently decides how pages look.

## Steps
1. Map all style sources and how each enters the page: global files, vendor CSS, CSS modules, CSS-in-JS, utility framework. Check the browser support targets.
2. Capture screenshots of representative pages and states before changing anything.
3. Declare the order once, in the first CSS loaded, for example `@layer reset, vendor, base, components, utilities;`.
4. Put third-party CSS in its layer with `@import url(...) layer(vendor);` or the bundler's equivalent.
5. Know the rule that surprises people: for normal declarations, unlayered styles beat every layered one. So wrapping only your overrides in a layer makes them lose to unlayered legacy CSS. Layer the old and third-party styles first.
6. Know the second: with `!important` the order reverses, so an important declaration in an early layer beats one in a later layer, and layered important beats unlayered important.
7. Migrate one source at a time and compare screenshots after each.
8. Remove now-unneeded `!important` and selector padding in the layers migrated.
9. Document the order beside the declaration and add a lint rule if the project lints CSS.

## Watch out for
- A utility framework may already define layers; read its output and fit your names around it rather than redeclaring.
- Runtime-injected styles usually arrive unlayered and will win.
- A layer first mentioned before the order statement takes its position from that first mention.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The layer order is declared in one place, migrated pages match their baseline screenshots or differ only as intended, and component overrides work without raising specificity.
