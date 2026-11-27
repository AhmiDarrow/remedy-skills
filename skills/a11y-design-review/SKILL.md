---
name: a11y-design-review
version: 1.0.1
description: >
  Review mockups, prototypes or specs for accessibility before code: contrast, focus order, target size, motion, structure and error states. Use when a design is about to be handed to developers.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - a11y
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: a11y-design-review
  official: true
  domain: design
  security_flags: []
---

# A11Y Design Review

## When to use
Screens exist as designs and fixing them is still cheap. For built UI, audit the code and test with assistive technology.

## Steps
1. Get the screens, every state (hover, focus, disabled, error, loading, empty), themes and the target standard. Default to WCAG 2.2 level AA and say so.
2. Compute contrast from actual color values: 4.5:1 for normal text, 3:1 for large text, 3:1 for the visuals needed to identify controls, their states and meaningful graphics. Check text over images at its worst spot, in each theme.
3. Find meaning carried only by color, position, shape or sound, and add text, icon or pattern.
4. Number the intended focus and reading order on each screen. Define where focus goes when dialogs, menus and new content open and close. Require a visible focus style.
5. Check targets: at least 24 by 24 CSS pixels or enough spacing under the AA rule (which has exceptions); recommend about 44 or more for touch.
6. Annotate heading levels, landmarks, accessible names for icon buttons and alternative text intent for images.
7. Check forms: persistent visible labels, format hints before entry, errors in text next to the field with how to fix them.
8. Provide alternatives for drag and complex gestures, controls for moving or auto-playing content, a reduced-motion version, and no more than three flashes per second.
9. Ask how layouts behave with text at 200% and at 320 CSS pixels width.
10. Report each finding with screen, element, problem, who is affected, fix and severity.

## Watch out for
- Placeholder text used as the only label vanishes on typing.
- Estimating contrast by eye, or ignoring opacity that changes the rendered color.
- Calling the product compliant: a design review cannot verify names, keyboard behaviour or screen reader output.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each screen and state has findings or an explicit pass with measured ratios, focus order is annotated, and items that need testing in code are listed.
