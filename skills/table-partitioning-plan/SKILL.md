---
name: table-partitioning-plan
version: 1.0.0
description: >
  Decide whether partitioning helps a large table and plan the key, retention and online conversion. Use when a table of events or logs is too big to maintain, purge or vacuum comfortably.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - scaling
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - grep
metadata:
  source: library
  library_id: table-partitioning-plan
  official: true
  domain: backend
  security_flags: []
---

# Table Partitioning Plan

## When to use
A single table is large and growing, and deletes of old data or index maintenance have become painful.

## Steps
1. Measure size, growth per month and the predicates on the main queries. Partitioning helps mostly when queries filter on the partition key or old data is removed by whole ranges.
2. Rule out cheaper fixes: a better index, a BRIN index, archiving unused rows.
3. Choose the scheme: range by time for retention, list for a few stable categories, hash to spread load. Aim for a manageable partition count, not thousands of tiny ones.
4. Check constraint consequences. In PostgreSQL, a primary key or unique constraint must include the partition key; find code relying on global uniqueness of another column.
5. Check inbound foreign keys and ORM support for composite keys on the installed versions.
6. Automate creating future partitions ahead of time and alert when headroom runs low. Decide whether a default partition exists; rows landing there complicate adding the matching range later.
7. Implement retention by detaching and then dropping or archiving partitions; ask before destroying data.
8. Plan conversion: either attach the existing table as the first partition after adding a validated `CHECK` that matches its bounds, or create a new table, dual-write, backfill in batches and swap.
9. Rehearse on a copy, recording lock durations.
10. Verify pruning with `EXPLAIN` on the top queries.

## Watch out for
- A query without the key scans every partition and can be slower than before.
- Wrapping the key column in a function often prevents pruning.
- Time ranges need an explicit time zone; boundaries differ between UTC and local midnight.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Top queries show pruning in their plans, future partitions are created automatically, and the conversion was rehearsed with acceptable lock time.
