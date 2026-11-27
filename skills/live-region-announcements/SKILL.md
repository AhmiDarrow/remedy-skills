---
name: live-region-announcements
version: 1.0.0
description: >
  Make toasts, validation results, loading states and other dynamic updates reach screen reader users reliably. Use when something changes on screen but nothing is announced, or it chatters.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - aria
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: live-region-announcements
  official: true
  domain: frontend
  security_flags: []
---

# Live Region Announcements

## When to use
Saved messages, search counts, chat arrivals or progress are visible only, or announcements flood the user.

## Steps
1. List dynamic changes and for each decide: move focus, announce, or stay silent. If the user must act on it, focus or a dialog is usually right, not a live region.
2. Use `role="status"` (polite) for results and confirmations, `role="alert"` only for urgent failures, `role="log"` for append-only feeds.
3. Render the region empty at load and change its text later. A region inserted together with its message is often not announced.
4. Provide one shared announcer utility, or use the existing one, rather than regions scattered per component.
5. Write short self-contained messages: `3 results`, `Upload failed: file is too large`.
6. For repeats of identical text, clear the region and set it again after a short delay.
7. Throttle progress to meaningful milestones and expose the continuous value through a `progressbar`.
8. Do not rely on timed toasts for important information or actions; keep them on screen long enough, pausable, and available somewhere persistent.
9. For field errors, associate text with `aria-describedby`, set `aria-invalid`, and on failed submit focus the first invalid field or an error summary.
10. Verify with at least one screen reader.

## Watch out for
- Hiding the region with `display: none` or `visibility: hidden` silences it; use a visually-hidden class.
- Marking a large re-rendering container as live reads out the whole thing.
- Assertive messages interrupt speech and can cut off each other.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each listed change is announced once, at the chosen urgency, as heard in a real screen reader, and silent items stay silent.
