---
name: visual-hierarchy-pass
version: 1.0.1
description: >
  Rework one screen or page so attention follows the user's priorities, using order, grouping, size, weight, contrast and space. Use when everything competes or the main action is hard to spot.
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
  library_id: visual-hierarchy-pass
  official: true
  domain: design
  security_flags: []
---

# Visual Hierarchy Pass

## When to use
A specific layout feels busy or flat and people miss what matters.

## Steps
1. State the screen's user task and rank: the first thing to see, the primary action, supporting information, rarely needed items. Confirm if the ranking is a product decision.
2. `read` the markup and styles, and get a screenshot or ask for one. Without a rendered view, label findings as code-based.
3. Squint or blur test: note what stands out first, second and third, and compare with the ranking.
4. Subtract first: remove duplicates, move rare material behind disclosure, drop unnecessary borders, backgrounds and icons.
5. Group by proximity and alignment before adding boxes.
6. Quiet competitors before enlarging the winner: reduce secondary weight or colour while keeping text contrast compliant.
7. Use one primary button style per decision area; make secondary and tertiary actions visibly lower. Keep destructive actions distinct and away from the default.
8. Apply existing type and spacing tokens, changing as few variables as achieve the order.
9. Keep visual order matching DOM, heading and focus order.
10. Check with real long, short, empty and error content, narrow width and both themes if supported. Present before and after with the reason for each change.

## Watch out for
- Making everything important bold, which restores the competition.
- Fading secondary text below readable contrast.
- Hiding frequently used controls to look cleaner.
- Burying prices, consent choices or cancellation to push the preferred action.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The rendered order matches the agreed ranking (or the pending visual check is stated), changes use existing tokens, semantics and contrast hold, and each change has a recorded reason.
