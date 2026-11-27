---
name: interaction-states
version: 1.0.1
description: >
  Specify full interaction states for components: default, hover, focus, active, disabled, error, loading.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ui
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: interaction-states
  official: true
  domain: design
  security_flags: []
---

# Interaction States

## Steps
1. Component list.
2. State matrix.
3. Motion/timing if any (subtle).
4. Keyboard focus visible.
5. Map to CSS/classes in code when implementing.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
