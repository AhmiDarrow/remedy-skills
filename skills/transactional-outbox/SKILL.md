---
name: transactional-outbox
version: 1.0.0
description: >
  Publish events reliably when a database change and a message must both happen, using an outbox table and a relay. Use when messages go missing or get sent for rolled-back writes.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - messaging
  - database
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: transactional-outbox
  official: true
  domain: backend
  security_flags: []
---

# Transactional Outbox

## When to use
Code writes to the database and then publishes to a broker (or the reverse), so a crash between the two leaves them disagreeing.

## Steps
1. Find each dual write with `grep` around publish calls and note what is lost or fabricated if the process dies between the two operations.
2. Create an outbox table: unique message id, aggregate type and id, event type, payload, created time, sent time, attempt count.
3. Insert the outbox row in the same transaction and connection as the business change. Confirm the ORM does not autocommit it separately.
4. Build a relay: select unsent rows in order with `FOR UPDATE SKIP LOCKED` where supported, publish, wait for the broker's acknowledgement, then mark sent. Log-based change capture on the outbox table is the alternative to polling.
5. If order matters per entity, publish with the entity id as the partition or ordering key and run one relay per key range. `SKIP LOCKED` with several relays can reorder events.
6. Make consumers deduplicate on the message id; the relay can crash after publish and before marking.
7. Add a partial index on unsent rows and delete or archive sent ones on a schedule.
8. Alert on the age of the oldest unsent row, which catches a stopped relay.
9. Test by killing the relay between publish and mark, and by rolling back the business transaction.

## Watch out for
- A sequence id is assigned before commit, so a lower id can become visible after a higher one. A relay that tracks "last id sent" will skip rows; track sent status per row.
- One unpublishable message at the head can block everything; define a quarantine after repeated failures.
- Holding a transaction open across slow broker calls bloats the table and pins connections; keep batches small.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Rolled-back changes produce no message, a killed relay causes at most a duplicate that the consumer ignores, and outbox age is monitored.
