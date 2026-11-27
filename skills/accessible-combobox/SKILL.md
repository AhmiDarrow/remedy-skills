---
name: accessible-combobox
version: 1.0.0
description: >
  Build an autocomplete or searchable select that works with keyboard, screen readers, touch and IME input. Use when a plain select is too long or a custom dropdown is inaccessible.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - forms
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.key
  - computer.snapshot
metadata:
  source: library
  library_id: accessible-combobox
  official: true
  domain: frontend
  security_flags: []
---

# Accessible Combobox

## When to use
Users must pick from many options by typing, such as countries, assignees or tags.

## Steps
1. Challenge the need: native `select` or radios serve short lists better. If a proven headless combobox is installed, configure it instead of writing one.
2. Decide the contract: must the value come from the list, may it be free text, can new items be created, single or multiple.
3. Put `role="combobox"` on the input with `aria-expanded`, `aria-controls` and `aria-autocomplete`; the popup is a `listbox` of `option` elements. Label the input visibly.
4. Keep DOM focus in the input and point `aria-activedescendant` at the highlighted option, scrolling it into view.
5. Down and Up move the highlight, Enter selects, Escape closes the popup and, per the pattern, may clear on a second press. Home, End and Left, Right keep editing the text.
6. On blur, apply the contract: revert unmatched text or keep it, consistently, and never silently select a different option.
7. Announce result counts, loading and no results through a polite status region present from the start.
8. Make option clicks work by preventing the input blur on pointer down.
9. For multi-select, give each chosen chip a named remove button.
10. Test desktop and mobile screen readers and a composition keyboard.

## Watch out for
- Closing the list on blur before the click registers makes options unselectable by mouse.
- Interactive controls inside an option are not reachable; options contain text, not buttons.
- Showing a label while submitting a stale id happens when the user edits the text after selecting.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Selection, correction, clearing and no-result paths work by keyboard and screen reader, and the submitted value always matches what the field displays.
