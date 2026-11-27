---
name: optimistic-ui-rollback
version: 1.0.0
description: >
  Add optimistic updates that feel instant and recover correctly when the server rejects, reorders or times out. Use when toggles, likes, renames or list edits wait on the network.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - state
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
  library_id: optimistic-ui-rollback
  official: true
  domain: frontend
  security_flags: []
---

# Optimistic Ui Rollback

## When to use
Small frequent actions feel sluggish, or an existing optimistic update leaves the screen disagreeing with the server.

## Steps
1. Check suitability: high success rate, easily reversible, result predictable on the client. Keep payments, deletions without undo and permission changes pessimistic.
2. Define the exact local patch, including derived places such as counters, filtered lists and detail views.
3. Before patching, cancel in-flight reads of the same data so an older response cannot overwrite the patch.
4. Prefer keeping pending operations separate and computing the view as server data plus pending operations. Rollback then means removing one operation, not restoring an old snapshot.
5. Give created items a temporary client id, send an idempotency key, and swap in the server id without changing the rendered row's key.
6. Serialise operations on the same entity so a toggle on then off cannot arrive reversed.
7. On failure, revert only that operation, say what did not happen, and offer retry while keeping the user's input.
8. After success reconcile with the returned object or refetch once the last pending operation finishes.
9. Test by injecting delay, errors and out-of-order responses.

## Watch out for
- Restoring a whole-list snapshot after one failure erases other changes made in between.
- A timeout does not mean the write failed; refetch or retry idempotently before claiming it did.
- Letting users act on an item that exists only locally produces requests with a temporary id.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
With forced failure and reversed response order, the final screen equals server state after refresh, each failure is reported, and no duplicate item is created.
