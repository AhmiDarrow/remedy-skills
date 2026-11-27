---
name: interaction-states
version: 1.0.1
description: >
  Specify and verify every state of interactive components, including combined states, keyboard behaviour and async transitions. Use when hover, focus, disabled, loading or error behaviour is missing or inconsistent.
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
  - grep
  - glob
metadata:
  source: library
  library_id: interaction-states
  official: true
  domain: design
  security_flags: []
---

# Interaction States

## When to use
Components are designed or built showing only their resting look.

## Steps
1. `glob` and `read` the components in scope and their styles. Record states that already exist and shared tokens for them.
2. For each component list interaction states (default, hover, focus-visible, pressed), persistent states (selected, checked, expanded, current, visited) and condition states (disabled, read-only, loading, error, success, empty) that actually apply.
3. Define combinations that occur, such as selected plus hover, error plus focus, checked plus disabled, and which visual wins.
4. Write the transitions: what triggers each, what the component accepts meanwhile and how it leaves, including async cancel, failure and stale responses.
5. Describe each state's appearance in tokens, plus cursor, text and icon changes. Use more than colour for meaning.
6. Keep focus visible with a clear indicator that is not removed or hidden behind sticky content. Hover content must also work with focus and touch.
7. Specify keys per component following native elements or the established ARIA pattern, and the matching attributes (`aria-expanded`, `aria-pressed`, `aria-invalid`, `aria-busy`).
8. Decide disabled versus alternatives. If people need to discover why, keep it focusable with `aria-disabled`, block the action in code and show the reason.
9. During loading, prevent duplicate submission, keep width stable and announce the outcome.
10. Produce a matrix and a story or test page that can force each state; check by mouse, keyboard and touch emulation.

## Watch out for
- `aria-disabled` alone does not stop clicks or submission.
- Hover styles sticking after a tap on touch screens.
- Removing the focused element or disabling it drops focus.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each component has a state matrix with triggers, appearance, keyboard behaviour and combinations, and each state is demonstrable or listed as not yet implemented or verified.
