---
name: design-token-architecture
version: 1.0.0
description: >
  Structure design tokens into raw, semantic and component layers with naming, theming and platform output rules. Use when setting up tokens or when hex values and one-off names have multiplied.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - design-system
  - tokens
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
  library_id: design-token-architecture
  official: true
  domain: design
  security_flags: []
---

# Design Token Architecture

## When to use
A design system needs a token model that survives new themes and platforms.

## Steps
1. `grep` styles and platform code for raw colors, sizes, radii, shadows, durations and font settings. Cluster near-duplicates and count use.
2. Create primitives from the clusters (the scales themselves), named by value family such as `blue-600` or `space-4`.
3. Create semantic tokens named by purpose and state, such as `color-text-muted` or `color-border-focus`, that reference primitives. Product code uses these.
4. Add component tokens only where a component must be themed independently of the semantic role.
5. Fix a naming grammar (category, role, variant, state) and write it down with examples.
6. Store one source in a machine-readable file, following the Design Tokens Community Group format if tooling supports it, and generate CSS variables and native resources from it with a build step.
7. Define themes and modes as alternative values for semantic tokens, and fail the build on missing values or broken references.
8. Check required foreground and background pairs for contrast in every theme automatically.
9. Migrate incrementally with a lint rule blocking new raw values.

## Watch out for
- Semantic names that encode appearance, such as `color-blue-button`, break on the first rebrand.
- A token for every component property creates thousands nobody can navigate.
- CSS variables resolve where they are declared: a variable defined on `:root` that references another will not pick up an override set lower in the tree.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Switching theme changes only semantic mappings, generated outputs come from the single source, the pair contrast check passes, and the lint rule rejects a new raw value.
