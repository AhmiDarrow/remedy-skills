---
name: bash-script-hardening
version: 1.0.0
description: >
  Harden an existing Bash script against unquoted expansions, silent failures, unsafe temp files and destructive paths. Use before running a script in CI, cron or on production.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - bash
  - shell
  - security
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: bash-script-hardening
  official: true
  domain: tooling
  security_flags: []
---

# Bash Script Hardening

## When to use
A Bash script does real work and failure or odd input could cause damage.
## Steps
1. Run `shellcheck` if installed and fix by category; justify any disable directive inline.
2. Add `set -euo pipefail`, then review each command whose failure is expected (`grep` with no match, `((i++))` from zero) and handle it explicitly.
3. Know where `set -e` does nothing: inside conditions, in functions called from `if` or `||` chains, and in `local x=$(cmd)`, where the status is masked. Declare then assign separately.
4. Quote expansions and use arrays for argument lists: `"${args[@]}"`.
5. Before any recursive delete or sync, require the variables: `"${DIR:?DIR not set}"`, and verify the path is inside the expected root.
6. Create scratch space with `mktemp -d` and remove it with `trap 'rm -rf -- "$tmp"' EXIT`.
7. Put `--` before file operands and handle names with spaces using globs or NUL-delimited input, not parsing `ls`.
8. Add a lock (`flock` where available) if overlapping runs would corrupt state.
9. Provide a dry-run switch for destructive actions and test only against throwaway copies in a temporary root, never real or production data: input with spaces, a leading dash, an empty set and a failing command.
## Watch out for
- With `pipefail`, `cmd | head -1` can fail from SIGPIPE.
- `set -x` prints secrets into logs.
- An unmatched glob stays literal unless `nullglob` is set, so loops run once on a fake name.
- macOS ships an old Bash; check the version before using associative arrays or `mapfile`.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
shellcheck is clean or annotated, and the hostile-input tests behave correctly, including a forced mid-script failure that cleans up.
