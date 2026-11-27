---
name: event-schema-evolution
version: 1.0.0
description: >
  Change an event or message schema while old and new producers, consumers and stored messages coexist. Use when adding, renaming or removing fields on queued or logged events.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - messaging
  - schemas
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: event-schema-evolution
  official: true
  domain: backend
  security_flags: []
---

# Event Schema Evolution

## When to use
A message format must change and not every producer and consumer can be updated at once.

## Steps
1. Find all producers, consumers and archives of the event, including analytics loaders and replay tools.
2. Establish how long old messages live: queue retention, DLQs, compacted topics, event stores. Compacted and event-sourced data may live forever.
3. Name the compatibility needed. Backward: new readers read old data, so upgrade consumers first. Forward: old readers read new data, so producers may go first. Full: both.
4. Prefer additive changes: new optional fields with defaults.
5. Never reuse a name or field number with a new meaning. In Protocol Buffers, mark removed numbers and names `reserved`.
6. For rename or type change, expand and contract: publish both, move consumers, confirm by metrics, then drop the old.
7. Check that consumers ignore unknown fields and handle unknown enum values; strict validators often reject additions.
8. If the format changes meaning, publish a new event type or major version and run both for a stated period.
9. Enforce in CI with a schema registry compatibility check or a test that parses a saved corpus of every historical version with the new code.

## Watch out for
- Schema-compatible is not the same as meaning-compatible: switching cents to whole units passes every checker.
- Checking only against the previous version misses incompatibility with older retained messages; use transitive checks.
- Rolling back a producer or consumer must also work after new-format messages exist.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The rollout order is written, the new code parses the historical corpus, and old consumers were tested against a new-format message.
