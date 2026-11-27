---
name: game-telemetry-events
version: 1.0.1
description: >
  Define gameplay telemetry events for funnels, balance, and crash context (privacy-aware).
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - ops
  - privacy
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: game-telemetry-events
  official: true
  domain: gaming
  security_flags: []
---

# Game Telemetry Events

## Steps
1. Questions design needs answered (drop-off, weapon usage, crash level).
2. Event list with properties and enums.
3. Avoid PII; hash ids if needed.
4. Sampling for high-frequency events.
5. Dashboard sketches (funnel, heat).
6. Retention/deletion notes.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
