---
name: cpp-linker-error-decode
version: 1.0.0
description: >
  Diagnose C and C++ linker errors such as undefined reference, unresolved external, duplicate symbol and missing shared libraries. Use when compilation succeeds but linking or loading fails.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - cpp
  - c
  - build
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: cpp-linker-error-decode
  official: true
  domain: tooling
  security_flags: []
---

# Cpp Linker Error Decode

## When to use
The compiler is happy and the linker or dynamic loader is not.
## Steps
1. Demangle the symbol (`c++filt`, or `undname` with MSVC) and read its full signature, including const, namespace and ABI tags.
2. Find where it should be defined, then check that object or library really defines it: `nm -C` for a `T` versus `U` entry, or `dumpbin /symbols` and `/exports`.
3. Print the actual link command from a verbose build. Confirm the object or library appears.
4. With static libraries on GNU-style linkers, order matters: a library must come after the objects that need it.
5. If signatures differ slightly, check for mismatched macros, calling conventions or language standard between declaring and defining code.
6. C functions called from C++ need `extern "C"` on the declaration.
7. Templates defined in a `.cpp` file need explicit instantiation there or the definition moved to the header. A declared but undefined static member or virtual function can produce a missing vtable error.
8. For duplicates, find definitions in headers lacking `inline`; for globals declare `extern` in the header and define once.
9. For load-time failures, use `ldd` or `readelf -d`, `otool -L`, or `dumpbin /dependents`, then fix rpath or deployment of the library.
## Watch out for
- Mixing Debug and Release or different runtime libraries on Windows causes confusing mismatches.
- Setting `LD_LIBRARY_PATH` globally is a debugging aid, not a deployment fix.
- Flags that allow multiple definitions silently pick one of two different implementations.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The binary links and starts on a clean machine or container, and the reason the symbol was missing or duplicated is stated.
