---
name: game-build-checklist
version: 1.0.1
description: >
  Pre-ship game build checklist: content locks, known issues, platform cert hygiene (generic).
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - release
kind: native
status: discovered
tools:
  - read
  - bash
metadata:
  source: library
  library_id: game-build-checklist
  official: true
  domain: gaming
  security_flags: []
---

# Game Build Checklist

## Checklist
1. Version/build number stamped.
2. Debug cheats off in release config.
3. Content cook/build succeeds cleanly.
4. Crash reporter configured.
5. Known issues list with severities.
6. First-boot path tested cold.
7. Save compatibility notes.
8. Store listing assets readiness (icons, trailers) if shipping.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
