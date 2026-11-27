---
name: sql-join-fanout-debug
version: 1.0.0
description: >
  Track down inflated totals and duplicate rows caused by joins at mismatched grain, then rewrite the query so figures reconcile. Use when a report's sums are too high or rows appear twice.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - sql
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: sql-join-fanout-debug
  official: true
  domain: data
  security_flags: []
---

# Sql Join Fanout Debug

## When to use
A query's revenue or count disagrees with the source table, or adding one join changed numbers it should not touch.

## Steps
1. Get the trusted figure from the base table alone: row count, distinct key count and the sum in question.
2. Write down what one row means in each joined table and the expected cardinality of each join.
3. Add joins back one at a time, recording row count, `COUNT(DISTINCT base_key)` and the sum after each. The step where they diverge is the fault.
4. On that table run `SELECT key, COUNT(*) ... GROUP BY key HAVING COUNT(*) > 1`, using the exact join columns.
5. Find out why: a missing join column (tenant, currency, version), history rows with validity ranges, genuine one-to-many, or bad duplicates.
6. Fix by cause: complete the join condition; pre-aggregate the many side to the base grain in a CTE; choose one row with a stated rule; or use `EXISTS` when the join only filters.
7. With two independent one-to-many children, aggregate each separately before joining.
8. Check lost rows too: an inner join, or a `WHERE` condition on the right table of a left join, drops unmatched records.
9. Add a test asserting uniqueness of the join key and equality with the base total.

## Watch out for
- `SELECT DISTINCT` hides fan-out and can also merge two genuinely separate rows with equal values.
- `SUM(DISTINCT amount)` discards distinct orders that happen to share an amount.
- NULL keys never match with `=`; decide how they should be counted.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The final sum and distinct count match the base table, or every difference is explained by a listed filter, and the key assumption is tested.
