---
name: cli-reference-from-help
version: 1.0.0
description: >
  Write a command-line reference grounded in the tool's real help output and behaviour. Use when a CLI lacks documentation or its reference has drifted.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - cli
  - reference
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
metadata:
  source: library
  library_id: cli-reference-from-help
  official: true
  domain: docs
  security_flags: []
---

# Cli Reference From Help

## When to use
Users need every command, flag and exit behaviour in one accurate place.

## Steps
1. Record the version under documentation from the tool's version command.
2. Walk the command tree: run `--help` at the top and for every subcommand. Only run commands that merely print help.
3. Read the argument-parser source to find hidden or deprecated flags, defaults, environment-variable equivalents and mutually exclusive options.
4. For each command document: one-line purpose, synopsis, arguments, flags with type and default, and what it changes on disk or remotely.
5. State configuration precedence (flag, environment, file, default) as the code implements it.
6. Document exit codes found in the source, and what goes to stdout versus stderr for scripting.
7. Add an example per common task. Run safe ones against scratch data and paste real, redacted output.
8. If a generator exists in the framework, generate the tables and hand-write only examples and cautions.

## Watch out for
- Running a destructive subcommand to see what it does; many ignore `--help` placed after arguments.
- Inventing conventional flags such as `--verbose` that this tool lacks.
- Documenting a default from help text that the code contradicts. Report the mismatch.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every subcommand in the parser appears with its flags and defaults, and each example is marked as run or not run.
