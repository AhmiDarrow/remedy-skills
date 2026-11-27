---
name: queue-consumer-safe
version: 1.0.1
description: >
  Build or review a message queue consumer with correct acknowledgement, idempotent handling, bounded retries and dead-lettering. Use when messages are lost, processed twice or block the queue.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - ops
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: queue-consumer-safe
  official: true
  security_flags: []
---

# Queue Consumer Safe

## When to use
Code consumes from a queue or stream.

## Steps
1. Read the broker and client configuration and confirm delivery semantics: acknowledgement mode, auto-commit, visibility timeout or lease, prefetch, ordering, redelivery and dead-letter support. Assume duplicates can occur.
2. Acknowledge only after the effect is durably recorded. Turn off automatic acknowledgement or offset commit if it can run ahead.
3. Deduplicate on a stable business or event id with a unique constraint, in the same transaction as the effect. For external calls, pass an idempotency key. If the handler publishes messages, use an outbox.
4. Validate the message schema and version first. Define compatibility with older and newer producers.
5. Classify failures. Retry transient ones with delay and backoff; send permanently invalid messages to the dead-letter destination with error and attempt context. During a dependency outage, pause consumption rather than burning every message's attempts.
6. Check what a negative acknowledgement does on this broker; immediate requeue can spin forever.
7. Keep the lease longer than processing time or extend it, and stop work if ownership is lost. In Kafka, watch the maximum poll interval and commit only contiguous completed offsets per partition.
8. Where order matters, serialise by key or reject stale versions, and decide whether a failed message blocks its key.
9. Bound concurrency to what downstream systems can take. On shutdown or rebalance, stop fetching and finish or release held work.
10. Test duplicate, concurrent duplicate, poison, out-of-order and crash-before-acknowledge cases. Add metrics for lag, oldest age, outcomes, retries and dead-letter count.

## Watch out for
- Catching an exception, logging it and acknowledging anyway.
- Parallel processing committing a later offset while an earlier one failed.
- Dead-letter queues that expire unnoticed.
- Deduplication records kept for less time than a replay can reach.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Crash and duplicate tests show no lost or doubled effects, poison messages leave the main path after bounded attempts, and dead letters raise an alert.
