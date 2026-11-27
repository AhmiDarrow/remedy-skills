---
name: budget-snapshot
version: 1.0.1
description: >
  Create a simple budget snapshot: income, fixed costs, variable, goals (no bank logins).
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - finance
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: budget-snapshot
  official: true
  domain: personal
  security_flags: []
---

# Budget Snapshot

## Steps
1. User-provided numbers only (never scrape banks).
2. Categories: fixed, variable, savings, debt.
3. Surplus/deficit.
4. 1–3 adjustment options.
5. Privacy: store only if user asks.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
