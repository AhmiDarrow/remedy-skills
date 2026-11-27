---
name: test-quality-review
version: 1.0.0
description: >
  Review tests in a change to confirm they would actually fail if the behaviour broke. Use when a pull request adds many tests or passes suspiciously easily.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - review
  - quality
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: test-quality-review
  official: true
  domain: testing
  security_flags: []
---

# Test Quality Review

## When to use
Green checks are about to be treated as evidence. Verify the evidence.
## Steps
1. Map each claimed behaviour to the test that covers it, then list behaviours with none.
2. Break the production code on purpose (invert a condition, return early) in a throwaway copy and run the tests. Survivors do not test that behaviour. Restore the code afterwards.
3. Check that assertions are specific: exact values and effects, not merely "no exception" or "not null".
4. Look for tautologies: expected values computed with the same logic as the code, or assertions on what a mock was told to return.
5. Count mocks. If the unit under test is mostly replaced, the test checks wiring only.
6. Confirm tests are really collected and run: check the runner's output for the count and names. Look for misnamed files and unawaited async assertions.
7. Check failure inputs and boundaries, not just the example from the ticket.
8. Look for dependence on time, order, network or machine state.
9. Read a failure message: would it tell the next person what broke?
## Watch out for
- Snapshot updates accepted wholesale, which bless whatever the code now does.
- Tests weakened in the same diff: loosened tolerances, removed assertions, new skips.
- High line coverage produced by tests that assert nothing.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each key behaviour has a test shown to fail when that behaviour is broken, and weak or missing ones are listed.
