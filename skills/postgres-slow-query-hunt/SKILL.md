---
name: postgres-slow-query-hunt
version: 1.0.0
description: >
  Rank a PostgreSQL workload by total cost with pg_stat_statements and slow-query logs to decide what to optimise first. Use when the whole database is slow and no single query is to blame yet.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - performance
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - grep
metadata:
  source: library
  library_id: postgres-slow-query-hunt
  official: true
  domain: backend
  security_flags: []
---

# Postgres Slow Query Hunt

## When to use
CPU or I/O is high, latency rose across features, or you want to spend tuning effort where it pays.

## Steps
1. Check that `pg_stat_statements` is available. It needs `shared_preload_libraries` (a restart, so ask the user) plus `CREATE EXTENSION pg_stat_statements;`.
2. Note when statistics were last reset. For a bounded window, take two snapshots and subtract rather than resetting shared statistics.
3. Rank by total execution time (`total_exec_time` since version 13, `total_time` before; check the installed version).
4. Make separate rankings by calls, mean time, shared blocks read and temp blocks written. A 3 ms query called a million times can outweigh a 5 s report.
5. For each top entry record calls, mean, rows per call and the code that issues it (`grep` a distinctive table and column pair).
6. Classify: too many calls (cache, batch, fix N+1), too much work per call (index, rewrite), waiting (locks, I/O), or an unnecessary query.
7. For parameter-dependent outliers, set `log_min_duration_statement` or use `auto_explain` with a threshold to capture slow instances.
8. Sample `pg_stat_activity` wait events during the slow period to separate lock waits from execution cost.
9. Fix the largest item, then compare an equal-length window at similar traffic.

## Watch out for
- Normalized query text hides which parameter values were slow.
- Mean time hides a bimodal query; check `stddev_exec_time` and maximum.
- Logging every statement can fill disks and record personal data in literals.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
You have a ranked table with a cause for each top entry and a before-and-after measurement for the ones changed.
