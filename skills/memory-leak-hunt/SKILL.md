---
name: memory-leak-hunt
version: 1.0.1
description: >
  Confirm that a long-running process is really leaking memory, find what retains it with comparative snapshots and verify the fix. Use when memory climbs until restarts or out-of-memory kills.
author: Remedy Official
license: Apache-2.0
tags:
  - perf
  - debug
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
  - jobs
metadata:
  source: library
  library_id: memory-leak-hunt
  official: true
  security_flags: []
---

# Memory Leak Hunt

## When to use
A service or app grows over time and you need the cause. Prefer reproducing outside production; ask before attaching to or dumping a live process.

## Steps
1. Plot process or container memory against traffic and uptime. Separate steady growth from warm-up, a bounded cache filling or one large spike.
2. Reproduce by repeating one operation in batches, with idle periods between, until growth per batch is measurable.
3. Compare runtime heap with total resident memory. Flat heap with growing RSS points to native allocations, buffers, thread stacks, mapped files or allocator fragmentation.
4. Take snapshots after warm-up, then after more batches, and diff them: Python `tracemalloc` or memray; Node heap snapshots plus `process.memoryUsage()` for external buffers; heaptrack, Valgrind or sanitizers for native code; other runtimes' heap profiler.
5. In the diff, follow retaining paths from the growing objects to their root. Where allocated and why still held are different questions.
6. Check unbounded maps and caches, listeners and timers never removed, queues faster inward than outward, per-request labels or keys, forgotten tasks and unclosed handles.
7. Fix ownership: close, unsubscribe, bound by size or add expiry, apply backpressure.
8. Rerun the same loop longer and compare growth per batch.

## Watch out for
- Memory not returned to the OS after objects are freed is not by itself a leak.
- A scheduled restart or higher limit only delays failure.
- A heap snapshot can pause the process, need substantial extra memory and contain secrets.
- Short tests miss slow growth.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The retaining path or allocation site is identified and the same workload levels off after the fix, with before-and-after figures; otherwise report what was ruled out.
