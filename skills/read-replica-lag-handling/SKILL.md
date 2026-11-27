---
name: read-replica-lag-handling
version: 1.0.0
description: >
  Route reads to replicas without showing users stale results of their own writes, and handle replication lag. Use when adding read replicas or when saved data seems to vanish on refresh.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - scaling
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: read-replica-lag-handling
  official: true
  domain: backend
  security_flags: []
---

# Read Replica Lag Handling

## When to use
Reads are split from writes, and some flows now read data older than what was just committed.

## Steps
1. List read paths and classify each: must be current (auth, permissions, balances, anything read to decide a write), must show the user's own writes, or may lag.
2. Find how routing happens (ORM router, proxy, separate DSN) and how transactions are pinned. Everything inside a write transaction goes to the primary.
3. Measure lag. In PostgreSQL, compare positions in `pg_stat_replication` on the primary; on a replica, `now() - pg_last_xact_replay_timestamp()` also grows when the primary is merely idle.
4. Pick a read-your-writes method: send the session to the primary for a short window after a write; or save the commit LSN and use a replica only once `pg_last_wal_replay_lsn()` has passed it; or return the written object and update the client from that.
5. Carry the marker across requests (session or token), since the redirect after a save may hit another instance.
6. Give background jobs the same care: a job enqueued on commit can run before the replica has the row.
7. Take a replica out of rotation beyond a lag threshold, and make sure the primary can absorb the fallback.
8. Handle query cancellations caused by replay conflicts on long replica reads.
9. Test with an artificially delayed replica, for example by pausing replay with `pg_wal_replay_pause()` in a test environment.

## Watch out for
- Local development with one database hides every lag bug.
- Filling a cache from a lagging replica right after invalidation stores the old value until expiry.
- Read-then-update that reads from a replica can overwrite newer data.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
With replay paused, the critical and read-your-writes flows still show correct data, and lag has a metric and a routing threshold.
