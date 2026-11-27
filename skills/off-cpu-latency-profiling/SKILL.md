---
name: off-cpu-latency-profiling
version: 1.0.0
description: >
  Find where a slow program waits rather than computes, such as locks, disk, network, DNS or scheduling. Use when requests are slow but CPU usage is low and CPU profiles show nothing.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - profiling
  - performance
  - latency
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: off-cpu-latency-profiling
  official: true
  domain: tooling
  security_flags: []
---

# Off Cpu Latency Profiling

## When to use
Wall-clock time is much larger than CPU time.
## Steps
1. Prove the gap: measure elapsed and CPU time for the slow operation, for example with `/usr/bin/time -v` or per-request timers.
2. Check the whole-machine suspects first: swapping, disk latency (`iostat -x`), CPU quota throttling in the cgroup's `cpu.stat`, and run queue pressure.
3. Take repeated stack snapshots during slowness with the runtime's dump tool. Frequently repeated wait frames are the lead.
4. Use a wall-clock profiler mode if the language has one, rather than a CPU-only sampler.
5. On Linux, trace system calls with timing: `strace -f -T -tt -p <pid>`, or `strace -c -w` for a wall-time summary. Tracing slows the process considerably; get approval before attaching to production.
6. Where eBPF tools are available, use off-CPU time and block I/O latency tools, which cost less. On Windows record a trace with wait analysis.
7. Break external calls into DNS, connect, TLS, first byte and transfer, using client instrumentation or `curl -w` timing variables.
8. Count calls per operation; many fast sequential round trips often explain more than one slow one.
9. Fix the largest wait and measure the same operation again.
## Watch out for
- Idle worker threads waiting for work dominate raw off-CPU graphs; filter to threads serving the slow operation.
- Syscall traces and packet data can contain secrets.
- Timeouts that are round numbers (5 s DNS retry, 30 s connect) point to a failing step, not general slowness.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Most of the elapsed time is accounted for by named waits with evidence, and the change reduces the measured total.
