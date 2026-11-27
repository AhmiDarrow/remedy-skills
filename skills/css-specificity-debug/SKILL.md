---
name: css-specificity-debug
version: 1.0.1
description: >
  Find why a CSS declaration is losing by walking the cascade from the winning rule, then fix it without escalating selectors. Use when a style does not apply or only works with !important.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - computer.snapshot
  - computer.screenshot
metadata:
  source: library
  library_id: css-specificity-debug
  official: true
  security_flags: []
---

# Css Specificity Debug

## When to use
One element ignores a style you expect, or it differs between builds or pages.

## Steps
1. Name the element, property, state and viewport. In developer tools, read the computed value and the rule that supplies it; ask the user for that panel if you cannot open it.
2. First confirm your rule is present at all. Missing from the styles list means unloaded file, selector mismatch, an invalid selector that drops the whole rule, a purge step, or a failing media or container query. A struck-through or warned declaration may be losing or invalid.
3. If it applies but does nothing, check whether the property works here (for example width on an inline element) or a shorthand later resets it.
4. Compare competitors in cascade order: origin and importance, then cascade layer, then specificity, then `@scope` proximity, then source order. Inline styles beat normal author rules; running animations override normal declarations.
5. Remember the layer traps: unlayered normal styles beat layered ones, and with `!important` the layer order reverses.
6. Compute specificity as (ids, classes/attributes/pseudo-classes, elements/pseudo-elements). `:where()` adds nothing; `:is()`, `:not()` and `:has()` take their most specific argument. For inherited values, any rule targeting the element directly wins.
7. If order differs between dev and production, inspect how the bundler concatenates files and when lazy chunks inject CSS.
8. Fix at the cause: correct the load or layer order, lower the competing selector, use a variant or variable the component exposes, or add one class matching the project convention.
9. Check the other states, themes and pages using both rules.

## Watch out for
- Adding ids or `!important` wins today and forces the next override higher.
- Deleting the competing rule without searching for other elements that rely on it.
- Scoped or module CSS adds attributes or hashed names that change what matches.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cascade step that decided the winner is named, the computed value is correct in affected states, and other uses of the changed rule were checked.
