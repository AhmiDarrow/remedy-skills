---
name: cache-invalidation
version: 1.0.1
description: >
  Design cache keys and invalidation so writes show on time, hot keys do not stampede and one user never sees another's data. Use when adding a cache or when users see stale or wrong values.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - perf
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: cache-invalidation
  official: true
  security_flags: []
---

# Cache Invalidation

## When to use
A cache is being introduced, or stale or misattributed data has been traced to one.

## Steps
1. For each cached value write down what it is derived from and how stale it may be. "Seconds are fine" and "never after a permission change" need different designs; some data should not be cached.
2. List every layer: process memory, shared cache, ORM, CDN and browser. Reproduce a stale read and find which layer served it.
3. Build the key from everything that changes the result: tenant, viewer or permission scope, parameters, locale, flags and a schema version for the serialized shape.
4. `grep` all write paths to the source data, including admin tools, batch jobs, migrations and direct SQL. Each one must invalidate, or a TTL must bound its staleness.
5. Invalidate after the database commit. Delete the entry rather than writing a computed value into it from concurrent writers. If losing an invalidation matters, drive it from an outbox or change stream and retry.
6. Handle the race where a reader loads old data, the writer deletes the key, then the reader stores the old value: use versioned keys or a version check on set.
7. For values feeding many entries, bump a namespace or entity version instead of scanning for keys to delete.
8. Give every entry a TTL as a backstop, and document how operators flush one tenant or namespace without emptying everything. Stop stampedes on hot keys: jitter TTLs and let one request rebuild (single-flight or a short lock) while others wait or get a stale value, only where step 1 allows it.
9. Test update, delete, permission removal, failed transaction and the interleaving in step 6.

## Watch out for
- Reading from a lagging replica right after invalidation refills the cache with the old row.
- A missing tenant or user part in a key is a data leak, not just staleness.
- Wildcard key scans on a busy cache can stall it.
- A TTL alone is no answer for revoked access.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every cached value has a stated staleness limit, a complete list of invalidating writes, and tests showing updates and revocations appear within that limit.
