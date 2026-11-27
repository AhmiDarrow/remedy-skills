---
name: monorepo-task-runner
version: 1.0.1
description: >
  Fix a monorepo's task graph so builds and tests run in the right order, only where needed, with correct caching. Use when affected filtering misses packages or cached results are stale.
author: Remedy Official
license: Apache-2.0
tags:
  - monorepo
  - tooling
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - grep
  - glob
metadata:
  source: library
  library_id: monorepo-task-runner
  official: true
  security_flags: []
---

# Monorepo Task Runner

## When to use
A workspace uses Turborepo, Nx, pnpm filters or similar and its tasks are slow, misordered or wrong.

## Steps
1. Identify package manager, runner and versions. Configuration keys change between major versions (Turborepo renamed `pipeline` to `tasks`), so check docs for the installed one.
2. Inspect the project graph with the runner's graph or dry-run output. Compare it with real imports; every cross-package import needs a declared dependency.
3. Define task dependencies: which tasks need dependencies built first, which need only their own package, which can run in parallel. Remove cycles.
4. For each cached task declare all inputs: sources, shared config, lockfile, tool versions and environment variables that change results.
5. Declare all outputs, so a cache hit restores them. Do not cache deploys or tasks with external side effects, and treat persistent dev servers separately.
6. Set the affected base to the merge base or last successful main run, and fetch enough history in CI. Include dependents of changed packages, for example pnpm's `...[ref]` filter form.
7. Verify with experiments: clean run, repeat for cache hits, change a leaf, a shared package, a global config and a relevant variable, and check exactly the expected tasks rerun.
8. Document the developer and CI commands and how to bypass the cache.

## Watch out for
- A cache hit with missing outputs "succeeds" and breaks a later step.
- Secrets can end up in cached logs or artifacts; limit who may write a shared remote cache.
- Root files outside any package may not mark anything affected.
- Phantom dependencies work only because of hoisting.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each experiment reruns the expected tasks and no others, a cache hit produces usable outputs, and a clean uncached run passes.
