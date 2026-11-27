---
name: windows-bsod-triage
version: 1.0.0
description: >
  Investigate Windows blue screens and sudden restarts using bug check codes, minidumps, event logs and one-change-at-a-time isolation. Use when a PC crashes, bluescreens or reboots by itself.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - windows
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - web.search
metadata:
  source: library
  library_id: windows-bsod-triage
  official: true
  domain: ops
  security_flags: []
---

# Windows Bsod Triage

## When to use
Repeated stop errors or unexplained restarts on a Windows machine.

## Steps
1. Build the crash list in PowerShell from the System log: bug check records and Kernel-Power event 41, with times and codes. Event 41 only says the last shutdown was unclean; a bug check code of zero suggests power loss, hard hang or a forced power-off.
2. Collect dumps from `C:\Windows\Minidump` and `C:\Windows\MEMORY.DMP` using an elevated copy into a working folder. If none exist, check dump settings and the page file.
3. Open dumps in WinDbg with Microsoft symbols and run `!analyze -v`. Compare several: code, faulting module and stack.
4. List recent drivers, updates, firmware and hardware changes around the first crash.
5. Look for hardware evidence: WHEA-Logger events, disk and controller errors, temperatures.
6. Different codes and random modules suggest memory, power or overclock: return CPU, memory (including XMP or EXPO profiles) and GPU to stock, then run an extended memory test.
7. A repeating third-party driver: update, roll back or remove it from the vendor's own source.
8. Use Driver Verifier only with a restore path ready: target suspect non-Microsoft drivers, and know that `verifier /reset` from Safe Mode or recovery undoes it. It can cause boot loops.
9. Change one thing, then run longer than the previous time between crashes.

## Watch out for
- The module named by the analysis may be the victim of corruption caused elsewhere.
- Cleanup tools can delete the dumps before you read them.
- Full memory dumps hold sensitive data; do not upload them publicly.
- Have the BitLocker recovery key available before firmware changes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A likely cause is supported by dump or log evidence, or hardware tests are recorded, and stability has been observed beyond the former crash interval.
