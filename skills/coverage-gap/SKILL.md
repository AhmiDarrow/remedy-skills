---
name: coverage-gap
version: 1.0.1
description: >
  Find the untested branches that matter in changed or high-risk code and add focused tests for them. Use when asked what a change leaves untested or to raise coverage usefully.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
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
  library_id: coverage-gap
  official: true
  security_flags: []
---

# Coverage Gap

## When to use
Tests exist, and you need to know which important behaviour they never run.

## Steps
1. Use the repository's coverage command and note its exclusions. Get branch coverage where supported: `coverage run --branch -m pytest`, `go test -coverprofile`, the JavaScript runner's coverage option, or `cargo llvm-cov` if installed.
2. Confirm the report includes files that no test imports; many setups omit them by default.
3. Intersect uncovered lines and branches with `git diff` against the merge base. A diff-coverage tool can do this.
4. Read each gap and state the behaviour at risk: error path, boundary, permission denial, money calculation, parser rejection, rollback or retry.
5. Rank by impact and likelihood. Skip trivial accessors and generated code, saying why. Note unreachable code as possible dead code.
6. Write tests through the public behaviour, with assertions on results, state and side effects that should not occur.
7. Check each new test can fail: break the guarded condition temporarily, see red, then restore it exactly.
8. Rerun targeted coverage and the full relevant suite, and report what remains uncovered.

## Watch out for
- An executed line need not be asserted; coverage shows what ran, not what was checked.
- Mocking the unit under test produces coverage with no evidence.
- Running a subset gives misleading totals.
- If a new test exposes a bug, report it rather than asserting the wrong behaviour.
- Raising thresholds or adding exclusions to turn a gate green is not closing a gap.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The top risks have tests shown to fail without the behaviour, and remaining important gaps are listed with reasons.
