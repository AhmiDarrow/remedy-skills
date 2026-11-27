---
name: cli-ux-polish
version: 1.0.1
description: >
  Improve a command-line tool's help, argument handling, output streams, exit codes, prompts and scripting behaviour without breaking callers. Use when a CLI is confusing or misbehaves in CI and pipes.
author: Remedy Official
license: Apache-2.0
tags:
  - cli
  - ux
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: cli-ux-polish
  official: true
  security_flags: []
---

# Cli Ux Polish

## When to use
People guess at flags, scripts cannot tell success from failure, or the tool hangs waiting for input in automation.

## Steps
1. Find the argument parser and list commands and flags. Run only help and read-only commands, capturing stdout, stderr and exit code separately. Use scratch data for anything else.
2. `grep` the repository, docs and CI for current invocations; these are the compatibility contract.
3. Help: `-h` and `--help` exit 0 and print to stdout, with a one-line purpose, usage, defaults and two or three realistic examples. A usage mistake prints a short error to stderr naming the bad argument and how to get help.
4. Validate all arguments and conflicts before any side effect. Reject unknown flags.
5. Send results to stdout and progress, warnings and diagnostics to stderr. Offer a machine format such as `--json` where scripts consume output, and keep it free of decoration.
6. Exit 0 only on success. Use a few documented non-zero codes where callers need to tell cases apart, and make partial failure non-zero.
7. When stdin is not a terminal, never block on a prompt: fail with the flag that supplies the answer. Destructive commands require an explicit `--yes` or equivalent; offer `--dry-run`.
8. Turn off colour and animations when output is not a terminal, and honour `NO_COLOR`.
9. Handle interrupts and closed pipes cleanly, leaving no half-written files; write to a temporary file then rename.
10. Add tests that assert exit code and each stream, including piped and non-interactive runs.

## Watch out for
- Renaming flags, changing default behaviour or reshaping parsed output breaks callers; add aliases and deprecation notices, or flag it as breaking.
- A global CI variable that silently means yes to deletion.
- Secrets passed as flags appear in shell history and process lists; accept a file, stdin or the environment, and do not echo them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Help matches real behaviour, tests confirm exit codes and streams including a non-interactive run, existing invocations still work or are listed as breaking, and docs are updated.
