---
name: load-test-plan
version: 1.0.1
description: >
  Plan and run a bounded load test with a realistic request mix, pass criteria and stop conditions. Use when checking whether an API or service will cope with expected or peak traffic.
author: Remedy Official
license: Apache-2.0
tags:
  - perf
  - testing
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - jobs
metadata:
  source: library
  library_id: load-test-plan
  official: true
  security_flags: []
---

# Load Test Plan

## When to use
You need evidence about throughput, latency or limits of a system you own or are authorised to load.

## Steps
1. State the question: meets expected peak, finds the breaking point, or survives a long soak. Set pass criteria for rate, p95 or p99 latency and error rate with the owner.
2. Get written or explicit approval for the target, window and maximum load. Prefer an isolated environment with production-like data volume. Stub or disable payments, email and third-party calls.
3. Build the mix from traffic evidence: endpoints, read/write ratio, payload sizes, user variety, think time and authentication.
4. Use an available tool such as k6, Locust, vegeta or hey, and verify its options. To model independent arrivals, use a fixed arrival rate; fixed virtual users slow their sending when the server slows and understate delay.
5. Validate with a tiny run that responses are correct, not fast errors.
6. Set automatic aborts where supported plus a manual stop: error rate, latency, resource saturation or any effect outside the target.
7. Ramp in steps and hold each. Watch client and server: percentiles, errors, achieved versus requested rate, CPU, memory, connection pools, queue depth and database load.
8. Report the last step that passed, the first that failed, the likely bottleneck with evidence, and environment differences. Clean test data.

## Watch out for
- A saturated load generator looks like a slow server; monitor it too.
- Reusing one ID or query measures the cache.
- Averages hide tail latency.
- Never load a shared or production system without permission.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Results are compared with the agreed criteria, the run is reproducible from the saved script, and limits of what it represents are stated.
