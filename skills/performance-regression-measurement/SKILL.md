---
name: performance-regression-measurement
version: 1.0.0
description: >
  Decide whether a code change really made a program slower and pin down the cause despite noisy measurements. Use when a release feels slower or a benchmark result moved.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - performance
  - profiling
  - benchmarking
kind: native
status: discovered
tools:
  - read
  - bash
  - jobs
  - grep
metadata:
  source: library
  library_id: performance-regression-measurement
  official: true
  domain: testing
  security_flags: []
---

# Performance Regression Measurement

## When to use
Comparing two builds where the difference may be smaller than run-to-run variation.
## Steps
1. State the metric and workload that matter and the smallest change worth acting on.
2. Build old and new with identical toolchain, flags and dependencies. Confirm both are release builds.
3. Run the old build against itself several times to learn the noise floor.
4. Reduce interference: same idle machine, mains power, fixed input data, and no parallel builds. Shared CI runners are poor judges of small differences.
5. Alternate A and B runs instead of all A then all B, so thermal or background drift affects both.
6. Collect enough samples and compare distributions with median and spread or the tool's significance test (`benchstat`, criterion, `hyperfine`).
7. If the difference exceeds noise, compare profiles of both under the same work and look at what changed in share and in call counts.
8. Bisect with an automated threshold script if the cause is unclear, rerunning ambiguous commits.
9. Confirm causation by reverting or fixing the suspect and watching the number return.
## Watch out for
- A faster result may come from doing less work; verify outputs are identical.
- Averages hide tail regressions; check high percentiles for latency.
- Code layout changes can shift microbenchmarks a few percent without real effect on the application.
- Dependency or data growth between releases can be the cause even when your code did not change.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The report shows sample counts, the noise floor and the measured difference, and says either which change caused it or that no significant difference was found.
