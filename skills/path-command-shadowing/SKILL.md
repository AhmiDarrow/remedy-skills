---
name: path-command-shadowing
version: 1.0.0
description: >
  Work out why a terminal runs the wrong version of a tool or cannot find an installed one. Use when command not found appears after install or versions differ between shells and editors.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - environment
  - cli
  - debugging
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: path-command-shadowing
  official: true
  domain: tooling
  security_flags: []
---

# Path Command Shadowing

## When to use
Installation succeeded but the shell disagrees.
## Steps
1. List every candidate, not the first: `type -a tool` in Bash or zsh, `Get-Command tool -All` in PowerShell, `where.exe tool` in the Windows command prompt.
2. Check for aliases, functions and cached lookups. `hash -r` clears Bash's cache.
3. Print the search path one entry per line in the failing context and in a working one, and compare order.
4. Resolve what each candidate is: a real binary, symlink, version manager shim or app store stub.
5. Compare contexts: login versus interactive shell, IDE launched from the desktop, cron, a service account and sudo each get different environments.
6. Find where the path is modified. Search shell startup files in load order; on Windows compare machine and user variables and the PowerShell profile.
7. Restart the process that should see a change. Already-running terminals and editors keep the old environment.
8. Propose the smallest fix: reorder one entry, configure the version manager, or use an absolute path in scheduled jobs. Show the exact line and get approval before editing profiles or system variables.
## Watch out for
- `setx` truncates long values, and writing the combined process PATH back to user scope duplicates machine entries. Edit only the scope's own value and save the old one first.
- A relative or empty path entry runs binaries from the current directory.
- On ARM and Intel mixed machines, two package manager prefixes can supply different architectures.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh instance of each affected context resolves the intended binary and reports the expected version, and the original value is recorded for rollback.
