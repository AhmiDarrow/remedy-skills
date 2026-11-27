---
name: node-event-loop-lag-diagnosis
version: 1.0.0
description: >
  Diagnose a Node.js server whose event loop stalls under load. Use when all requests slow down together, health checks time out, or timers fire late.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - nodejs
  - performance
  - profiling
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
  - jobs
metadata:
  source: library
  library_id: node-event-loop-lag-diagnosis
  official: true
  domain: backend
  security_flags: []
---

# Node Event Loop Lag Diagnosis

## When to use
Latency rises for unrelated endpoints at once, which points to the single main thread being held.
## Steps
1. Measure before guessing: use `perf_hooks.monitorEventLoopDelay()` and log the p99 delay periodically, alongside request latency.
2. Reproduce with a steady load tool against a local or staging instance, run in the background with `jobs`.
3. Capture a CPU profile during the stall using `node --cpu-prof` or the inspector, and open it in a profiler view. Look for wide self-time blocks.
4. Check the common holders: `JSON.parse` or `stringify` on multi-megabyte bodies, synchronous `fs` and crypto calls, catastrophic regular expressions, large sorts, and synchronous template rendering.
5. Separate thread pool starvation from loop blocking. If loop delay is low but file, DNS lookup or some crypto operations are slow, the libuv pool is saturated; consider `UV_THREADPOOL_SIZE` set before startup.
6. Check garbage collection with `--trace-gc`. Frequent long major collections suggest heap pressure rather than one slow function.
7. Fix at the source: stream or paginate large payloads, use async variants, move CPU work to `worker_threads`, and partition unavoidable loops with `setImmediate`.
8. Rerun identical load and compare p99 loop delay.
## Watch out for
- Splitting work with resolved promises does not yield to I/O; the microtask queue runs fully before the loop continues.
- Adding more cluster processes masks the stall and multiplies memory.
- Do not expose the inspector port on a reachable network interface; it grants code execution.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The blocking function or saturated resource is named from profile evidence, and p99 loop delay under the same load is lower by a measured amount.
