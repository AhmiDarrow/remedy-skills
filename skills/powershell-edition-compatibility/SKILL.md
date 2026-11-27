---
name: powershell-edition-compatibility
version: 1.0.0
description: >
  Make scripts work on Windows PowerShell 5.1 and PowerShell 7, covering encoding, syntax and module differences. Use when a script behaves differently between powershell.exe and pwsh.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - powershell
  - windows
  - cross-platform
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: powershell-edition-compatibility
  official: true
  domain: tooling
  security_flags: []
---

# Powershell Edition Compatibility

## When to use
A script must run on both editions, or is moving from one to the other.
## Steps
1. Decide the supported editions and declare them with `#Requires`: `-Version` sets only a minimum, while `-PSEdition` restricts a script to one edition.
2. Parse the script under each shell; operators such as `&&`, `||`, ternary and `??` are syntax errors in 5.1, so the whole file fails to load.
3. Check file encoding. Default encodings for `Set-Content`, `Out-File` and redirection differ; pass `-Encoding` explicitly and remember that `utf8` writes a BOM in 5.1 while 7 offers `utf8NoBOM`.
4. Save scripts containing non-ASCII text with a BOM if 5.1 must read them correctly.
5. Replace WMI cmdlets such as `Get-WmiObject` with `Get-CimInstance`.
6. Check modules: some Windows-only modules do not load natively in 7 and use a compatibility session that returns deserialized objects without live methods.
7. Review web calls: parameters and error types on `Invoke-WebRequest` and `Invoke-RestMethod` differ between editions.
8. If cross-platform, use `Join-Path`, respect case-sensitive file systems, and guard Windows-only code with `$IsWindows` while handling that the variable does not exist in 5.1.
9. Check native argument passing with spaces and embedded quotes in both.
10. Run the same Pester or smoke tests under each shell.
## Watch out for
- Aliases such as `curl` or `wget` resolve differently by edition; call the full cmdlet or `curl.exe`.
- `ConvertTo-Json` truncates beyond its default depth; set `-Depth`.
- Module paths are separate per edition, so a module installed for one may be missing in the other.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same tests pass under both claimed editions, and output files have byte-identical encoding where required.
