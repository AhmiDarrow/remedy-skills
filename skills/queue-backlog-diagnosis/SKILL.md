---
name: queue-backlog-diagnosis
version: 1.0.0
description: >
  Work out why a queue or consumer group is falling behind and add capacity or fix the bottleneck without making it worse. Use when queue depth, consumer lag or message age keeps climbing.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - queues
  - performance
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: queue-backlog-diagnosis
  official: true
  domain: backend
  security_flags: []
---

# Queue Backlog Diagnosis

## When to use
Work is arriving faster than it finishes, and processing delay is visible to users or alerts.

## Steps
1. Plot arrival rate, completion rate and oldest-message age over the same window. Establish whether arrivals rose, completions fell, or both.
2. Compute drain time as backlog divided by (processing rate minus arrival rate). If that difference is not positive it never drains.
3. Check consumers are alive and receiving: restarts, crash loops, rebalances, paused subscriptions, prefetch settings.
4. For partitioned logs, view lag per partition, for example `kafka-consumer-groups.sh --bootstrap-server <host> --describe --group <group>` (script name varies by distribution). One hot or stuck partition differs from uniform lag.
5. Break down time per message: dependency calls, database, CPU, waiting on pools or rate limits.
6. Look for redelivery loops where processing exceeds the visibility timeout or poll interval, so work repeats.
7. Confirm the downstream has headroom before adding consumers. In Kafka, consumers beyond the partition count sit idle in a group.
8. Apply the matching fix: batch writes, bounded concurrency, a longer processing window, isolating slow message types in their own queue, or shedding stale work with the user's approval.
9. Watch the age metric until it returns to normal and record the capacity per consumer.

## Watch out for
- Scaling consumers against a saturated database lowers total throughput.
- Raising concurrency can break per-key ordering.
- Purging the queue or resetting offsets loses work; treat it as destructive and ask.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The bottleneck is identified with measurements, processing rate exceeds arrival rate, and the oldest-message age is back within its target.
