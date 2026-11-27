---
name: debugger-breakpoint-session
version: 1.0.0
description: >
  Use a real debugger with breakpoints, watchpoints and post-mortem inspection instead of scattering print statements. Use when a bug depends on runtime state that is hard to see from logs.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - debugger
kind: native
status: discovered
tools:
  - bash
  - jobs
  - read
  - edit
metadata:
  source: library
  library_id: debugger-breakpoint-session
  official: true
  domain: tooling
  security_flags: []
---

# Debugger Breakpoint Session

## When to use
A value is wrong somewhere between two points, rebuilds are slow, or you need to see many variables at the moment of failure.
## Steps
1. Build with debug info and low optimisation; optimised builds reorder lines and hide variables.
2. Pick the launcher: `python -m pdb script.py` or `breakpoint()`, `node --inspect-brk`, `gdb --args` or `lldb --`, `dlv test`. A debugger waiting for input blocks a non-interactive shell, so use batch mode (`gdb -batch -ex run -ex bt --args ./app`) or ask the user to drive it.
3. For crashes, break where the error is raised: `catch throw` in gdb, or Python's post-mortem (`python -m pdb -c continue script.py`).
4. Use conditional breakpoints for the one bad iteration instead of stepping through thousands.
5. When memory or a variable changes unexpectedly, set a watchpoint (`watch expr` in gdb, `watchpoint set variable name` in lldb) and let it stop at the writer.
6. At each stop, write down expected against actual state before continuing. Walk up frames to find where they first diverge.
7. In threaded programs, dump all threads (`thread apply all bt`, `bt all` in lldb) rather than only the stopped one.
8. Turn the discovered condition into a test, then remove temporary breakpoints from source.
## Watch out for
- Breakpoints pausing a process that has timeouts or holds locks, creating new failures.
- Expressions evaluated in the debugger that have side effects.
- Attaching to a production process: it freezes the service. Ask first and prefer a dump.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
You have observed the first point where state differs from expectation and a test or assertion now covers it.
