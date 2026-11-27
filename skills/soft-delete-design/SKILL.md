---
name: soft-delete-design
version: 1.0.0
description: >
  Decide between soft delete, archive tables and hard delete, and make filtering, uniqueness, relations and purging consistent. Use when users need to restore records or a deleted_at column is leaking.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - modeling
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: soft-delete-design
  official: true
  domain: backend
  security_flags: []
---

# Soft Delete Design

## When to use
A requirement asks for undo or history of deleted records, or "deleted" items keep reappearing in lists, counts or logins.

## Steps
1. Ask what is actually needed: user undo for a window, an audit trail, or referential history. Each may be served differently.
2. Compare options: a `deleted_at` column, moving rows to an archive table, an event or history log, or hard delete with backups.
3. If using `deleted_at`, `grep` every read path: ORM queries, raw SQL, reports, exports, search index, caches, background jobs.
4. Centralize the filter with a view, row-level policy or ORM default scope, and make including deleted rows explicit.
5. Replace plain unique constraints with partial unique indexes (`WHERE deleted_at IS NULL`) where a name may be reused, and decide what restore does on conflict.
6. Define the fate of children: deleted together with the same deletion batch id so restore brings back exactly those, or blocked, or left.
7. Update search indexes, caches and external copies on delete and restore.
8. Set a retention period and a purge job that hard-deletes in dependency order. Privacy erasure requests may require real removal; have the user confirm the obligation with whoever handles it.
9. Test list, count, join, login, uniqueness reuse, restore and purge.

## Watch out for
- Joins filter the main table but forget the joined one, so deleted authors or items still show.
- ORM default scopes are commonly bypassed by raw queries and bulk operations.
- A soft-deleted user whose sessions or API keys stay valid can still act.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests prove deleted rows are invisible on every listed read path, restore works including conflicts, and purge removes expired rows.
