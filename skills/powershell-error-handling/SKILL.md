---
name: powershell-error-handling
version: 1.0.0
description: >
  Make PowerShell scripts fail loudly and correctly across cmdlets and native programs. Use when a script continues after errors, try/catch never fires, or CI reports false success.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - powershell
  - error-handling
  - windows
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: powershell-error-handling
  official: true
  domain: tooling
  security_flags: []
---

# Powershell Error Handling

## When to use
A PowerShell script's failures are ignored or its exit code is wrong. Run commands with `pwsh` or `powershell`, whichever production uses.
## Steps
1. Record `$PSVersionTable` on the machine that runs the script.
2. Set `$ErrorActionPreference = 'Stop'` at the top, or `-ErrorAction Stop` on specific calls. `try/catch` catches only terminating errors.
3. Add `Set-StrictMode -Version Latest` and fix the uninitialized variables and missing properties it reveals.
4. After each native executable, test `$LASTEXITCODE`. Native failures do not throw by default; newer PowerShell 7 releases have a preference variable for this, so verify the installed version.
5. Wrap that check in one small function, allowing known success codes (robocopy treats several nonzero codes as success).
6. In `catch`, record `$_.Exception.Message` and `$_.ScriptStackTrace`; rethrow with bare `throw` to preserve the original.
7. Put cleanup in `finally`.
8. Make the process exit code explicit: `exit 1` on failure. Check how the caller invokes the script, since `-File` and `-Command` report exit codes differently.
9. Test by forcing a cmdlet failure, a native failure and a thrown error, and read the code the caller receives.
## Watch out for
- `$?` reflects only the last statement and is easily overwritten.
- In Windows PowerShell 5.1, redirecting native stderr under Stop preference can raise errors for harmless progress output.
- An empty `catch {}` recreates the silent failure.
- `Write-Host` is not an error signal; use the error stream or throw.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each of the three forced failures stops the script and produces a nonzero exit code in the real caller.
