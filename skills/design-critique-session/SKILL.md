---
name: design-critique-session
version: 1.0.1
description: >
  Facilitate a design critique: goals, evidence, actionable feedback, decisions.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - process
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: design-critique-session
  official: true
  domain: design
  security_flags: []
---

# Design Critique Session

## Steps
1. Presenter states goal and constraints (2 min).
2. Silent review.
3. Feedback: observation → impact → suggestion.
4. Separate taste from usability evidence.
5. Capture decisions and follow-ups.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
