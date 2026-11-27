---
name: pipeline-partition-backfill
version: 1.0.0
description: >
  Re-run a data pipeline over historical periods safely, with idempotent partition writes, validation and a rollback path. Use when fixing wrong history or backfilling a new column or table.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - pipelines
  - backfill
kind: native
status: discovered
tools:
  - read
  - bash
  - todo
  - write
metadata:
  source: library
  library_id: pipeline-partition-backfill
  official: true
  domain: data
  security_flags: []
---

# Pipeline Partition Backfill

## When to use
Past outputs of a batch pipeline must be recomputed because logic, inputs or schema changed.

## Steps
1. Define the date range, affected outputs and every downstream table, report, model and export that reads them.
2. Check the inputs for old periods still exist and have the same meaning; source retention or format changes may limit how far back you can go.
3. Find non-reproducible logic: `now()`, "latest" dimension lookups, external API calls, unpinned reference files. Pass the logical run date in as a parameter.
4. Make each run replace exactly its partition (overwrite, or delete and insert in one transaction). Plain append duplicates on retry.
5. Disable side effects such as emails, outbound syncs and alerts for backfill runs.
6. Snapshot the affected data, or write to a parallel location and swap.
7. Run one representative period. Compare row counts, key totals and a row-level diff against the old output, and explain each difference.
8. Show the user the comparison, cost estimate and downstream list before the full run.
9. Run in batches with bounded concurrency, respecting order where a period depends on the previous one, and record status per partition.
10. Rebuild downstream aggregates in dependency order and verify totals end to end.

## Watch out for
- Scheduled live runs can collide with the backfill on the same partition; coordinate or pause with approval.
- Applying today's business rules to old periods may restate published figures; confirm that is intended.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every partition in range is marked succeeded and validated, a rerun of one gives identical results, and downstream figures have been refreshed.
