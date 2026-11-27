---
name: characterization-tests-legacy
version: 1.0.0
description: >
  Pin down what untested legacy code currently does with tests before changing it. Use when you must modify code that has no tests and whose intended behaviour is unclear.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - refactoring
  - legacy
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: characterization-tests-legacy
  official: true
  domain: testing
  security_flags: []
---

# Characterization Tests Legacy

## When to use
You cannot safely refactor what you cannot detect changing. These tests record behaviour, right or wrong.
## Steps
1. Mark the smallest public surface that covers the code you will change.
2. List its outputs, including side effects: files, queries, calls, printed text.
3. Neutralise nondeterminism at the edges (clock, random, network) with the least invasive change available, such as a parameter with the old value as default.
4. Call the code with varied inputs. Write an assertion you expect to fail, run it, and copy the actual result into the test.
5. For large outputs, save approved output files and compare, after scrubbing timestamps and ids.
6. Use branch coverage on the target to find paths not yet exercised and add inputs that reach them.
7. Name tests by observed behaviour. Mark surprising results with a comment such as "current behaviour, possibly a bug".
8. Sanity check the net: introduce a small deliberate change and confirm a test fails, then revert it.
9. Refactor in small steps with the tests green. Fix suspected bugs separately, each updating its test on purpose.
## Watch out for
- Correcting a bug while writing the tests, so the baseline no longer matches production.
- Running legacy code against real services or data to capture output; use copies.
- Approved files so large nobody can tell whether a change in them matters.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The branches you will touch are exercised, a deliberate mutation is caught, and the tests pass on the unmodified code.
