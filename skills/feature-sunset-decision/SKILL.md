---
name: feature-sunset-decision
version: 1.0.0
description: >
  Decide whether to retire a product feature and plan the exit using usage, cost and customer impact. Use when a little-used feature costs more to keep than it returns.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - product
  - lifecycle
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: feature-sunset-decision
  official: true
  domain: data
  security_flags: []
---

# Feature Sunset Decision

## When to use
A feature adds maintenance, confusion or risk and someone asks whether it can go.

## Steps
1. Measure use over a window long enough to include periodic tasks such as quarter-end and annual ones.
2. Break users down by account and importance; a tiny share can include critical customers. Confirm the instrumentation covers all entry points, including API and automation.
3. List costs with evidence: bugs, support volume, blocked work, security exposure.
4. Ask a sample of users what they use it for.
5. Find contractual, regulatory and sales commitments and send questions to the responsible people.
6. Compare options: keep, simplify, replace, make optional, retire.
7. If retiring, define alternative, data export, notice period, stages (hide from new users, then read-only, then remove) and exceptions.
8. Set what would reverse the decision and keep data until the agreed deletion date.

## Watch out for
- Reading zero events as zero use when tracking was never added.
- Deleting user data as part of removing the screen.
- Learning of a key customer's dependency from their complaint.
- No owner for exception requests.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The decision record shows usage, affected accounts, options and, if retiring, export path, stages and communication owner.
