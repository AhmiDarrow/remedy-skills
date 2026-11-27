---
name: perf-profile-cpu
version: 1.0.1
description: >
  Capture and read a CPU profile to find where time is really spent, then verify an optimization with a second profile. Use when a program is CPU-bound or uses far more CPU than expected.
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
  - write
  - edit
metadata:
  source: library
  library_id: perf-profile-cpu
  official: true
  security_flags: []
---

# Perf Profile Cpu

## When to use
CPU is busy and you need evidence before changing code. If the program mostly waits with low CPU, profile off-CPU time instead.

## Steps
1. Define a repeatable workload and metric such as CPU seconds per request. Confirm CPU is the limit, per core, and note any container quota throttling.
2. Profile an optimised build with symbols. Use `perf record -g` on Linux, `py-spy record` for Python, `node --cpu-prof`, Go's pprof CPU profile, or the platform's profiler. Ask before attaching to production, and install tools only with approval.
3. Record steady state long enough for many samples, separately from startup unless startup is the problem.
4. Check quality: unknown frames or broken stacks need symbols, frame pointers, unwind settings or a runtime perf map.
5. Read both views. Self time shows functions burning CPU; inclusive time shows paths responsible. In a flame graph width is sample share and left-to-right order is not time.
6. For each hot path ask whether the work is needed, repeated, or done at the wrong frequency, before tuning instructions. Consider GC, serialisation, regex, logging and lock spinning.
7. Estimate the best possible gain: removing a 5 percent frame saves at most about 5 percent.
8. Change one thing, run the same workload several times, and compare the metric and profile. Check results are still correct.

## Watch out for
- Instrumenting profilers distort small, frequent functions.
- Inlining can charge time to a caller.
- A narrower flame can be relative; compare absolute CPU per unit of work.
- Profiles may reveal internal paths and data; share carefully.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The main cost is tied to named code from a saved profile, and any change shows a repeatable improvement on the same workload or is reported as no gain.
