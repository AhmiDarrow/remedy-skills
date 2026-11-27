---
name: incremental-load-design
version: 1.0.0
description: >
  Load only new and changed rows from a source using watermarks, overlap windows and idempotent merges. Use when full reloads are too slow or an incremental sync is missing records.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - pipelines
  - etl
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - edit
metadata:
  source: library
  library_id: incremental-load-design
  official: true
  domain: data
  security_flags: []
---

# Incremental Load Design

## When to use
A pipeline copies data on a schedule and should stop rereading everything.

## Steps
1. Study how the source changes: inserts only, updates, hard deletes, backdated edits.
2. Pick the change marker and test it. An `updated_at` is trustworthy only if every writer sets it, including bulk scripts; check triggers or find rows where it predates a known change.
3. Remember that timestamps and sequence ids are assigned before commit, so a long transaction can surface behind your watermark. Re-read an overlap window longer than the longest expected transaction.
4. Define the window as half-open `[low, high)` and fix `high` when the run starts, using the source's clock.
5. Load into a staging table, deduplicate on the business key keeping the latest version, then upsert into the target.
6. Apply an incoming row only if its version is not older than the stored one.
7. Advance the watermark only after the merge commits, in the same transaction if both live in one database.
8. For ties on the marker, page by (marker, primary key).
9. Handle deletes separately: tombstones, change data capture, or periodic key comparison.
10. Schedule a reconciliation of counts and checksums by period, and keep a way to reload any range.

## Watch out for
- Taking the next watermark from the pipeline host's clock loses rows under clock skew.
- Setting it to `now()` after an empty or failed extract silently skips data.
- A new source column with a backfill may not touch `updated_at`, so old rows never refresh.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Rerunning a window changes nothing, a late-committing row is still picked up, and reconciliation matches the source for a sample period.
