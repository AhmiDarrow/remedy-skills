---
name: postgres-vacuum-bloat
version: 1.0.0
description: >
  Diagnose dead-tuple buildup and table bloat in PostgreSQL, find what holds vacuum back and tune autovacuum per table. Use when tables or indexes keep growing or scans slow down over time.
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
  - write
metadata:
  source: library
  library_id: postgres-vacuum-bloat
  official: true
  domain: backend
  security_flags: []
---

# Postgres Vacuum Bloat

## When to use
Disk use grows faster than the data, a heavily updated table gets slower, or monitoring warns about transaction id age.

## Steps
1. Read `pg_stat_user_tables`: `n_live_tup`, `n_dead_tup`, `last_autovacuum`, `last_autoanalyze`. These are estimates.
2. Measure real sizes with `pg_total_relation_size`, split into heap, indexes and TOAST. Use the `pgstattuple` extension for accurate bloat, remembering that it reads the relation.
3. Before tuning, find what pins old row versions: long-running or idle transactions (`backend_xmin` in `pg_stat_activity`), inactive replication slots (`pg_replication_slots`), forgotten prepared transactions (`pg_prepared_xacts`), and standbys with `hot_standby_feedback`.
4. Resolve the pin, asking before dropping a slot or ending sessions.
5. If vacuum runs but cannot keep up, lower `autovacuum_vacuum_scale_factor` for that table with `ALTER TABLE ... SET (...)`, and review the cost delay and limit settings and worker count.
6. Watch a run in `pg_stat_progress_vacuum` or with `VACUUM (VERBOSE)`.
7. Check wraparound headroom with `age(datfrozenxid)` per database and `age(relfrozenxid)` per table.
8. To return space to the OS, plan `REINDEX CONCURRENTLY` for indexes (version 12 and later) and an online repack tool such as `pg_repack` for tables. `VACUUM FULL` takes an exclusive lock for the whole rewrite.
9. Reduce churn: avoid updates that change nothing, and consider a lower `fillfactor` so more updates are HOT.

## Watch out for
- Plain vacuum makes space reusable but rarely shrinks files; unchanged size does not mean it failed.
- Disabling autovacuum to reduce I/O makes the later cost far larger.
- A rewrite needs free disk roughly the size of the new table and indexes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause of retention is identified and removed, dead tuples fall after vacuum, and size or transaction age stays stable over a normal load cycle.
