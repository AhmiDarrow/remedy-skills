---
name: ci-cache-tuning
version: 1.0.0
description: >
  Make CI dependency and build caches actually save time without serving stale results, using measured hit rates and correct keys. Use when pipelines are slow or caches rarely hit.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - ci
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
  library_id: ci-cache-tuning
  official: true
  domain: ops
  security_flags: []
---

# Ci Cache Tuning

## When to use
Jobs spend minutes downloading or recompiling, or a cache exists but nobody knows whether it helps.

## Steps
1. From several recent runs, note per step: duration, cache restore time, save time, hit or miss, and cache size.
2. Cache downloaded inputs first (the package manager's download store) rather than installed trees. Installed trees embed paths, OS and runtime versions.
3. Build each key from everything that invalidates the content: OS, architecture, toolchain version and a hash of the lockfile. Hash the lockfile, not the manifest with loose version ranges.
4. Add fallback prefix keys only where a partly stale cache is safe, such as a download store or a compiler cache that verifies its inputs.
5. Check scoping rules in your CI system: many let a branch read the default branch's cache but not a sibling's. Make the default branch populate the cache.
6. For container builds, order the Dockerfile so dependency manifests are copied and installed before the source, and configure a remote layer cache if runners are ephemeral.
7. Compare restore plus save time with the time of a cold step. Delete any cache that does not clearly win.
8. Change one cache at a time and compare medians across at least five runs.

## Watch out for
- Many cache actions never overwrite an existing key. A key without a lockfile hash freezes the first content forever.
- Total cache quotas evict old entries, so one oversized cache can make every other one miss.
- Caches written by untrusted pull requests must never be restored by jobs that publish or deploy.
- Never put credentials or config files containing tokens in a cached path.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Before and after median job times are recorded, hit rate is visible in logs, and changing the lockfile demonstrably produces a new cache.
