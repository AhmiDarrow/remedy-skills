---
name: design-system-audit
version: 1.0.1
description: >
  Audit a product's UI code against its design system: component inventory with usage and missing states, hard-coded values, duplicates, one-offs and accessibility gaps. Use for UI kit inventory or drift review.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ui
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: design-system-audit
  official: true
  domain: design
  security_flags: []
---

# Design System Audit

## When to use
Screens have drifted from the system, or nobody knows what components exist and which states they cover. This is a read-only review with a report.

## Steps
1. Find the source of truth: component library, tokens, docs, design files the user can export. Record versions and what is officially deprecated. If none exists, say the audit is an inventory.
2. `glob` component files and `grep` imports to count real usage per component and per app area.
3. Search for bypasses: raw colours, pixel values, font settings, shadows and z-index values; native elements styled by hand where a system component exists; style overrides reaching into component internals.
4. Cluster look-alikes: different names with the same job, copied components, parallel versions.
5. For used components build a matrix of variants and states (default, hover, focus-visible, active, disabled, loading, error, selected, empty) marked present, missing or not applicable, with file evidence.
6. Check accessibility in code: semantics, names, keyboard support, focus visibility, token contrast. Mark what still needs testing in a running browser.
7. Classify each finding: product should adopt the system, system has a gap, legitimate exception, or dead code.
8. Compare documented components with code both ways.
9. Rank by user impact, spread and effort. Group fixes into batches, naming a lint rule or check that would stop each kind from returning.

## Watch out for
- Search counts include generated files, tests and vendored code unless excluded.
- Dynamic imports and class names built at runtime make a component look unused.
- A repeated one-off often means the system lacks something; forcing the nearest component can harm usability.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The report lists components with usage and state coverage, findings with file paths and a classification, a ranked fix list and what could not be verified statically, with no code changed.
