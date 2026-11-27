---
name: deadlock-debug
version: 1.0.1
description: >
  Diagnose a hung program by capturing every thread or task stack, building the wait-for cycle and fixing the cause. Use when a process stops making progress with little CPU activity.
author: Remedy Official
license: Apache-2.0
tags:
  - debug
  - concurrency
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: deadlock-debug
  official: true
  security_flags: []
---

# Deadlock Debug

## When to use
Requests or threads are stuck waiting. Capture evidence before restarting, and ask before pausing or signalling a production process.

## Steps
1. Confirm it is stuck, not slow or spinning: check CPU, progress counters and two stack captures some seconds apart.
2. Capture all stacks with the runtime's tool: `py-spy dump` for Python (add `--native` where supported), `gdb` or `lldb` all-thread backtraces for C, C++ and Rust, a process dump with a debugger on Windows, a thread dump for the JVM. For Go prefer the pprof goroutine endpoint with full stacks if enabled; sending SIGQUIT dumps stacks but terminates the process by default.
3. For async runtimes inspect pending tasks too; thread stacks may show only an idle event loop.
4. For each waiter record what it waits on and who holds it. Draw the edges until you find a cycle, or an owner that is stuck on something else.
5. Include non-lock waits: full or empty channels, joins, exhausted pools whose tasks wait for more pool work, blocking calls on the event loop, pipe buffers, database locks, and a callback made while holding a lock.
6. Look for lock leaks on error or cancel paths.
7. Fix the cycle: one global lock order, smaller critical sections, no I/O or unknown callbacks under a lock, separate pools, scoped release.
8. Force the old interleaving with barriers in a test that has a timeout, and run it against old and new code.

## Watch out for
- A timeout alone turns a hang into a failure and may leave half-done state.
- Debugger attachment can need privileges and stops the process while attached.
- Dumps contain memory with secrets; restrict and delete them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The wait chain is shown from captured evidence and the forced test passes after failing before, or missing evidence and how to capture it next time are recorded.
