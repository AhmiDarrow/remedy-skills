---
name: keyboard-composite-widgets
version: 1.0.0
description: >
  Implement correct keyboard behaviour for tabs, menus, toolbars, trees and grids using roving focus. Use when custom widgets need arrow keys or every item is a separate Tab stop.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - keyboard
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - computer.navigate
  - computer.key
  - computer.snapshot
metadata:
  source: library
  library_id: keyboard-composite-widgets
  official: true
  domain: frontend
  security_flags: []
---

# Keyboard Composite Widgets

## When to use
A custom control works by mouse only, or has roles added without the behaviour those roles promise.

## Steps
1. First ask whether native elements or a plain list of links and buttons would do. Site navigation is not an ARIA `menu`.
2. Read the WAI-ARIA Authoring Practices pattern for the exact widget and write its key map as a table before coding.
3. Make the widget one Tab stop. With roving tabindex the active item has `tabindex="0"`, others `-1`, and arrow keys move both the value and real focus. Use `aria-activedescendant` only when focus must stay on a container or input.
4. Match arrows to orientation, and mirror horizontal ones in right-to-left.
5. Add Home, End, typeahead and wrap behaviour as the pattern specifies.
6. For tabs, choose automatic activation only if panels appear instantly; otherwise Enter or Space activates.
7. Keep state attributes true: `aria-selected`, `aria-expanded`, `aria-checked`, `aria-controls`.
8. Handle removal or disabling of the active item so one item always remains tabbable.
9. Call `preventDefault` only for keys the widget consumed.
10. Write interaction tests per row of the key table and check with a screen reader.

## Watch out for
- `role="menu"` switches many screen readers into a mode where users expect full menu keys; half an implementation is worse than none.
- Moving the visual highlight without focus or active descendant is silent to assistive technology.
- Removing focus outlines hides the position you just implemented.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every row of the key table passes, Tab enters and leaves the widget in one press each way, and focus is always visible.
