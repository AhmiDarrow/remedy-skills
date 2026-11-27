---
name: spa-route-focus
version: 1.0.0
description: >
  Fix focus, page titles and announcements on client-side navigation so single-page apps behave like real page changes. Use when screen reader users hear nothing after clicking a link.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - navigation
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
  library_id: spa-route-focus
  official: true
  domain: frontend
  security_flags: []
---

# Spa Route Focus

## When to use
After in-app navigation, focus stays on the old link or falls to the body and the tab title never changes.

## Steps
1. Check what the router or framework already does (some include a route announcer) so you do not announce twice.
2. Set a unique, specific `document.title` per route, most specific part first, updated when its data arrives.
3. Pick one focus strategy: move focus to the new page's main heading or main container, given `tabindex="-1"`. Alternatively announce the title through a persistent status region, but then check where Tab continues from.
4. Run it after the new content has rendered, not on the click, and wait out lazy chunks and loaders.
5. Skip it for the first load, for in-page changes such as filter parameters or tabs, and where a dialog manages its own focus.
6. On Back, prefer returning focus to the link that led away, when it still exists.
7. Keep a skip link that targets the main region and works after navigation.
8. Render real anchors with `href` for navigation so open in new tab and link semantics survive.
9. Tell users of slow transitions that loading is happening.
10. Walk three routes forward and back with keyboard and a screen reader.

## Watch out for
- Focusing an element that is still animating in or hidden silently fails.
- Triggering on any URL change steals focus while someone types in a search box that updates the query.
- Calling `focus()` without `preventScroll` can fight scroll restoration.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each route change updates the title, announces the new page once and leaves Tab continuing from the new content, while filter updates leave focus alone.
