---
name: mutation-testing-pass
version: 1.0.0
description: >
  Use mutation testing to find code that tests execute but do not actually check. Use when coverage is high but bugs still slip through, or before trusting tests around critical logic.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - mutation-testing
  - quality
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - write
metadata:
  source: library
  library_id: mutation-testing-pass
  official: true
  domain: testing
  security_flags: []
---

# Mutation Testing Pass

## When to use
Coverage says lines ran. Mutation testing asks whether anything would notice if they were wrong.
## Steps
1. Make sure the suite passes reliably first; flaky tests produce false kills.
2. Pick a tool for the language, such as Stryker, mutmut, PIT or cargo-mutants, and follow the installed version's docs (mutmut has needed `fork`, meaning WSL on Windows).
3. Limit scope to a critical module or the files changed on this branch. Whole-repo runs can take hours.
4. Run it as a background job on a clean tree, as some tools modify sources in place; confirm the tree is clean afterwards.
5. Triage surviving mutants: a missing assertion, an untested boundary, dead code, or an equivalent mutant that cannot change behaviour.
6. For real gaps write a test about behaviour (the boundary value, the side effect), not one crafted to match the mutation.
7. For survivors in dead or redundant code, simplify the code.
8. Investigate timeouts separately; they may be real infinite loops or just slow tests.
9. Rerun the scoped set and record remaining survivors with reasons.
## Watch out for
- Chasing a 100 percent score through trivial logging and string mutants.
- Mutating code whose tests hit real services, which can cause real side effects.
- Reading uncovered mutants and surviving mutants as the same problem.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each surviving mutant in the chosen scope is killed by a meaningful test, removed with the code, or recorded as equivalent or accepted.
