---
name: desktop-ui-thread-freeze
version: 1.0.0
description: >
  Diagnose and fix desktop app freezes caused by blocking work on the UI thread, with progress and cancellation. Use when a window shows not responding or stutters during file or network tasks.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - desktop
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - jobs
metadata:
  source: library
  library_id: desktop-ui-thread-freeze
  official: true
  domain: frontend
  security_flags: []
---

# Desktop Ui Thread Freeze

## When to use
Clicking an action locks the window until it finishes, or the app hangs intermittently.

## Steps
1. Reproduce with a large or slow input and capture the UI thread's stack during the freeze using a debugger, sampling profiler or process dump. Repeat to confirm the same frame. Dumps hold process memory, including secrets, so keep them local and delete them afterwards.
2. Classify: file or network I/O, CPU work, waiting on a lock or synchronous result, synchronous inter-process call, or flooding the UI with updates.
3. Move the work off the UI thread with the toolkit's idiom: async I/O, worker thread or separate process. In Electron the main process must not block either.
4. Pass immutable data in and send results back through the dispatcher or message channel; touch widgets only on the UI thread.
5. Never block the UI thread waiting for async work (`.Result`, `.Wait()`, join, synchronous IPC), a classic deadlock.
6. Coalesce progress updates to a few per frame at most.
7. Add cancellation that stops the work, cleans partial files and covers window close.
8. Tag results with a request id so late ones do not overwrite newer state.
9. Disable only conflicting actions and show progress if the wait is noticeable.
10. Re-run with the same large input while moving and resizing the window.

## Watch out for
- Marking a function async does not move its synchronous or CPU work off the thread.
- Pumping the event loop manually inside a long task invites reentrancy bugs.
- Rendering thousands of rows at once freezes the UI even when loading was in the background.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
With the reproducing input the window keeps responding, cancel and close work mid-task, and the previous blocking frame no longer appears on the UI thread.
