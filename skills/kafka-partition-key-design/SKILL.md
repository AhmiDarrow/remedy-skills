---
name: kafka-partition-key-design
version: 1.0.0
description: >
  Choose topic partition counts and message keys that keep required ordering without creating hot partitions. Use when creating a Kafka-style topic or fixing skewed or out-of-order consumption.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - queues
  - kafka
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: kafka-partition-key-design
  official: true
  domain: backend
  security_flags: []
---

# Kafka Partition Key Design

## When to use
A partitioned log is being set up, or one partition lags while others idle.

## Steps
1. State which events must be processed in order relative to each other, usually all events for one entity. Ordering exists only within a partition.
2. Pick the smallest entity that satisfies that as the key.
3. Measure key distribution from real data: share of events for the top keys. One tenant at 40% will overload its partition whatever the count.
4. For hot keys, consider a compound key (tenant plus order id) if ordering is only needed at the finer level. Random salting breaks per-key order.
5. Size partitions from target throughput divided by measured per-consumer throughput, with room to grow, and no more than needed since each adds overhead.
6. Know that increasing partitions changes the key-to-partition mapping, so ordering can break across the change. Plan a drain or a new topic.
7. Check all producers use the same partitioner; client libraries in different languages may hash the same key differently.
8. Preserve order through failures: use the idempotent producer, and decide how consumer retries work, since sending a failed record to a retry topic lets later records overtake it.
9. If consumers process in parallel within a partition, keep per-key serialization and commit only contiguous completed offsets.
10. For compacted topics, require a key and define what a tombstone means.

## Watch out for
- Null keys give no per-entity ordering.
- Auto-created topics get broker defaults that nobody chose; check the topic's actual configuration.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The ordering requirement, key, partition count and skew estimate are written down, and a test with real key distribution shows acceptable balance.
