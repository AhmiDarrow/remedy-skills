---
name: postgres-explain-plan
version: 1.0.0
description: >
  Read a PostgreSQL EXPLAIN ANALYZE plan to locate where time and bad row estimates come from, then verify a fix. Use when one specific query is slow and you need to know why.
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
  - edit
metadata:
  source: library
  library_id: postgres-explain-plan
  official: true
  domain: backend
  security_flags: []
---

# Postgres Explain Plan

## When to use
You have a particular statement and parameters, and need to explain its plan instead of guessing at indexes.

## Steps
1. Use the real parameter values, including the slow tenant or date range, on data of realistic size.
2. Run `EXPLAIN (ANALYZE, BUFFERS) <query>;` in `psql`. ANALYZE executes the statement: wrap writes in `BEGIN; ... ROLLBACK;`, and ask before running it on production. Rollback does not undo sequence advances or effects outside the database made by triggers and functions, and row locks are held while it runs.
3. Read from the most indented nodes outward. `actual time` and `rows` are per loop; multiply by `loops` for totals.
4. Find where time is added by subtracting children's time from each parent. Treat parallel plans with care, since per-worker figures are averaged.
5. Compare estimated with actual rows. The lowest node that is off by 10 times or more usually explains bad choices above it.
6. For bad estimates, run `ANALYZE tablename`, check skew in `pg_stats`, raise the column statistics target, or use `CREATE STATISTICS` for correlated columns.
7. Match symptoms: large `Rows Removed by Filter` suggests a missing or poorly ordered index; a nested loop with huge `loops` suggests underestimation; `Sort Method: external merge` or many hash batches mean the operation spilled past `work_mem`.
8. Compare `shared hit` with `read`; a second run may be fast only because data is cached.
9. Change one thing, rerun the same command, and keep both plans.

## Watch out for
- A sequential scan is correct for small tables or when a large fraction of rows is needed.
- Setting `enable_seqscan = off` is a diagnostic, not a production fix.
- Prepared statements can switch to a generic plan that differs from what you get with literals.
- Raising `work_mem` globally multiplies across sorts and connections.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
You can name the node that caused the cost, and before and after plans on the same data show the improvement.
