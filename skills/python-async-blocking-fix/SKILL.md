---
name: python-async-blocking-fix
version: 1.0.0
description: >
  Find and remove blocking calls that stall a Python asyncio service. Use when async endpoints queue behind each other, heartbeats miss, or latency spikes while CPU looks idle.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - python
  - asyncio
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: python-async-blocking-fix
  official: true
  domain: backend
  security_flags: []
---

# Python Async Blocking Fix

## When to use
An asyncio program is slow or freezes under concurrency, and individual requests are fast when run alone.
## Steps
1. Reproduce with debug mode on: run with `PYTHONASYNCIODEBUG=1` or `asyncio.run(main(), debug=True)`. Set `loop.slow_callback_duration` to 0.05 so each callback that holds the loop longer than 50 ms is logged with its source.
2. `grep` inside `async def` bodies for the usual blockers: `time.sleep`, `requests.`, synchronous database drivers, `subprocess.run`, plain file reads of large files, `.result()` on a concurrent future, and heavy parsing or hashing.
3. Also follow the sync helpers called from coroutines. The blocker is often two frames below the `async def`.
4. For a live hung process, take a stack sample with `py-spy dump --pid <pid>` (if installed) and see which frame the event loop thread is sitting in.
5. Fix by kind: I/O with an async library available gets the async client; blocking I/O without one goes through `await asyncio.to_thread(fn, ...)` (3.9+); CPU-bound work goes to a `ProcessPoolExecutor` via `loop.run_in_executor`.
6. Bound the fan-out with an `asyncio.Semaphore`. The default thread pool is small, so hundreds of `to_thread` calls just queue there.
7. Keep a strong reference to every task you create, or use `asyncio.TaskGroup` (3.11+), so tasks are not garbage-collected mid-flight or fail silently.
8. Rerun the same concurrent load and compare p95 latency and the slow-callback log.
## Watch out for
- `to_thread` does not make pure Python CPU work faster on a GIL build; it only stops it from owning the loop thread, and it still competes for the interpreter.
- Cancelling an awaiting coroutine does not stop the thread it started. Give the blocking call its own timeout.
- A client object created in one event loop and reused in another fails in confusing ways; create it inside the running loop.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same concurrent load produces no slow-callback warnings above the threshold, and the before and after p95 numbers are written down.
