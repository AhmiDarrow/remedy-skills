---
name: relational-schema-design
version: 1.0.0
description: >
  Turn a domain description into tables with keys, constraints and relationships that make bad states unstorable. Use when designing a new database schema or reviewing one before data goes in.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - modeling
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - bash
metadata:
  source: library
  library_id: relational-schema-design
  official: true
  domain: backend
  security_flags: []
---

# Relational Schema Design

## When to use
New tables are about to be created and mistakes are still cheap to fix.

## Steps
1. List the entities and, for each, one sentence saying what a single row represents.
2. Write the questions and writes the application must support; they test the design later.
3. Write invariants in plain words ("one active subscription per account", "an invoice line cannot outlive its invoice").
4. Give every table a primary key. Keep real-world identifiers as unique columns, since emails and codes change.
5. Normalize so each fact is stored once. Copy a value only when it records history, such as the price at the time of order, and name it to say so.
6. Turn invariants into constraints: `NOT NULL`, `UNIQUE` (including composite and partial unique indexes), `CHECK`, foreign keys with a deliberate `ON DELETE` rule.
7. Model many-to-many with a join table holding its own attributes and a unique pair.
8. Avoid generic `entity_type` plus `entity_id` references where real foreign keys are possible, and avoid comma-separated lists in a column.
9. Choose types precisely: exact numerics for money, timezone-aware timestamps for instants, dates for calendar days.
10. In a multi-tenant system carry the tenant id on owned tables and include it in unique and foreign keys.
11. Insert sample data, including cases that should be rejected, and write the main queries.

## Watch out for
- `UNIQUE` allows multiple NULLs in many databases, which silently breaks "only one" rules.
- Cascading deletes from a central table can remove far more than intended; trace each path.
- A status column plus several booleans permits contradictory combinations.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The DDL runs on an empty database, every listed invariant has a constraint or a written reason it lives in code, and invalid sample inserts fail.
