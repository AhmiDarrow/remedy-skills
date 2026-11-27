---
name: distributed-lock-review
version: 1.0.0
description: >
  Check whether a distributed lock is needed and make it safe against expiry, pauses and crashes with fencing or constraints. Use when code takes a lock in a cache or database to stop duplicate work.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - concurrency
  - reliability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: distributed-lock-review
  official: true
  domain: backend
  security_flags: []
---

# Distributed Lock Review

## When to use
Several processes must not do the same thing at once, and the code uses a key with a TTL, a lock table or an advisory lock.

## Steps
1. State what breaks if two holders run at once. Wasted work tolerates a best-effort lock; corrupted data or double charges need a guarantee enforced by the resource.
2. Look for a lock-free guard first: a unique constraint, a conditional `UPDATE ... WHERE state = 'pending'`, `FOR UPDATE SKIP LOCKED` for claiming work, or an idempotency key.
3. If the protected data lives in one database, use its transaction or advisory locks. In PostgreSQL, prefer `pg_advisory_xact_lock`, which releases at transaction end; session locks misbehave behind transaction-mode poolers.
4. For a Redis-style lease, acquire with one atomic `SET key token NX PX ttl`, with a random token per holder.
5. Release and renew only if the stored token still matches, using a server-side script so check and delete are atomic.
6. Assume the lease can expire while the holder is paused or partitioned. For correctness, issue an increasing fencing token and have the written resource reject older ones.
7. Size the TTL from observed job duration, renew from a heartbeat, and stop work when renewal fails.
8. Decide what contenders do: skip, wait with a deadline, or queue.
9. Test by forcing expiry mid-job and starting a second holder.

## Watch out for
- A plain `DEL key` on release can remove the next holder's lock.
- Failover of an asynchronously replicated lock store can grant the same lock twice.
- A lock key that is too broad serializes unrelated tenants; too narrow protects nothing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The forced-expiry test shows the stale holder cannot corrupt data, or the lock was replaced by a constraint or atomic update that makes it unnecessary.
