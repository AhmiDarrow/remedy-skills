---
name: race-condition-hunt
version: 1.0.0
description: >
  Find and prove a race between threads, tasks or processes, then fix the ordering instead of adding sleeps. Use when results vary run to run or fail only under load or parallelism.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - debugging
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: race-condition-hunt
  official: true
  domain: testing
  security_flags: []
---

# Race Condition Hunt

## When to use
Occasional duplicates, lost updates, use-after-close errors or failures that disappear when you add logging.
## Steps
1. Identify the shared thing: variable, file, row, cache entry, socket. List every reader and writer and which execution context each runs in.
2. Look for check-then-act and read-modify-write with a gap: exists-then-create, load-increment-save, or an `await` between the check and the update.
3. Run the available detector: `go test -race`, `-fsanitize=thread` for C and C++, or the stress and interleaving tools of the language, such as loom for Rust.
4. Raise the odds: loop the test hundreds of times, use more workers than cores, and inject a deliberate delay inside the suspected window.
5. Force the bad interleaving deterministically with barriers, latches or controllable promises, so one test fails every time.
6. Fix by removing sharing, or making the step atomic (unique constraint, conditional update, exclusive file create, atomic operation), or locking the whole invariant rather than each field.
7. When using several locks, define a single acquisition order and avoid calling unknown code while holding one.
8. Run the forced test and the stress loop again, then remove the injected delay.
## Watch out for
- A sleep or retry that only makes the window rarer.
- In-process locks guarding data that several processes or servers modify.
- A silent detector run treated as proof; it only sees paths that executed.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A deterministic or high-rate test failed before the fix and passes after it, and the invariant is protected for every writer.
