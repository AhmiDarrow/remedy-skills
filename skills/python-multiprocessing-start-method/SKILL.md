---
name: python-multiprocessing-start-method
version: 1.0.0
description: >
  Fix Python multiprocessing code that hangs, crashes or respawns itself because of spawn, fork or forkserver differences. Use when parallel code works on one OS or version only.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - python
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: python-multiprocessing-start-method
  official: true
  domain: backend
  security_flags: []
---

# Python Multiprocessing Start Method

## When to use
A process pool works on Linux but fails on Windows or macOS, hangs after an interpreter upgrade, or raises serialization errors.
## Steps
1. Print `multiprocessing.get_start_method()` on both the working and failing machines. Windows and macOS default to spawn, and the Linux default changed away from fork in Python 3.14, so check the installed version.
2. Set the method explicitly with `ctx = multiprocessing.get_context("spawn")` and create pools from that context, so behavior matches everywhere. Do not call `set_start_method` from library code.
3. Put process creation behind `if __name__ == "__main__":`. Under spawn the child re-imports the main module, and unguarded code runs again.
4. Make worker targets module-level functions. Lambdas, nested functions and objects holding locks, sockets or open files cannot be serialized to a child.
5. Stop relying on inherited globals. Pass configuration as arguments, or build per-worker resources in the pool `initializer`.
6. If fork is in use and the parent has started threads, suspect a child deadlocked on a lock copied in the held state; move to spawn or forkserver.
7. When a pool hangs, check whether a worker was killed (out of memory, segfault). `ProcessPoolExecutor` raises `BrokenProcessPool`, which is easier to diagnose than a bare pool waiting.
8. With `Queue`, drain results before joining the producer; joining first can deadlock when the pipe buffer is full.
## Watch out for
- Spawn re-imports heavy modules in every worker, so startup cost can exceed the work. Raise `chunksize` or reuse the pool.
- Interactive sessions and notebooks cannot pickle functions defined in them; move workers into a file.
- Shared memory segments must be closed by each process and unlinked once, or they leak.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same test passes with the start method set to spawn, workers shut down cleanly, and no stray child processes remain.
