---
name: connection-pool-sizing
version: 1.0.0
description: >
  Size database or HTTP connection pools from measurements and fix exhaustion and leaks. Use when requests wait for a connection, the database reports too many clients, or latency spikes under load.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: connection-pool-sizing
  official: true
  domain: backend
  security_flags: []
---

# Connection Pool Sizing

## When to use
Errors like "pool timeout" or "too many connections" appear, or adding application instances made the database slower.

## Steps
1. Compute the real maximum: instances times processes per instance times pool maximum, plus workers, cron jobs, migration tools and admin sessions. Compare it with the server limit (`SHOW max_connections;` in PostgreSQL), leaving reserve.
2. Look at what connections are doing: in PostgreSQL, group `pg_stat_activity` by `state` and `application_name`. Many `idle in transaction` sessions point at code, not pool size.
3. Measure pool wait time, checked-out count and time each connection is held.
4. Fix long holds first: HTTP calls, file uploads or user think-time inside a transaction; lazy loading during response rendering.
5. Find leaks: every checkout must release on all paths, including errors and cancellation. Use context managers, `finally` or the framework's scoped helper.
6. Estimate need as throughput times average hold time, then add headroom. The database's CPU and disk set the ceiling; beyond it, more active connections add contention.
7. Set a checkout timeout so exhaustion fails visibly, and a maximum lifetime shorter than any firewall or proxy idle cut-off.
8. When many instances or short-lived functions are unavoidable, put a pooler such as PgBouncer in front. In transaction mode, check use of session state: `SET`, advisory locks, `LISTEN` and, depending on version and driver, prepared statements.
9. Load test before and after and compare wait time and throughput.

## Watch out for
- Pools created per request or per forked child before the fork cause churn or corrupted shared sockets.
- Autoscaling multiplies the pool maximum during exactly the incident that is already straining the database.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Worst-case connection count fits under the server limit with reserve, and a load test shows bounded pool wait with no leaked checkouts afterward.
