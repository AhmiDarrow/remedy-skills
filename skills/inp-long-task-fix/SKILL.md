---
name: inp-long-task-fix
version: 1.0.0
description: >
  Fix sluggish clicks and typing by tracing Interaction to Next Paint delay and breaking up main-thread work. Use when a page feels frozen on input or INP is poor.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - performance
  - web-vitals
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
metadata:
  source: library
  library_id: inp-long-task-fix
  official: true
  domain: frontend
  security_flags: []
---

# Inp Long Task Fix

## When to use
Buttons respond late, typing lags, or field data shows INP above 200 ms at the 75th percentile.

## Steps
1. Find which interactions are slow from real-user attribution if available; otherwise exercise the main flows with CPU throttling of 4x or more.
2. Record a performance trace of one slow interaction and split it into input delay, event handler time and presentation delay.
3. Input delay means something else held the main thread: startup scripts, timers, third-party code, hydration. Defer, split or remove it.
4. Long handlers: paint the immediate feedback first, then yield before the rest. Use `scheduler.yield()` where supported with a `setTimeout` fallback; a resolved promise does not let the browser paint.
5. Chunk long loops by a time budget of a few tens of milliseconds, and cancel outdated work when a newer input arrives.
6. Move pure CPU work (parsing, filtering large sets, compression) into a web worker. Measure transfer cost, use transferable buffers, and keep DOM work on the main thread.
7. Presentation delay: reduce DOM size and the area restyled, stop reading layout after writing it inside loops, and use `content-visibility` for offscreen sections where suitable.
8. In component frameworks, profile what re-renders on that interaction and narrow it.

## Watch out for
- Debouncing a handler hides the lag in a trace while the visible response gets later.
- Testing on a fast development machine without throttling shows nothing.
- Yielding can let a second click start while the first is half done; guard shared state.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same interaction under the same throttling is traced again, feedback paints within the target, and no single task in it remains long without a stated reason.
