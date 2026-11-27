---
name: redis-memory-eviction
version: 1.0.0
description: >
  Investigate Redis memory growth, find large or non-expiring keys and set limits and eviction that match each use. Use when Redis hits out-of-memory errors or evicts data it should keep.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - caching
  - redis
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: redis-memory-eviction
  official: true
  domain: backend
  security_flags: []
---

# Redis Memory Eviction

## When to use
Memory climbs, writes fail with OOM errors, latency spikes, or sessions and jobs disappear unexpectedly.

## Steps
1. Read `INFO memory` and `INFO stats`: used memory, resident size, fragmentation ratio, `evicted_keys`, `expired_keys`, hits and misses.
2. Check `maxmemory` and `maxmemory-policy` with `CONFIG GET`; managed services may restrict this and expose settings elsewhere.
3. Sample with `redis-cli --bigkeys` and, where the version has it, `--memkeys`; use `MEMORY USAGE <key>` on suspects. Iterate with `SCAN`, never `KEYS *` on a live server.
4. Group keys by prefix and check `TTL` on samples. A result of -1 means no expiry.
5. Map each prefix to its writer with `grep`, and label it cache (safe to lose) or state (sessions, queues, locks, counters).
6. Match policy to content. `noeviction` rejects writes; `allkeys-lru` or `allkeys-lfu` suits pure cache; `volatile-*` policies evict only keys with a TTL. Mixed cache and queue data belongs in separate instances.
7. Add TTLs in the same command as the write (`SET ... EX`), with jitter. Note that a later plain `SET` removes an existing TTL unless `KEEPTTL` is used.
8. Bound growing lists, sets and streams with trimming. Trimming discards entries, so for anything labelled state, confirm they are processed or expendable and get the user's approval first. Changing `maxmemory` or the policy on a live server also needs approval, since it can start evicting at once.
9. Delete large keys with `UNLINK`, after the user approves what will be removed.
10. Check client output buffers and replication memory if keys do not explain usage.

## Watch out for
- `MONITOR` and full scans add load to an already struggling server.
- Persistence forks can need substantial extra memory under heavy writes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each major prefix has an owner, bound and expiry rule, the policy matches the data, and memory stays below the limit over a full traffic cycle.
