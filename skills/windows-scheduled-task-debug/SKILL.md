---
name: windows-scheduled-task-debug
version: 1.0.0
description: >
  Fix Windows scheduled tasks that work by hand but fail or never run, checking account context, working folder, triggers and result codes. Use when a Task Scheduler job silently does nothing.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - windows
  - automation
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: windows-scheduled-task-debug
  official: true
  domain: ops
  security_flags: []
---

# Windows Scheduled Task Debug

## When to use
A task shows success with no effect, an error result, or no run at all.

## Steps
1. Read it with `Get-ScheduledTask` and `Get-ScheduledTaskInfo`: action, arguments, start-in folder, principal, run level, triggers, settings, last and next run, last result.
2. Check history in the `Microsoft-Windows-TaskScheduler/Operational` log, enabling it first if off.
3. Interpret common results: `0` success, `0x41301` running, `0x41303` not yet run. Other values are often the program's own exit code.
4. If it never fires, check trigger time and expiry, conditions such as AC power or idle, wake settings, missed-start behaviour and multiple-instance policy.
5. Account for the context. Running without a logged-on user means no visible desktop, no mapped drive letters and possibly a different profile. Use UNC paths and confirm the account's rights.
6. Set program and arguments separately. For PowerShell, use the full executable path with `-NoProfile -File "C:\path\script.ps1"` and set the start-in folder without surrounding quotes.
7. Add logging inside the script: start, identity, working directory, errors, and exit non-zero on failure.
8. Reproduce under the same account, then start the task through the scheduler.
9. Wait for one real triggered run.

## Watch out for
- A script that swallows errors returns 0 and looks successful.
- The user enters any task account password; do not put it in scripts or command history.
- Running as SYSTEM to make it work grants far more than needed, and anyone able to edit the script gains SYSTEM.
- Network credentials are unavailable with some "do not store password" logon types.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A scheduled, not manual, run produces the expected output and exit code, and a forced failure is visible in the result and log.
