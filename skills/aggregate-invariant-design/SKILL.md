---
name: aggregate-invariant-design
version: 1.0.0
description: >
  Decide which objects must stay consistent together and where each business rule is enforced. Use when invalid data keeps appearing because several code paths update related records independently.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - domain-modeling
  - consistency
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: aggregate-invariant-design
  official: true
  domain: backend
  security_flags: []
---

# Aggregate Invariant Design

## When to use
Totals disagree with line items, capacity gets exceeded or a child record outlives its parent.
## Steps
1. Write each rule as a statement that must always hold, for example "booked seats never exceed room capacity".
2. For each, decide with the domain owner whether it must hold instantly or may be briefly violated and repaired. Only the first kind needs one transaction.
3. List the data each instant rule needs. The smallest set that covers a rule is a consistency boundary with one root.
4. Route all changes through operations on that root; remove setters and direct writes that bypass them.
5. Reference other aggregates by id instead of loading and mutating them in the same operation.
6. Handle concurrent edits: a version number with conditional update, row locking, or a database constraint. In-memory checks alone lose races.
7. Push expressible rules into the database too (unique, check, foreign key).
8. For eventual rules, define the event, the handler, behaviour on repeat delivery and a reconciliation check.
9. Query existing data for violations before adding constraints.
## Watch out for
- A giant aggregate that loads thousands of children and makes every edit contend.
- Checking a rule with a read in one transaction and writing in another.
- Rules duplicated in UI and server with different edge behaviour; the server is authoritative.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every listed rule has a named enforcement point that survives concurrent writes, or a defined eventual repair, and existing violations are counted.
