---
name: design-token-sync
version: 1.0.1
description: >
  Replace hard-coded colors, spacing, type and radii with the project's existing design tokens without unnoticed visual changes. Use when code has drifted from the theme or breaks in dark mode.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - design
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
  library_id: design-token-sync
  official: true
  security_flags: []
---

# Design Token Sync

## When to use
A token system exists but components still carry raw values. To design a new token model, treat that as a separate task.

## Steps
1. Find the real token source (CSS variables, utility theme config, theme modules, generated files) and edit sources, never generated output.
2. List tokens with their resolved value in each theme and their intended role.
3. `grep` for hex, `rgb`, `hsl`, `oklch`, named colors, pixel and rem values, shadows, font sizes and z-index, including inline styles, script style objects and SVG attributes. Exclude vendor and generated paths.
4. Classify each hit: exact match with the right role, near match, ambiguous, or intentional literal (brand logo, email markup, data visualisation, canvas drawing).
5. Map by purpose. Two tokens with the same light value may diverge in dark mode, so a border must use the border token even if a text token matches.
6. Report near matches as visible changes with old and new values and let the user or designer decide. Do not round silently.
7. Propose a new token only for a repeated value with a clear role, defined in every theme.
8. Change in small component groups. Compare screenshots of default, hover, focus, disabled and error states in each theme.
9. Run the build and tests. If the project has a style linter, add a rule against new raw values after agreement.

## Watch out for
- A misspelled CSS variable fails quietly and the property falls back to its initial or inherited value.
- Alpha variants may not work if a token stores a finished color instead of channels; check how the project does opacity.
- Replacing a value that was never a design choice, such as a 1px hairline offset, with a spacing token that may later scale.
- Creating a second parallel variable file.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Replaced values map to existing tokens by role, remaining literals are listed with reasons, intentional visual changes are approved, and themes were compared.
