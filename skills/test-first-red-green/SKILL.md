---
name: test-first-red-green
version: 1.0.0
description: >
  Build a behaviour test-first, watching each test fail for the right reason before writing the code. Use when the user asks for TDD or when logic is intricate enough to need a spec in executable form.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - tdd
  - workflow
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: test-first-red-green
  official: true
  domain: testing
  security_flags: []
---

# Test First Red Green

## When to use
The behaviour can be stated as examples before the implementation exists.
## Steps
1. Write a short list of behaviours as examples, from simplest to nastiest. This is a queue, not a batch of tests to write now.
2. Take one. Write a test through the public interface using a name that states the behaviour.
3. Run it and read the failure. It must fail because the behaviour is missing, not from a typo, import error or bad fixture. If it passes, find out why before going on.
4. Write the least code that passes without special-casing the test's exact values into the production path.
5. Run the whole fast suite, not only the new test.
6. With everything green, remove duplication and improve names. No new behaviour in this step.
7. Add examples that force generality when the current code is still a shortcut.
8. Add newly discovered cases to the list rather than handling them silently.
9. For bugs found along the way, start again at the failing test.
## Watch out for
- Writing many tests first, then debugging them all against one large implementation.
- Testing private methods or call sequences, which makes refactoring break tests.
- Editing the expected value to match the output without deciding which is correct.
- Reporting a test-first process when the tests were written afterwards.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each listed behaviour has a test that was observed failing before its code, the suite is green and a cleanup pass has been made.
