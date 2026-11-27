---
name: cpp-sanitizer-run-triage
version: 1.0.0
description: >
  Run AddressSanitizer, UBSan and ThreadSanitizer on C or C++ code and fix what they report. Use when crashes are intermittent, optimization changes behavior, or memory looks corrupted.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - cpp
  - c
  - memory-safety
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: cpp-sanitizer-run-triage
  official: true
  domain: testing
  security_flags: []
---

# Cpp Sanitizer Run Triage

## When to use
You suspect undefined behavior or memory errors in code you can rebuild.
## Steps
1. Create a separate build directory so instrumented and normal objects never mix.
2. Build with `-fsanitize=address,undefined -fno-omit-frame-pointer -g -O1` on both compile and link. MSVC supports `/fsanitize=address` with a narrower set.
3. ThreadSanitizer (`-fsanitize=thread`) needs its own build; it cannot be combined with ASan.
4. Run the tests and the failing scenario. Set `UBSAN_OPTIONS=print_stacktrace=1:halt_on_error=1` so UB fails the run.
5. Fix the first report before reading later ones. For ASan, read three stacks: the bad access, the free (if use-after-free) and the allocation. Make sure a symbolizer is available.
6. Classify root cause: lifetime (dangling view, iterator invalidation), bounds, uninitialized state, signed overflow, bad shift, alignment or invalid cast.
7. Uninitialized reads are not covered by ASan; use MemorySanitizer where all dependencies can be instrumented, or Valgrind.
8. Reduce each bug to a test that fails under the sanitizer, then fix.
9. Add sanitizer jobs to CI.
## Watch out for
- A clean run only covers executed paths; pair with fuzzing for parsers.
- Suppression files should name third-party symbols narrowly, with a reason, never your own broad directories.
- Sanitizer builds are for testing; do not ship them.
- Adding `volatile` or extra logging may hide the symptom while the bug stays.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The reproducer and test suite run clean under the relevant sanitizers, and each fix addresses the lifetime or bounds error shown in the report.
