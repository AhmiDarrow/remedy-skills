---
name: python-interpreter-upgrade
version: 1.0.0
description: >
  Move a Python project to a newer interpreter release, handling removed stdlib modules, deprecations and compiled wheels. Use before raising requires-python or the runtime image.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - python
  - upgrade
  - dependencies
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
  - web.fetch
  - todo
metadata:
  source: library
  library_id: python-interpreter-upgrade
  official: true
  domain: tooling
  security_flags: []
---

# Python Interpreter Upgrade

## When to use
A Python version is nearing end of life, or a dependency requires a newer one.
## Steps
1. Record the current and target versions and read the official "What's New" porting sections for every minor release in between, not just the target.
2. On the old version, run the tests with `python -X dev -W default::DeprecationWarning -m pytest` and list each warning with its owner: your code or a dependency. Turn them into errors once the list is clear.
3. `grep` for modules removed along the way, such as `distutils` and `imp` (gone in 3.12) and the legacy modules dropped in 3.13 (`cgi`, `telnetlib`, `crypt` and others).
4. Check every compiled dependency publishes a wheel for the target version and platform. Try `pip download --only-binary=:all: --python-version <target> --platform <tag> -d <empty dir> -r <locked requirements>`; without the version flag pip checks the interpreter running it.
5. Upgrade blocking dependencies first, while still on the old interpreter, so failures are attributable.
6. Create a new virtual environment with the target interpreter. Never repoint an old one.
7. Run tests, type check and a real smoke run of entry points, including scripts and scheduled jobs that tests do not import.
8. Run both versions in CI until deployed, then update `requires-python`, classifiers, container base image and tool target-version settings together.
## Watch out for
- A missing wheel makes the installer build from source, which may succeed on a laptop with compilers and fail in a slim image.
- Behavior changes without errors, such as multiprocessing defaults or datetime deprecations, only show in runtime tests.
- Tool configs (linter, formatter, type checker) often pin their own target version and keep enforcing old rules.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests and smoke runs pass on the target interpreter from a fresh environment, and every place that names the old version has been found by search and updated.
