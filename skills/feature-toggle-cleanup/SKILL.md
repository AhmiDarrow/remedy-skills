---
name: feature-toggle-cleanup
version: 1.0.1
description: >
  Find stale feature flags and remove dead code paths safely.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: feature-toggle-cleanup
  official: true
  security_flags: []
---

# Feature Toggle Cleanup

## Steps
1. Inventory flags and default states.
2. Identify permanently on/off.
3. Delete dead branch after confirm.
4. Remove config entries.
5. Tests still pass.

## Operating rules
- Prefer **read-only** exploration before edits.
- Show commands run and their outcomes.
- Ask before destructive git, production changes, or secret access.
- Never commit or print live secrets.
- Stop with a clear blocker list if environment tools are missing.

## Done when
The user's goal is met **or** you report exactly what remains blocked and why.
