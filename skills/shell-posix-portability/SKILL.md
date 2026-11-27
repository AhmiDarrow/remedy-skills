---
name: shell-posix-portability
version: 1.0.0
description: >
  Make shell scripts run across dash, BusyBox, macOS and Linux by removing bashisms and GNU-only flags. Use when a script works on your machine but fails in a container or on another OS.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - shell
  - posix
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
  library_id: shell-posix-portability
  official: true
  domain: tooling
  security_flags: []
---

# Shell Posix Portability

## When to use
A script's target shell or userland differs from where it was written.
## Steps
1. Decide the contract: either require Bash (`#!/usr/bin/env bash`, and ensure it is installed) or write POSIX `sh`. Do not leave it ambiguous.
2. Check how it is invoked. `sh script.sh` ignores the shebang.
3. For POSIX, run `shellcheck -s sh` and `checkbashisms` if available.
4. Replace `[[ ]]` with `[ ]` or `case`, `==` with `=`, `source` with `.`, and remove arrays, `<<<`, process substitution and `${var//a/b}`.
5. Replace `echo -e` and `echo -n` with `printf`.
6. Audit external tools: `sed -i` takes a suffix argument differently on BSD and GNU; `date -d` is GNU while BSD uses other flags; `readlink -f`, `grep -P` and `xargs -r` are not dependable everywhere.
7. Use `command -v` instead of `which` to detect tools.
8. Check line endings: a CRLF file produces "bad interpreter" or stray `\r` errors. Enforce LF via `.gitattributes`.
9. Run the script in each claimed environment, for example `dash`, an Alpine container and a macOS shell, with the same inputs.
## Watch out for
- `local` is widely supported but not POSIX; know whether your targets accept it.
- `set -o pipefail` is missing in older `sh` implementations.
- Linking `/bin/sh` to Bash on one machine hides bashisms during testing.
- Locale affects sorting and character ranges; set `LC_ALL=C` where byte order matters.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The script passes the same test inputs in every environment it claims to support, and the supported list is stated in its header.
