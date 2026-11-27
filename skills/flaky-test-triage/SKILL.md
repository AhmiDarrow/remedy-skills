---
name: flaky-test-triage
version: 1.0.1
description: >
  Reproduce a flaky test, classify the cause (order, time, shared state, async race, environment) and fix it with proof. Use when a test passes and fails on the same code.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - debug
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - grep
metadata:
  source: library
  library_id: flaky-test-triage
  official: true
  security_flags: []
---

# Flaky Test Triage

## When to use
A test is intermittent locally or in CI.

## Steps
1. Collect several failing logs with commit, runner, seed, order, parallelism and timing. Check that failures share one signature.
2. Run the test alone in a loop, then with its file, then the suite. Use the runner's repeat and shuffle options (such as `go test -count=100 -shuffle=on`, or installed repeat and random-order plugins).
3. Use the pattern to classify. Passes alone but fails in the suite: leaked state; bisect the preceding tests to find the polluter. Fails only in parallel: shared database, port, file or global. Fails under load: timing assumption. Fails at certain times: clock, timezone, month end. CI only: locale, case sensitivity, resources, network.
4. Force it: replay the order and seed, limit CPU or add workers, inject a temporary delay at the suspected point, or freeze the clock at the failing moment.
5. Fix the cause: reset what the test changes, allocate unique resources, await the specific completion signal, inject clock and randomness, compare unordered results without assuming order, fake external services.
6. If the race is in production code, fix and report it as a product bug.
7. Repeat the original reproduction enough times for the old failure rate to make a clean run meaningful, and record both counts.

## Watch out for
- Longer sleeps and automatic retries lower the frequency without removing the cause.
- A test that fails 1 in 100 needs hundreds of clean runs, not ten.
- Weakening the assertion until it cannot fail.
- If quarantine is unavoidable, give it an owner, issue and end date.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause is demonstrated by a reliable or forced reproduction and the fix survives it, or the test is visibly quarantined with the evidence so far.
