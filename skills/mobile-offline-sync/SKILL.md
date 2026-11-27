---
name: mobile-offline-sync
version: 1.0.0
description: >
  Design offline-first sync for a mobile or web app with a local store, an operation outbox and conflict rules. Use when users must create or edit data with poor or no connectivity.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - mobile
  - sync
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: mobile-offline-sync
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Offline Sync

## When to use
Field, travel or note-style apps need to work offline without losing or duplicating data.

## Steps
1. List which data must be readable offline, which actions must be writable, expected offline duration and whether several people or devices edit the same records.
2. Make the local database the source the UI reads. Network results update it.
3. Record writes in a durable outbox in the same transaction as the local change, with client-generated ids and idempotency keys.
4. Replay in order per entity with backoff. Handle dependencies, such as a child created under a parent that has no server confirmation yet.
5. Classify failures: transient retries; auth pauses the queue until sign-in; permanent rejection is surfaced with the user's data kept for fixing.
6. Choose conflict rules per field or type: server versions to detect, then merge, last writer wins only where loss is acceptable, or ask the user. Do not rely on device clocks for ordering.
7. Pull changes by server cursor and propagate deletions as tombstones.
8. Show per-item pending and failed state plus last sync time.
9. Plan schema migrations that run with a non-empty outbox, and handle logout or account switch without sending one user's queue as another.
10. Test airplane mode mid-request, app kill, duplicate delivery, two-device edits and a long-offline client.

## Watch out for
- A reachability flag does not prove the server is reachable; rely on request results.
- Background execution is not guaranteed by either mobile platform, so also sync on foreground.
- Clearing local data on an auth error destroys unsynced work.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The listed failure tests end with both devices and the server agreeing, no duplicates or silent losses, and rejected operations visible to the user.
