---
name: transaction-isolation-bugs
version: 1.0.0
description: >
  Find race conditions that come from isolation levels, such as lost updates and write skew, and fix them with locks, constraints or retries. Use when invariants break only under concurrent load.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: transaction-isolation-bugs
  official: true
  domain: backend
  security_flags: []
---

# Transaction Isolation Bugs

## When to use
Data occasionally violates a rule the code appears to check: overbooked slots, negative balances, two "primary" records.

## Steps
1. Write the invariant and `grep` every code path that writes rows affecting it.
2. Mark check-then-act sequences: a `SELECT` whose result decides a later write.
3. Confirm the real isolation level on the app's connection. PostgreSQL defaults to Read Committed; MySQL InnoDB to Repeatable Read, with different semantics. Do not assume the level names mean the same thing.
4. Identify the anomaly. Lost update: two read-modify-writes of one row. Write skew: two transactions read an overlapping set and update different rows. Phantom: a row appears that the check did not see.
5. Reproduce with two database sessions, stepping them by hand in the bad order.
6. Pick the narrowest fix: an atomic conditional `UPDATE`; a unique or exclusion constraint (PostgreSQL exclusion constraints suit overlapping bookings); `SELECT ... FOR UPDATE` on the rows or on a parent row that serializes the group; or Serializable isolation. When the read and write span separate HTTP requests, add a version column, update `WHERE id = ... AND version = ...`, check the affected row count, and expose it as `ETag` with `If-Match` (412 on mismatch); every other writer must bump the version.
7. With Serializable, retry the whole transaction on serialization failure (SQLSTATE `40001`), with a bounded loop, and keep external side effects outside it.
8. Turn the reproduction into an automated concurrency test using barriers rather than sleeps.

## Watch out for
- `FOR UPDATE` locks only rows returned; it cannot lock a row that does not exist yet.
- Raising isolation on one writer does not protect the invariant if others stay at a weaker level.
- A retry that reuses values read in the failed attempt repeats the bug.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The two-session sequence that broke the invariant now blocks, fails or retries correctly, and an automated test covers it.
