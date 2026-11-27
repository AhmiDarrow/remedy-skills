---
name: transcript-cleanup
version: 1.0.1
description: >
  Clean a transcript: speakers, paragraphs, filler removal, summary bullets.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - writing
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: transcript-cleanup
  official: true
  domain: content
  security_flags: []
---

# Transcript Cleanup

## Steps
1. Identify speakers.
2. Paragraph by topic.
3. Light cleanup (keep meaning).
4. Mark inaudible.
5. Executive summary + action items.
6. Redact sensitive info.

## Operating rules
- Prefer read-only exploration before changing files.
- Report commands and outcomes; do not invent results.
- Ask before destructive, paid, or irreversible actions.
- Never print or commit secrets, tokens, or private personal data.
- Use Remedy's tool names (`read`, `write`, `bash`); do not assume a tool that is not in your tool list.

## Done when
The user goal is met, or you list concrete blockers and the next safe step.
