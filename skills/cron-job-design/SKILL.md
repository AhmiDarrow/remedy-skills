---
name: cron-job-design
version: 1.0.1
description: >
  Design a scheduled job that survives overlap, missed or double runs, time zone changes and silent failure. Use when adding a cron job, nightly task or periodic worker.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - ops
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: cron-job-design
  official: true
  security_flags: []
---

# Cron Job Design

## When to use
Work must run on a schedule without someone watching it.

## Steps
1. State what the job does, how fresh the result must be, its expected and worst-case duration, and the harm if it runs late, twice or never.
2. Pick the scheduler the project already uses and check its guarantees on missed, duplicate and concurrent runs.
3. Set the schedule and time zone explicitly. Prefer UTC for technical work. For local business time, specify behaviour at daylight saving changes, where a time can be skipped or repeated.
4. Check expression semantics. In standard cron, restricting both day-of-month and day-of-week runs when either matches. Some schedulers add a seconds field.
5. Select work from durable state (unprocessed rows or the last successful watermark), not "the previous hour from now", so a missed run is caught up. Pass the logical period as an argument.
6. Make repeats safe using unique keys, transactional markers or idempotency keys for external effects.
7. Prevent overlap across all instances with the scheduler's policy (a Kubernetes CronJob has `concurrencyPolicy`), a database lock or a lease with expiry and ownership check. A per-host file lock covers only one host. Decide whether to skip, queue or replace.
8. Set a deadline, batch with checkpoints, bound retries and handle termination.
9. Run with minimal permissions and an explicit environment, working directory and `PATH`.
10. Record start, finish, counts and exit status. Alert when no success arrives within the expected window, and document manual run, backfill and pause commands.

## Watch out for
- Alerting only on errors, so a job that never starts is silent.
- A lock lease expiring during a long run and letting a second copy write.
- Many jobs set at midnight overloading the same dependency.
- A catch-up releasing weeks of notifications at once.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests or a dry run show rerun and overlap are harmless, missed periods are recovered or deliberately skipped, and a missing success raises an alert.
