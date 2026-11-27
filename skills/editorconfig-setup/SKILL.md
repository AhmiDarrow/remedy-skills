---
name: editorconfig-setup
version: 1.0.1
description: >
  Add .editorconfig aligned with project formatters.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: editorconfig-setup
  official: true
  security_flags: []
---

# Editorconfig Setup

## Steps
1. Detect languages.
2. UTF-8, final newline, trim trailing whitespace.
3. Indent matching prettier/black/gofmt conventions.
4. Don't fight dedicated formatters.

## Operating rules
- Prefer **read-only** exploration before edits.
- Show commands run and their outcomes.
- Ask before destructive git, production changes, or secret access.
- Never commit or print live secrets.
- Stop with a clear blocker list if environment tools are missing.

## Done when
The user's goal is met **or** you report exactly what remains blocked and why.
