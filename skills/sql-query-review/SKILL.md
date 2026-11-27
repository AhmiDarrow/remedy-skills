---
name: sql-query-review
version: 1.0.1
description: >
  Review SQL or ORM code in a change for injection, wrong results, unsafe writes and scaling problems before it merges. Use when reviewing new or edited database queries.
author: Remedy Official
license: Apache-2.0
tags:
  - database
  - perf
  - security
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
metadata:
  source: library
  library_id: sql-query-review
  official: true
  security_flags: []
---

# Sql Query Review

## When to use
A diff adds or changes queries and you want them checked before production data meets them.

## Steps
1. Read the schema, constraints, indexes and expected row counts. Capture the SQL the ORM really emits.
2. Injection: all values bound as parameters. Table names, columns and sort direction cannot be bound, so map them from an allowlist. Check raw ORM fragments and IN lists built by joining strings.
3. Access: every query on owned data filters by the authenticated owner or tenant.
4. Results: check NULL behaviour (`NOT IN` with a NULL returns no rows), a WHERE condition that turns a LEFT JOIN into an inner join, joins that multiply rows before SUM or COUNT, inclusive date ranges on timestamps, and LIMIT without a unique ORDER BY.
5. Writes: UPDATE and DELETE scoped as intended, related changes in one transaction, read-then-write races replaced by constraints, atomic updates or locks, and large writes batched.
6. Scale: queries inside loops, unbounded result sets, deep OFFSET pagination, functions or implicit casts on filtered columns that defeat indexes, and wide selects on hot paths.
7. Verify doubtful ones on representative non-production data with the database's explain tool. Remember that variants such as EXPLAIN ANALYZE execute the statement, including writes.
8. Report each issue with location, a triggering case, impact and corrected query. Propose indexes only with the query they serve and their write cost.

## Watch out for
- A plan from a tiny development table says little about production.
- Adding DISTINCT usually hides a join error.
- Do not run unreviewed statements against production to test them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every changed query is checked for safety, correctness and scale, and findings are marked verified by execution or by reading only.
