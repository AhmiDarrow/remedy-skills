---
name: screen-reader-test-pass
version: 1.0.0
description: >
  Run a hands-on screen reader test of a web flow with the right browser pairing, commands and issue reporting. Use when automated accessibility checks pass but real usability is unverified.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - accessibility
  - frontend
kind: native
status: discovered
tools:
  - read
  - edit
  - computer.navigate
  - computer.snapshot
  - todo
metadata:
  source: library
  library_id: screen-reader-test-pass
  official: true
  domain: testing
  security_flags: []
---

# Screen Reader Test Pass

## When to use
A key flow needs verification with assistive technology before release, or a user reports it is unusable with a screen reader.

## Steps
1. Pick two or three critical tasks and the pairings to cover, commonly NVDA with Firefox or Chrome on Windows and VoiceOver with Safari on macOS or iOS.
2. Say plainly that an accessibility tree snapshot or automated scan is not a screen reader test. If you cannot operate or hear one, give the user this script and record their observations.
3. Learn the quit and stop-speech keys first. In NVDA the speech viewer shows output as text.
4. Pass one, structure: list headings and landmarks, then links and form controls. Check one clear main heading, sensible levels and names that make sense out of context.
5. Pass two, task: complete each flow without looking, using Tab and reading keys. Note where you could not tell what something was, its state, or what just happened.
6. At each control check name, role, state and value. Check images, tables with header announcements, errors, loading and success messages.
7. Test both browse and focus modes; custom widgets often break in one.
8. Record each issue with pairing and versions, steps, heard output, expected output, severity and the element.
9. Fix causes in markup first, then rerun the failed tasks.

## Watch out for
- Adding `aria-label` to a generic `div` or `span` is unreliable and often ignored.
- An `aria-label` that differs from the visible text breaks voice control users.
- One pairing's quirk is not necessarily a page bug; confirm the markup before working around it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each chosen task has a pass or fail result per tested pairing from actual output, issues are logged reproducibly, and untested pairings are named.
