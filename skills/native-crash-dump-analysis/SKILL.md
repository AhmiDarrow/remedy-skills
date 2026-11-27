---
name: native-crash-dump-analysis
version: 1.0.0
description: >
  Analyze a core dump or Windows minidump from a native program to find the faulting code and cause. Use when a C, C++ or other native binary crashes where no debugger was attached.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - cpp
  - crash
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
metadata:
  source: library
  library_id: native-crash-dump-analysis
  official: true
  domain: tooling
  security_flags: []
---

# Native Crash Dump Analysis

## When to use
You have, or can arrange to capture, a dump from a crash you cannot reproduce interactively.
## Steps
1. Make sure dumps are captured: on Linux check `ulimit -c` and `/proc/sys/kernel/core_pattern` (or `coredumpctl`); on Windows configure error reporting local dumps. Changing these settings needs approval.
2. Get the exact matching binary, shared libraries and symbols. Compare build IDs or PDB signatures; a rebuild from the same commit may not match.
3. Open with `gdb <exe> <core>`, `lldb -c <core> <exe>`, or a Windows debugger with the symbol path set and `!analyze -v`.
4. Record the signal or exception code and faulting address. Near zero suggests a null pointer plus field offset; an address near the stack limit with deep frames suggests stack overflow; a trap or abort suggests a failed assertion or heap check.
5. Dump all threads (`thread apply all bt`), not only the faulting one.
6. Walk up frames, inspecting arguments and object contents. In optimized builds treat locals with suspicion and confirm with disassembly and registers.
7. A crash inside `malloc` or `free` usually means earlier corruption; reproduce under a sanitizer or page heap.
8. Form one hypothesis that explains the address and values, then confirm with a test or added assertion.
## Watch out for
- Dumps contain process memory, including credentials and user data. Do not upload them or paste raw memory into reports.
- A stack without symbols or with `??` frames may be corrupt; do not infer from it.
- Keep release symbols archived per build or later dumps will be unreadable.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The report names the faulting frame, the bad value and how it got there, or states plainly which symbols or data are missing to determine it.
