---
name: powershell-admin-script-safety
version: 1.0.0
description: >
  Write or review PowerShell administration scripts so bulk changes support WhatIf, stop on errors, check native exit codes and log targets. Use before running a script that modifies or deletes in bulk.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - windows
  - powershell
kind: native
status: discovered
tools:
  - read
  - edit
  - write
  - bash
metadata:
  source: library
  library_id: powershell-admin-script-safety
  official: true
  domain: ops
  security_flags: []
---

# Powershell Admin Script Safety

## When to use
A script touches many files, users, services or registry keys.

## Steps
1. Establish the target edition and version (Windows PowerShell 5.1 and PowerShell 7 differ in encoding, operators and module support) and whether elevation is needed.
2. Split selection from change: first return the exact target objects, review count and sample, then act on that list.
3. Add `[CmdletBinding(SupportsShouldProcess, ConfirmImpact='High')]` and wrap every change in `if ($PSCmdlet.ShouldProcess($target, $action))`.
4. Guard native programs and .NET method calls inside that block; they ignore `-WhatIf` on their own.
5. Set `$ErrorActionPreference = 'Stop'` and `Set-StrictMode -Version Latest`; use try/catch where continuing is intentional.
6. Check `$LASTEXITCODE` after native commands, remembering some tools such as robocopy use non-zero codes for success.
7. Use `-LiteralPath` for paths from data. Refuse empty variables and roots: resolve the full path and verify it sits under the expected base before recursive deletion.
8. Make it rerunnable: check current state first, and export old values for rollback.
9. Log each target and outcome. Run with `-WhatIf`, then on one item, then the rest after the owner approves.

## Watch out for
- An empty variable in a path such as `"$root\*"` can target the drive root.
- A single result may not behave like an array on older versions; wrap with `@()`.
- `-Filter` and wildcard `-Path` can match more than expected.
- `Set-ExecutionPolicy` changes do not make a script safe, and should not be loosened machine-wide to run it.
- Never build commands from input strings with `Invoke-Expression`.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The WhatIf run lists exactly the intended targets without changing anything, a single-item run is verified, and failures produce a non-zero exit and log entry.
