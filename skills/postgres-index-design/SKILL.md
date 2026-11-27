---
name: postgres-index-design
version: 1.0.0
description: >
  Choose PostgreSQL index columns, order, type and partial or covering options from real query patterns, and create them safely. Use when adding, auditing or removing indexes.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - postgresql
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: postgres-index-design
  official: true
  domain: backend
  security_flags: []
---

# Postgres Index Design

## When to use
A table needs indexes for its queries, or has accumulated indexes that slow writes without helping reads.

## Steps
1. Collect the actual queries on the table from code and query statistics, with filter columns, operators, sort order, limit and frequency.
2. List existing indexes with `\d+ tablename` and usage from `pg_stat_user_indexes`.
3. For B-tree column order, put equality columns first, then the range or sort column. A range condition limits how well later columns narrow the scan.
4. Use a partial index when queries always filter a small subset (`WHERE status = 'pending'`); the query's condition must imply the index predicate.
5. Use an expression index when queries filter on an expression such as `lower(email)`.
6. Use `INCLUDE` for index-only scans only when the plan shows heap fetches matter; the visibility map must be current too.
7. Pick the type by operator: GIN for `jsonb` containment, arrays and full text; GiST for ranges and geometry; trigram (`pg_trgm`) for `LIKE '%term%'`; BRIN for huge tables physically ordered by the column.
8. Index the referencing side of foreign keys that are joined on or whose parents get deleted; PostgreSQL does not do it automatically.
9. On live tables use `CREATE INDEX CONCURRENTLY`, outside a transaction block. If it fails it leaves an invalid index to drop and retry.
10. Confirm with `EXPLAIN (ANALYZE, BUFFERS)` that the planner uses it and the query improved.

## Watch out for
- `idx_scan = 0` is not proof of uselessness: check when statistics were reset, replicas (which keep their own), and whether the index enforces uniqueness.
- Every added index costs writes and can prevent HOT updates when its columns change.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each new index is tied to a named query with a better measured plan, and any dropped index was verified unused on all nodes.
