---
name: dead-letter-queue-triage
version: 1.0.0
description: >
  Work through a dead-letter queue by grouping failures, fixing causes and replaying safely. Use when messages have piled up in a DLQ or someone wants to redrive them.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - queues
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
  - edit
metadata:
  source: library
  library_id: dead-letter-queue-triage
  official: true
  domain: backend
  security_flags: []
---

# Dead Letter Queue Triage

## When to use
Messages have been dead-lettered and each needs to be replayed, repaired or deliberately discarded.

## Steps
1. Check the DLQ retention period first. If expiry is near, export the messages somewhere access-controlled before investigating.
2. Inspect without consuming. Learn whether the broker's peek or receive changes visibility, order or delivery counts.
3. Collect for each: message id, type, enqueue time, attempts, error if recorded, source queue. Recover missing errors from consumer logs by id.
4. Group by error signature and message type, and line up first occurrences with deploys, schema changes and dependency outages.
5. Classify each group: transient (replay as is), consumer bug (fix, then replay), bad producer data (fix producer, repair or discard), or obsolete (superseded by newer state).
6. Before replay, verify the consumer is idempotent for that type. A message may have partly succeeded before failing.
7. Check ordering: replaying an old "address changed" after a newer one reverts data. Compare versions or timestamps.
8. Show the user the plan with counts per group and get approval for replay or deletion.
9. Replay a few, verify effects downstream, then the rest at a limited rate while watching the DLQ and live latency.
10. Close the gap: an alert on DLQ depth and age, and the error stored with each dead-lettered message.

## Watch out for
- Bulk redrive before the fix just fills the DLQ again, and may repeat side effects.
- Replay through a different path can drop headers, keys or trace ids the consumer needs.
- Payload exports may contain personal data; keep them out of tickets and repositories and delete them afterward.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every message is accounted for as replayed and verified, repaired, or discarded with approval, and the cause has a fix or an owner.
