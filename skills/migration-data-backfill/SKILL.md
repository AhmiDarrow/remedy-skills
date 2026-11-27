---
name: migration-data-backfill
version: 1.0.1
description: >
  Plan batched data backfills that won't lock production tables.
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
metadata:
  source: library
  library_id: migration-data-backfill
  official: true
  security_flags: []
---

# Migration Data Backfill

## Steps
1. Estimate row counts.
2. Batch updates with sleeps/checkpoints.
3. Idempotent backfill script.
4. Progress metrics.
5. Verify counts; schedule during low traffic if needed.

## Operating rules
- Prefer **read-only** exploration before edits.
- Show commands run and their outcomes.
- Ask before destructive git, production changes, or secret access.
- Never commit or print live secrets.
- Stop with a clear blocker list if environment tools are missing.

## Done when
The user's goal is met **or** you report exactly what remains blocked and why.
