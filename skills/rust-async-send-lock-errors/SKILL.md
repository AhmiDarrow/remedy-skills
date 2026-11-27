---
name: rust-async-send-lock-errors
version: 1.0.0
description: >
  Fix Rust async compile errors and stalls involving Send bounds, locks held across await, and blocking calls. Use when spawn says the future cannot be sent between threads.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - rust
  - async
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: rust-async-send-lock-errors
  official: true
  domain: backend
  security_flags: []
---

# Rust Async Send Lock Errors

## When to use
Code using an async runtime fails with "future cannot be sent between threads safely", or the service stalls under load.
## Steps
1. Read to the note saying which value is "used across an await" or "may be used later". It names the non-Send type and the await point.
2. Typical culprits are `std::sync::MutexGuard`, `Rc`, `RefCell` borrows, raw pointers, thread-local handles and a boxed `dyn Error` without `+ Send + Sync`.
3. End the value's life before the await by enclosing it in a block. A call to `drop` is not always enough for the compiler's analysis.
4. For short critical sections with no await inside, keep a standard mutex and release it before awaiting. Use the runtime's async mutex only when the guard must span an await.
5. If a resource needs exclusive async access from many tasks, give it to one owner task and talk to it over a channel.
6. Move blocking I/O and heavy computation to `spawn_blocking` or a dedicated thread pool.
7. In `select!`, check each branch is cancellation safe: a dropped future may lose partially read data. Check the method's documentation.
8. Keep the `JoinHandle` and handle its error; a panic in a spawned task is reported only there.
9. For stalls, use the runtime's console or tracing instrumentation to find tasks with long poll times.
## Watch out for
- Switching to a single-threaded runtime or `LocalSet` to avoid Send is a design change, not a fix.
- Holding an async lock across a slow network call serializes every caller.
- Dropping a join handle usually detaches the task; it keeps running.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The code compiles without unsafe Send implementations, and a concurrent test completes with a timeout guarding against deadlock.
