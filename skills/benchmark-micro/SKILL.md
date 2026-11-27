---
name: benchmark-micro
version: 1.0.1
description: >
  Write a trustworthy microbenchmark for a hot function, avoiding optimizer, warm-up and input-realism traps. Use when comparing implementations of code that profiling showed to matter.
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
metadata:
  source: library
  library_id: benchmark-micro
  official: true
  security_flags: []
---

# Benchmark Micro

## When to use
A specific small piece of code needs a repeatable before-and-after measurement. For noisy whole-program regressions use a broader measurement process.

## Steps
1. Confirm from a profile that the function takes enough time to matter, and state the question and smallest speed difference worth acting on.
2. Use the language's harness, already in the project if possible: Criterion for Rust, JMH for Java, BenchmarkDotNet for .NET, `go test -bench` with `-benchmem`, pyperf or pytest-benchmark for Python, Google Benchmark for C++.
3. Capture input sizes and shapes from the real workload without copying private data. Include small, typical and large, plus the hit/miss or sorted/random mix that matters.
4. Keep setup outside the timed region. If the function mutates input, give each call a fresh copy and account for that cost.
5. Stop the compiler deleting or precomputing work: consume results and hide constant inputs with the harness facility (`black_box`, JMH `Blackhole` and state fields, a sink in Go or the benchmark loop helper of newer versions).
6. Build with release optimisation, no debugger or coverage. Reduce background load and record hardware, runtime version and flags.
7. Run both versions several times, alternating where possible. Report median or harness estimate with spread, and allocations. For Go, compare repeated `-count` runs with `benchstat`.
8. Sanity check: doubling input should change time as expected. Verify both implementations return identical results in a normal test.

## Watch out for
- A sub-nanosecond result for real work usually means it was optimised away.
- Reusing one input can flatter caches and branch prediction.
- A hand-rolled timer loop in a JIT runtime mostly measures warm-up.
- A large microbenchmark win may be invisible end to end.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The benchmark runs from a documented command, results with spread are reported for both versions, and the claim is limited to the inputs and machine measured.
