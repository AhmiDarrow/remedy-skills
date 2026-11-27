---
name: windows-component-repair
version: 1.0.0
description: >
  Repair Windows system file and component store corruption with DISM and SFC in the right order and read their logs. Use when updates fail, system features break or SFC reports unrepairable files.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - windows
  - repair
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: windows-component-repair
  official: true
  domain: ops
  security_flags: []
---

# Windows Component Repair

## When to use
Evidence points to damaged Windows components. Commands need an elevated terminal.

## Steps
1. Record the exact update or feature error code, Windows edition, version, build, architecture and language.
2. Check disk health and free space first, using `chkdsk C: /scan` and disk events. Repairing files on a failing drive is wasted effort.
3. Make sure important data is backed up and note pending reboots; restart if one is pending.
4. Run `DISM /Online /Cleanup-Image /ScanHealth`.
5. If corruption is repairable, run `DISM /Online /Cleanup-Image /RestoreHealth`.
6. Then run `sfc /scannow`, and rerun it after a reboot if it repaired anything.
7. If DISM cannot find source files, use official installation media matching build, edition and language: check indexes with `DISM /Get-WimInfo /WimFile:<path>`, then add `/Source:wim:<path>:<index> /LimitAccess` (use `esd:` for an install.esd).
8. For failures that remain, read `C:\Windows\Logs\DISM\dism.log` and `C:\Windows\Logs\CBS\CBS.log` around the run, searching for `[SR]` lines and the first error.
9. If still broken, offer an in-place repair install that keeps apps and files, after backup and with the user's approval.
10. Retry the original failing operation.

## Watch out for
- SFC before a damaged store is fixed has nothing good to repair from.
- `StartComponentCleanup /ResetBase` is cleanup, not repair, and prevents uninstalling existing updates.
- Never download individual DLLs from the web.
- A progress bar that pauses is not necessarily hung; do not power off during servicing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The health scan and SFC report no remaining violations and the originally failing operation succeeds, or the residual log error is reported.
