---
name: migration-data-backfill
version: 1.0.1
description: >
  Backfill or rewrite many rows in a live database in resumable batches without blocking users or overwriting new data. Use when a new column or format must be filled for existing records.
author: Remedy Official
license: Apache-2.0
tags:
  - database
  - ops
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - grep
metadata:
  source: library
  library_id: migration-data-backfill
  official: true
  security_flags: []
---

# Migration Data Backfill

## When to use
Existing rows in an application database must change while the application keeps running. Reprocessing analytics partitions is a different task.

## Steps
1. Identify the database and version, table size, write rate, indexes, triggers, cascades, replication and change-data consumers.
2. Make sure new writes are already correct: deploy dual writing or the new write path first, or the backfill never catches up.
3. Define the target as a query that counts rows still needing work, and a deterministic transformation. Preview samples including nulls and odd values.
4. Plan recovery: keep the old data, or save original values for affected keys, and verify a backup exists. State what cannot be reversed.
5. Walk the table by an indexed unique key (keyset ranges), not growing `OFFSET`. Commit each batch separately and persist the last key.
6. Make each update conditional so it is safe to repeat and cannot overwrite a newer value, using a predicate, version check or row lock.
7. Check the query plan, set lock and statement timeouts, and start with a small batch. Adjust to keep transactions short.
8. Throttle on live latency, lock waits, replication lag, log growth and storage; pause automatically at agreed limits. Provide a manual stop.
9. Rehearse on a realistic copy to estimate runtime. Present the script, dry-run counts and thresholds, and get approval before production.
10. Verify with the remaining-work count, invariants and sampled comparisons, rescanning for rows missed by concurrent inserts. Only then add constraints or switch reads, using the database's low-lock method where available.

## Watch out for
- One giant transaction creating long locks, bloat and a long rollback.
- ORM saves firing emails, hooks or timestamp changes for each row.
- Failed rows skipped past by the checkpoint and forgotten; record them.
- Dropping the old column in the same release.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No eligible rows remain or exceptions are listed, invariants pass, the job resumed correctly after a test interruption, and cleanup is scheduled separately.
