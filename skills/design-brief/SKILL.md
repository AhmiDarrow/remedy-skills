---
name: design-brief
version: 1.0.1
description: >
  Write a design brief: problem, audience, constraints, success metrics, deliverables.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - product
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: design-brief
  official: true
  domain: design
  security_flags: []
---

# Design Brief

## Steps
1. Problem statement and non-goals.
2. Audience and contexts of use.
3. Constraints (time, brand, tech, a11y).
4. Success metrics.
5. Deliverables and milestones.
6. Open questions.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
