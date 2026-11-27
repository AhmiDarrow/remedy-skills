---
name: kotlin-coroutine-cancellation-audit
version: 1.0.0
description: >
  Fix Kotlin coroutine cancellation and error propagation bugs in services and libraries. Use when cancelled work keeps running, one failure kills siblings, or errors disappear.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - kotlin
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
  library_id: kotlin-coroutine-cancellation-audit
  official: true
  domain: backend
  security_flags: []
---

# Kotlin Coroutine Cancellation Audit

## When to use
Server-side or shared Kotlin code using coroutines behaves wrongly on timeout, failure or shutdown. Mobile screen lifecycle is a separate concern.
## Steps
1. `grep` for `GlobalScope`, ad hoc `CoroutineScope(` and `runBlocking`. Each needs an owner that cancels it, or a replacement with `coroutineScope`.
2. Find `catch (e: Exception)`, `catch (e: Throwable)` and `runCatching` around suspending calls. They swallow `CancellationException`; rethrow it first or call `currentCoroutineContext().ensureActive()` after catching.
3. In CPU-bound loops add `ensureActive()` or `yield()`, since cancellation is cooperative.
4. Wrap blocking calls in `withContext(Dispatchers.IO)`; for interruptible Java calls use `runInterruptible`.
5. Choose structure by failure intent: `coroutineScope` cancels siblings on a child failure; `supervisorScope` isolates children and requires each to handle its own error.
6. Check every `async` is awaited. A `CoroutineExceptionHandler` does not handle exceptions held in a deferred.
7. Use `withTimeoutOrNull` for expected timeouts, and note `withTimeout` throws a cancellation subtype that broad handlers may mistake.
8. Put suspending cleanup in `finally` inside `withContext(NonCancellable)`, keeping it short and bounded.
9. Test with `kotlinx-coroutines-test` and `runTest`: cancel mid-operation and assert children stopped and resources closed.
## Watch out for
- Passing `SupervisorJob()` as an argument to `launch` breaks the parent link and does not supervise as expected.
- Thread-locals such as logging context do not follow coroutines across threads without a context element.
- Injected dispatchers make tests deterministic; hardcoded ones do not.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A cancellation test shows all child work ending promptly, and no handler can absorb a `CancellationException` without rethrowing.
