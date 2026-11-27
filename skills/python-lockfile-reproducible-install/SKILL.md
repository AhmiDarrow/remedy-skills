---
name: python-lockfile-reproducible-install
version: 1.0.0
description: >
  Make a Python application install the same dependency versions everywhere using a lock file and hashes. Use when builds differ between laptops, CI and servers.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - python
  - dependencies
  - build
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: python-lockfile-reproducible-install
  official: true
  domain: tooling
  security_flags: []
---

# Python Lockfile Reproducible Install

## When to use
For applications and services that are deployed. Libraries should keep ranges in their metadata and lock only their own development environment.
## Steps
1. Find what exists: `pyproject.toml`, `requirements*.txt`, `setup.py`, `uv.lock`, `poetry.lock`, `Pipfile.lock`. Keep the tool already in use; pick a new one only if there is none.
2. Record the interpreter version in one place (`requires-python`, plus the version file the team's tool reads) and match it in CI and the container image.
3. Separate direct dependencies with compatible ranges from the fully pinned lock. Never hand-edit the lock.
4. With a requirements workflow, compile from an input file with hashes (`pip-compile --generate-hashes` or `uv pip compile --generate-hashes`).
5. Split development and test tools into their own group so they do not ship to production.
6. Install in CI in strict mode: `pip install --require-hashes -r requirements.txt`, `uv sync --locked`, or the equivalent for the installed tool (check its version for the exact flag).
7. Resolve for the platforms you deploy to. A requirements file compiled on one OS can miss markers or wheels for another.
8. Prove it by creating a fresh virtual environment from the lock twice and comparing `pip freeze` output.
## Watch out for
- A CI step that runs a plain unpinned `pip install somepackage` after the locked install can silently change locked versions.
- Extra package indexes allow a public package to shadow an internal name. Configure one authoritative index or explicit per-package sources.
- Upgrading everything while introducing the lock mixes two changes. First lock the versions currently working, upgrade later.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean environment builds from the lock with strict mode on, and CI fails if the lock is stale relative to the declared dependencies.
