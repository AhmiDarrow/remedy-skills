---
name: python-subprocess-hardening
version: 1.0.0
description: >
  Make Python subprocess calls safe and reliable: argument lists, timeouts, exit codes, pipe deadlocks and Windows quirks. Use when code shells out to external programs.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - python
  - cli
  - reliability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: python-subprocess-hardening
  official: true
  domain: security
  security_flags: []
---

# Python Subprocess Hardening

## When to use
Reviewing or fixing code that launches other programs, especially with user-influenced input or in long-running services.
## Steps
1. Inventory calls: `grep` for `subprocess`, `os.system` and `os.popen`. Mark which arguments come from users, files or the network.
2. Pass a list of arguments and let no shell parse them. Replace shell pipelines by connecting two processes or filtering in Python.
3. For user values that could start with a dash, insert `--` before them if the target program supports it, or validate against an allow list. A list argument stops shell injection, not option injection.
4. Add `check=True` or inspect `returncode` explicitly. Note which tools use nonzero for non-errors, such as `grep` returning 1 for no match.
5. Give every call a `timeout`. With `Popen`, on timeout call `kill()` then `communicate()` to reap the child. If it spawns grandchildren, start it in its own process group or session and terminate the group.
6. Use `capture_output=True` or `communicate()`. Calling `wait()` while stdout is a pipe deadlocks once the buffer fills. Stream line by line for large output.
7. Set `text=True` with an explicit `encoding` and an `errors` policy; the locale default differs across machines.
8. Resolve the executable with `shutil.which` and fail with a clear message if missing. Pass a minimal `env` when secrets in the parent environment should not reach the child.
## Watch out for
- On Windows, `.bat` and `.cmd` files are run through the command interpreter even with a list, so untrusted arguments to them need strict validation.
- Command lines are visible to other users in process listings; send secrets via stdin or a protected file.
- `CalledProcessError` messages include the full argument list, which can leak tokens into logs.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every call has a timeout and exit-code handling, none passes untrusted text to a shell, and a test with a hostile argument shows it is treated as data.
