---
name: sql-window-functions
version: 1.0.0
description: >
  Write correct window-function queries for ranking, latest-row-per-group, running totals and period comparisons. Use when SQL needs per-group calculations without collapsing rows.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - sql
  - analysis
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: sql-window-functions
  official: true
  domain: data
  security_flags: []
---

# Sql Window Functions

## When to use
The result needs each detail row plus a rank, previous value, running sum or share of its group.

## Steps
1. State the grain of the output and which columns define the partition and the order.
2. Check the ordering columns for ties, and add a unique tiebreaker when the result must be deterministic.
3. For one row per group, use `ROW_NUMBER()`, filtering in an outer query because window results cannot appear in `WHERE`. Use `RANK` or `DENSE_RANK` only when tied rows should all survive.
4. For running totals write the frame: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. The default with `ORDER BY` is a `RANGE` frame that includes all peers, so tied rows show the same total.
5. For moving averages, remember `ROWS` counts rows, not days. Join to a date spine first so missing days exist, or use an interval range frame if the engine supports it.
6. For previous-period values use `LAG`, after aggregating to one row per period.
7. With `LAST_VALUE`, set the frame to `UNBOUNDED FOLLOWING`, or it returns the current peer.
8. For shares, divide by `SUM(x) OVER (PARTITION BY ...)`, guard with `NULLIF(..., 0)` and avoid integer division.
9. Verify one partition by hand, choosing one with ties, a gap and a single row.

## Watch out for
- Filtering in `WHERE` happens before the window is computed, so a date filter removes the history `LAG` or a running total needs. Compute first, filter outside.
- Joining before windowing can duplicate rows and inflate every total.
- NULL ordering differs between databases; state `NULLS LAST` where supported.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A hand-checked partition matches the output, repeated runs give identical rows, and totals reconcile with a plain `GROUP BY`.
