---
name: scroll-position-restoration
version: 1.0.0
description: >
  Restore scroll position and list state when users go Back in a single-page app, including lazy and infinite lists. Use when returning from a detail page jumps to the top.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - navigation
  - ux
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.scroll
  - computer.snapshot
metadata:
  source: library
  library_id: scroll-position-restoration
  official: true
  domain: frontend
  security_flags: []
---

# Scroll Position Restoration

## When to use
Users open an item from a long list, press Back and lose their place or their loaded pages.

## Steps
1. Check what the router already offers and whether code sets `history.scrollRestoration` or calls `scrollTo` on every route change.
2. Identify the scrolling element. Routers usually restore the window, not an inner overflow container.
3. Set the policy: new navigation starts at the top (or the hash target); Back and Forward restore; changes of filters within a page follow a stated rule.
4. Key saved state by history entry, not by pathname, so two visits to the same URL stay independent.
5. Make the content available before restoring: reuse cached data, including all previously loaded pages of an infinite list.
6. Prefer saving an anchor (first visible item id and its offset) over a pixel value, since content heights change.
7. With virtualization, save the item index and offset and restore through the virtualizer's own API; keep measured sizes too.
8. Restore once, after layout, and cancel if the user has already scrolled.
9. Test Back, Forward, reload, direct load, and a list whose items changed while away.

## Watch out for
- Restoring with a fixed timeout works on a fast machine and fails on slow ones.
- If the cache was discarded, refetching only page one makes the saved position unreachable.
- Moving focus to the top after Back undoes restoration for keyboard users; return focus to the link that was opened without extra scrolling (`preventScroll`).

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
From deep in the list, opening an item and pressing Back shows the same item at nearly the same place on both slow and fast connections, while fresh navigation starts at the top.
