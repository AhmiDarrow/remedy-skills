---
name: python-packaging
version: 1.0.1
description: >
  Package a Python project with pyproject.toml, build the wheel and sdist, and prove they install and run from a clean environment. Use when making a library or CLI installable.
author: Remedy Official
license: Apache-2.0
tags:
  - python
  - packaging
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: python-packaging
  official: true
  security_flags: []
---

# Python Packaging

## When to use
Python code needs to be distributed or installed rather than run from its folder.

## Steps
1. Identify import packages, entry points, supported Python versions, data files and any native code. Keep the existing build backend unless there is a reason to change.
2. Set `[build-system]` and `[project]`: name, version or dynamic source, description, readme, license, `requires-python` and dependencies. Check which license metadata form the backend version supports. Keep development tools out of runtime dependencies.
3. For a new project prefer a `src/` layout so tests do not import the checkout by accident.
4. Declare commands under `[project.scripts]` as `name = "package.module:function"`.
5. Configure non-code files and `py.typed` per the backend, and load them with `importlib.resources`.
6. Remove old build output, then run `python -m build` or `uv build`.
7. List contents of both wheel and sdist. Confirm required files are present and tests, secrets, env files and local data are not unintentionally included.
8. In a fresh virtual environment, outside the source tree, install the wheel, import the package, run each command and read a data file. Separately build or install from the sdist. Cover the oldest and newest supported Python available.
9. If publishing is requested, check metadata with `twine check`. Publishing needs explicit approval; a version on a public index cannot be re-uploaded.

## Watch out for
- An editable install hides missing modules and data.
- Exact pins in a library's dependencies cause conflicts for users.
- Check that the distribution name is available and not confusingly close to another.
- A universal wheel tag is wrong for compiled extensions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Clean installs from the built artifacts import and run, contents have been inspected, and nothing was published without approval.
