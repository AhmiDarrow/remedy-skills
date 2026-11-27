---
name: swift-retain-cycle-hunt
version: 1.0.0
description: >
  Find and break Swift memory leaks from strong reference cycles in closures, delegates, timers and tasks. Use when deinit never runs or object counts keep growing.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - swift
  - memory
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: swift-retain-cycle-hunt
  official: true
  domain: tooling
  security_flags: []
---

# Swift Retain Cycle Hunt

## When to use
Swift objects stay alive after they should be released, in command line, server or library code as well as apps.
## Steps
1. Confirm the leak with a test: create the object in a scope, keep only a `weak` reference, release the owner, and assert the weak reference becomes nil.
2. Use the memory graph debugger or leak instruments where available to see the incoming strong references.
3. Check stored closures that use `self`. If `self` owns the closure, capture `[weak self]` and handle nil.
4. Check delegate and parent back-references; declare them `weak`, which requires a class-bound protocol.
5. Check timers, notification observers and subscriptions. A repeating timer retains its target or block until invalidated, and `deinit` cannot be where you invalidate it if the cycle prevents `deinit`.
6. For stored subscription tokens, make sure the sink closure does not capture `self` strongly.
7. Check long-running `Task`s iterating an endless async sequence. A `guard let self` before the loop keeps the object alive for the whole loop; rebind inside each iteration and cancel the task from an explicit stop method.
8. Use `unowned` only when the captured object provably outlives the closure.
9. Re-run the weak reference test.
## Watch out for
- Non-escaping closures cannot form a lasting cycle; adding weak capture there is noise.
- A short one-shot task capturing `self` merely extends lifetime until it finishes.
- Singletons and caches holding references are retention, not cycles, and weak captures will not release them.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The weak reference test passes for each fixed object and fails if the fix is reverted.
