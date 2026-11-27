---
name: desktop-window-state-restore
version: 1.0.0
description: >
  Save and restore desktop window size, position and layout safely across restarts and monitor changes. Use when windows reopen off-screen, wrong sized or forget their layout.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - desktop
  - ux
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: desktop-window-state-restore
  official: true
  domain: frontend
  security_flags: []
---

# Desktop Window State Restore

## When to use
Users find the app invisible after undocking, or must rearrange windows and panes every launch.

## Steps
1. Check what the OS, toolkit or an installed plugin already restores.
2. List what to remember: normal bounds, maximised or fullscreen state, display, pane sizes, open documents.
3. Store the restored (non-maximised) bounds separately from the maximised flag, so un-maximising returns to a sensible size. Do not overwrite bounds while minimised.
4. Save on move and resize with debounce and again on close, writing atomically to the per-user config location.
5. On restore, intersect the saved rectangle with current monitor work areas. If too little of the title bar is reachable, move it onto the primary or nearest display and clamp the size.
6. Allow for negative coordinates and monitors with different scale, using the toolkit's logical or physical convention consistently.
7. Validate the stored file; on corruption or old schema use defaults.
8. Set a sensible minimum size and cascade additional windows instead of stacking exactly.
9. Respect platforms where applications cannot set position, such as many Wayland sessions; restore size and state there.
10. Test restore logic as a pure function with simulated monitor lists: removed, rearranged, smaller, rescaled.

## Watch out for
- Treating negative coordinates as invalid moves windows off a legitimate left-hand monitor.
- Showing the window before applying bounds makes it visibly jump.
- Reopening a document whose file moved must not block startup.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests with each simulated monitor change keep the window reachable, and a real restart restores size, state and layout; real multi-monitor behaviour not tried is reported.
