---
name: fact-check-pass
version: 1.0.1
description: >
  Fact-check a draft: claims, numbers, links, attribution, uncertainty language.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - quality
kind: native
status: discovered
tools:
  - read
  - web.search
metadata:
  source: library
  library_id: fact-check-pass
  official: true
  domain: content
  security_flags: []
---

# Fact Check Pass

## Steps
1. Extract factual claims.
2. Verify each with sources; prefer primary.
3. Check numbers and dates.
4. Link rot check.
5. Soften unverified claims.
6. Log corrections.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
