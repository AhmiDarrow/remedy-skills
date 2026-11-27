---
name: cache-stampede-protection
version: 1.0.0
description: >
  Prevent a popular cache key's expiry or a cold cache from flooding the backend, using coalescing, stale serving and jitter. Use when load spikes each time a hot entry expires or the cache restarts.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - caching
  - reliability
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: cache-stampede-protection
  official: true
  domain: backend
  security_flags: []
---

# Cache Stampede Protection

## When to use
Many concurrent requests miss the same key and all recompute it at once.

## Steps
1. Confirm from logs or metrics that database spikes line up with expiry, deploys, flushes or restarts. Identify the keys and their recompute cost.
2. Coalesce within a process so concurrent misses share one in-flight computation. Check for an existing single-flight helper.
3. If many instances still overwhelm the backend, add a short cross-instance lease per key; losers serve stale or wait briefly, then recheck the cache.
4. Store two times per entry: a soft expiry that triggers one background refresh and a hard expiry after which it must not be served.
5. Alternatively refresh early with a probability that rises as expiry approaches, scaled by recompute time.
6. Add random jitter to TTLs so keys written together do not expire together.
7. Cache "not found" results briefly so missing ids cannot hammer the database.
8. When recompute fails, serve stale within the hard limit and back off instead of retrying on every request.
9. For cold starts, warm the highest-traffic keys with bounded concurrency, or ramp traffic.
10. Load test by deleting the hot key under concurrency and counting backend calls.

## Watch out for
- A lease without expiry stays stuck if its holder crashes.
- Waiters that poll without limit exhaust request workers.
- Stale serving is unsafe for permissions, revocations and similar data; exclude those.
- Remove the shared in-flight entry after failure, or the error is cached forever.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Expiring the hottest key under load produces about one recompute (or one per instance by design), and a failing recompute does not multiply backend calls.
