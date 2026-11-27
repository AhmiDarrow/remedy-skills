---
name: view-transitions-web
version: 1.0.0
description: >
  Add page and state transitions with the View Transitions API, with shared elements, fallbacks and motion preferences. Use when route or view changes should animate on the web.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - animation
  - css
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
metadata:
  source: library
  library_id: view-transitions-web
  official: true
  domain: frontend
  security_flags: []
---

# View Transitions Web

## When to use
Navigation or in-page view swaps feel abrupt and the target browsers include ones with view transition support.

## Steps
1. Check current support for the two forms separately: same-document (`document.startViewTransition`) and cross-document (`@view-transition { navigation: auto; }`, same origin). Make the change work without either.
2. Wrap updates in a helper that calls the update directly when the API is missing or reduced motion is requested.
3. Ensure the DOM is final when the update callback resolves. In React and similar frameworks flush synchronously (`flushSync`) or use the framework's integration.
4. Do slow data fetching before starting, because rendering is held while the callback runs.
5. Start with the default crossfade, then customise `::view-transition-old(...)` and `::view-transition-new(...)`.
6. For shared elements set the same `view-transition-name` on the source and destination. Names must be unique among rendered elements, so assign them just before the transition on the clicked item.
7. Fix aspect ratio changes by sizing the old and new pseudo-elements with `object-fit`.
8. Handle the promises (`ready`, `finished`) and rapid repeat navigation; a new transition skips the running one.
9. Test Back and Forward, slow network, scrolled positions and sticky headers.

## Watch out for
- A duplicate name causes the whole transition to be skipped.
- During the transition the page shows snapshots and does not respond to clicks, so keep durations short.
- Long or large sliding motion without a reduced-motion rule causes discomfort.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Supported browsers animate the specified elements in both directions without console errors, unsupported ones and reduced motion switch views correctly, and input is not blocked noticeably.
