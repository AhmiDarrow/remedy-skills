---
name: game-bug-triage
version: 1.0.1
description: >
  Triage gameplay bugs by repro, severity, blocker status, and regression risk.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - qa
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: game-bug-triage
  official: true
  domain: gaming
  security_flags: []
---

# Game Bug Triage

## Steps
1. Repro steps and build number.
2. Severity (blocker/major/minor/polish).
3. Platform/config matrix.
4. Regression likelihood.
5. Assign owner and milestone.
6. Link logs/saves without private data.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
