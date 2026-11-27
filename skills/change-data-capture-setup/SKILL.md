---
name: change-data-capture-setup
version: 1.0.0
description: >
  Set up log-based change data capture with a consistent snapshot, ordered apply, delete handling and slot monitoring. Use when replicating database changes to a warehouse, index or another service.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - pipelines
  - replication
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - web.fetch
metadata:
  source: library
  library_id: change-data-capture-setup
  official: true
  domain: data
  security_flags: []
---

# Change Data Capture Setup

## When to use
Downstream systems need inserts, updates and deletes from a database with low delay, without polling queries.

## Steps
1. Confirm database version, permissions and what the host allows; fetch the connector's current documentation for these. Log settings may need a restart, so ask before changing them.
2. For PostgreSQL this means `wal_level = logical`, a publication and a replication slot; MySQL needs row-based binary logging with adequate retention.
3. Check every captured table has a primary key or suitable replica identity, otherwise updates and deletes cannot be matched.
4. Select tables and columns explicitly and exclude data the destination should not hold.
5. Take the initial snapshot tied to a log position, so streaming begins with no gap.
6. Apply idempotently by primary key, using the log position to ignore older changes. Assume at-least-once delivery.
7. Preserve order per key through any broker.
8. Represent deletes explicitly and handle truncates and primary key updates.
9. Test schema changes in staging; logical replication in PostgreSQL does not carry DDL.
10. Monitor lag in time and bytes, and for slots the retained WAL in `pg_replication_slots`.
11. Document resnapshot, failover behaviour and decommissioning, including removing the slot.

## Watch out for
- A stopped consumer with a live slot retains WAL until the primary's disk fills.
- Unchanged large (TOAST) values may be absent from update events; do not overwrite them with null or a placeholder.
- Transaction boundaries can be lost downstream, exposing half-applied changes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
After inserts, updates, deletes and a consumer restart, source and destination match by key and checksum, and lag and log retention are alerted.
