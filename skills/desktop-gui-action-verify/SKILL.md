---
name: desktop-gui-action-verify
version: 1.0.0
description: >
  Operate a desktop application step by step, checking the screen before and after each action. Use when a task can only be done through a graphical program's controls.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - desktop
  - automation
kind: native
status: discovered
tools:
  - computer.windows
  - computer.window
  - computer.snapshot
  - computer.click
  - computer.type
  - computer.key
  - computer.uia.action
  - computer.uia.read_text
metadata:
  source: library
  library_id: desktop-gui-action-verify
  official: true
  domain: tooling
  security_flags: []
---

# Desktop Gui Action Verify

## When to use
No file, command line or API route does the job and the GUI must be driven.

## Steps
1. Confirm that no safer non-GUI route exists. State the end state you intend to reach.
2. List windows, focus the right one and confirm the document or account name in its title or body.
3. Snapshot. Locate targets by accessible name and role; use coordinates only when no element is exposed, and take them from the current snapshot.
4. Prefer element actions and menu items over pixel clicks. Check that a shortcut means what you expect in this application and operating system.
5. Before typing, verify which field has focus.
6. Perform one state-changing action, then read the screen to confirm its effect before the next.
7. On any unexpected dialog, stop and read all of it. Do not dismiss it by reflex with Enter or Escape.
8. Pause for approval before overwrite, delete, send, purchase or permission prompts.
9. At the end, verify the outcome independently where possible, such as reading the saved file.

## Watch out for
- A notification or another window can steal focus mid-typing.
- Display scaling, window moves and loading delays invalidate old coordinates.
- Clicking again because nothing seemed to happen can run the action twice; wait and look first.
- Never type secrets, and never use the GUI to get around a restriction that blocks the direct route.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The intended end state is observed on screen or on disk, and any step that failed or stayed uncertain is reported.
