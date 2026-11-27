---
name: troubleshooting-guide-tree
version: 1.0.0
description: >
  Write a symptom-first troubleshooting guide that narrows causes with observable checks. Use when a product or system has recurring problems people cannot diagnose alone.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - troubleshooting
  - support
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: troubleshooting-guide-tree
  official: true
  domain: docs
  security_flags: []
---

# Troubleshooting Guide Tree

## When to use
Several different causes produce similar symptoms and readers guess at fixes.

## Steps
1. Gather real cases from tickets, issues and logs; record the symptom in the reporter's words.
2. Make one entry point per symptom, not per component, since readers do not know which component failed.
3. For each symptom list candidate causes, weighted by how often they occur and how cheap they are to check.
4. Write each node as: check to perform, where to look, what result A means, what result B means. Every branch ends in a fix, another check or escalation.
5. Put read-only checks before anything that changes state.
6. Mark fixes that lose data, restart services or log users out, with how to undo them.
7. Give commands per operating system where they differ and show the output line that matters.
8. At the escalation leaf, list exactly what to collect.
9. Walk each branch against a past case and confirm it lands on the known cause.

## Watch out for
- "Reinstall" or "clear everything" as an early step; it destroys evidence.
- Checks with no interpretation ("look at the logs").
- Branches that loop back without new information.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every symptom path ends in a fix or an escalation checklist, and past cases route to their known causes.
