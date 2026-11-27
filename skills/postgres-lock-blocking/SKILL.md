---
name: postgres-lock-blocking
version: 1.0.0
description: >
  Trace PostgreSQL lock waits to the root blocking session and fix the transaction or migration pattern behind them. Use when queries hang, pile up behind a DDL change, or sit waiting on a lock.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - postgresql
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: postgres-lock-blocking
  official: true
  domain: backend
  security_flags: []
---

# Postgres Lock Blocking

## When to use
Statements that are normally fast are stuck right now, or lock waits recur at certain times.

## Steps
1. List waiters with their blockers: query `pg_stat_activity`, selecting `pid`, `state`, `wait_event_type`, `xact_start`, `query` and `pg_blocking_pids(pid)`.
2. Follow the chain to a session that blocks others but is not itself blocked. That root is the target, not the longest waiter.
3. Read its state. `idle in transaction` means the application opened a transaction and went away; its `query` column shows only the last statement, which may not be the one that took the lock.
4. Check `pg_locks` for the relation and lock mode involved.
5. To relieve it, prefer `pg_cancel_backend(pid)`; it cannot end an idle transaction, which needs `pg_terminate_backend(pid)`. Both discard work, so show the user the session and ask first.
6. Check for a queued DDL: an `ALTER TABLE` waiting for an exclusive lock behind a long read also blocks every later reader.
7. For migrations, set a short `lock_timeout`, retry, and split changes so exclusive locks are brief.
8. Fix the source: shorter transactions, no network calls inside them, a consistent update order, and `idle_in_transaction_session_timeout` for the application role.
9. Enable `log_lock_waits` to capture the next occurrence.

## Watch out for
- A killed application session may immediately be recreated by the same retrying job.
- Autovacuum running to prevent transaction id wraparound must not be repeatedly cancelled.
- Foreign key checks take row locks on parent rows, so blocking can involve a table the statement never names.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The root blocker and the code path that produced it are identified, and a reproduction or later monitoring shows the chain no longer forms.
