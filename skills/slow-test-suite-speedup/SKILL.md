---
name: slow-test-suite-speedup
version: 1.0.0
description: >
  Make a slow test suite faster by measuring where time goes and fixing the biggest costs without dropping coverage. Use when developers avoid running tests because they take too long.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - performance
  - ci
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
  library_id: slow-test-suite-speedup
  official: true
  domain: testing
  security_flags: []
---

# Slow Test Suite Speedup

## When to use
The suite has grown until feedback takes long enough that people push and hope.
## Steps
1. Record a baseline: total time, test count, pass count, and the split between install, build, collection, setup and test bodies.
2. List the slowest items (`pytest --durations=20`, or the runner's timing report).
3. Look for fixed sleeps and long timeouts; replace with waiting on a condition or a controllable clock.
4. Look for repeated expensive setup: fresh database migrations per test, app boot per file. Share what is immutable and isolate mutable state by transaction rollback, template copy or unique namespaces.
5. Find accidental network calls by running with network blocked in a safe test environment.
6. Check build settings and cache keys; a cold build may dominate everything else.
7. Parallelise only after fixing shared ports, files and records. Choose worker count from actual cores and memory.
8. Move truly slow end-to-end cases to a separate tier that still runs at a defined point.
9. Compare against the baseline, then run several times to check stability.
## Watch out for
- Speed gained because tests stopped being collected; the count must match.
- Retries added to hide failures introduced by parallelism.
- Optimising many tiny tests while one fixture takes most of the time.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Measured wall time is reduced against the baseline, the same tests run (or moves are listed), and repeated runs pass consistently.
