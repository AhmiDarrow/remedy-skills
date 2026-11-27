---
name: java-thread-dump-analysis
version: 1.0.0
description: >
  Read JVM thread dumps to explain hangs, deadlocks, pool exhaustion and spinning CPU. Use when a Java service stops responding or one core stays pinned.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - java
  - jvm
  - debugging
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
metadata:
  source: library
  library_id: java-thread-dump-analysis
  official: true
  domain: backend
  security_flags: []
---

# Java Thread Dump Analysis

## When to use
A running JVM is stuck or unexpectedly busy and restarting would destroy the evidence.
## Steps
1. Before any restart, capture three dumps about ten seconds apart with `jcmd <pid> Thread.print -l > dumpN.txt` or `jstack -l <pid>`, run as the same user as the process.
2. If virtual threads are in use, also use `jcmd <pid> Thread.dump_to_file` (JDK 21+), since the classic dump does not list them all.
3. Search for the deadlock section the JVM prints. It covers monitors and many lock cycles but not logical deadlocks such as a pool task waiting on another task in the same full pool.
4. Group threads by identical stacks and count. Hundreds waiting at one frame is the bottleneck.
5. For BLOCKED threads, take the lock address in "waiting to lock" and find the thread showing "locked" with it. Follow until reaching a thread that is not blocked on a lock; see what it is doing.
6. For pool waits (database connection borrow, HTTP client lease), count holders and see where they sit, often an I/O call without a timeout.
7. Remember that RUNNABLE includes threads blocked in socket reads. To find real CPU users, list threads with `top -H -p <pid>` and match the thread ID converted to hex against `nid` (newer JDKs may print it in decimal).
8. Compare the three dumps: a thread in the same frame with no progress is stuck; changing frames mean slow but moving.
## Watch out for
- A single dump cannot distinguish stuck from momentarily there.
- Idle pool threads parked on a queue are normal and usually the largest group.
- Adding threads to an exhausted pool often just moves the pile-up to the database.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The blocking chain or hot thread is identified with stacks from at least two dumps, and the proposed fix removes that specific wait.
