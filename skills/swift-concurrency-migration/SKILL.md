---
name: swift-concurrency-migration
version: 1.0.0
description: >
  Migrate Swift code to strict concurrency checking, fixing Sendable and actor isolation diagnostics properly. Use when enabling Swift 6 language mode or facing data race errors.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - swift
  - concurrency
  - upgrade
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: swift-concurrency-migration
  official: true
  domain: tooling
  security_flags: []
---

# Swift Concurrency Migration

## When to use
A package or app target is being moved to complete concurrency checking.
## Steps
1. Check the installed toolchain version, since diagnostics and defaults differ between releases.
2. Turn on complete checking in the current language mode first, so findings are warnings.
3. Migrate module by module from the leaves of the dependency graph.
4. Sort diagnostics by root: global mutable state, non-Sendable values crossing isolation, protocol conformance isolation, and callback APIs. Fix globals first.
5. For globals, prefer `let` of a Sendable type, then isolate to a global actor. Use `nonisolated(unsafe)` only where external synchronization exists and is documented.
6. Make value types Sendable. For mutable shared reference types, choose an actor, global actor isolation, or a final class guarded by a lock with `@unchecked Sendable` and a comment naming the lock.
7. Wrap completion handler APIs with checked continuations, resuming exactly once on every path, including errors and cancellation.
8. Review actor methods for reentrancy: state read before `await` may have changed after it. Re-check or cache the in-flight task.
9. Replace blocking semaphores that wait on async work; they can stall the cooperative pool.
10. Switch the language mode per target once warnings reach zero and run tests with Thread Sanitizer.
## Watch out for
- `@preconcurrency import` quiets a dependency's diagnostics without making it safe.
- Sprinkling main actor isolation moves heavy work onto the main thread.
- `Task.detached` drops actor context, priority and task-local values.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Migrated targets build in the new mode, and each unchecked or unsafe annotation has a written synchronization justification.
