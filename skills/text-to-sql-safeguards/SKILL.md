---
name: text-to-sql-safeguards
version: 1.0.0
description: >
  Build natural-language database querying with least-privilege access, schema context, query limits and result-based evaluation. Use when letting users or an assistant query data in plain language.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - sql
  - hardening
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - grep
metadata:
  source: library
  library_id: text-to-sql-safeguards
  official: true
  domain: llm
  security_flags: []
---

# Text To Sql Safeguards

## When to use
A model will generate SQL that runs against a real database.

## Steps
1. Scope the questions to support and the users. For common ones, prefer parameterized report tools over free SQL.
2. Expose curated views with clear names, not the raw schema, and exclude sensitive columns.
3. Connect with a dedicated read-only role granted only those views, preferably on a replica. Check callable functions too; a `SELECT` can invoke ones with side effects.
4. Enforce tenant and row access in the database from the authenticated user, never from model-written `WHERE` clauses. Verify view ownership does not bypass row-level security, and that generated SQL cannot change the tenant setting.
5. Give the model table grain, column meanings, join keys, enum values, time zone and metric definitions.
6. Parse the SQL with a real parser and allow a single read query. Treat this as an extra layer over permissions, not the barrier.
7. Apply statement timeout, row and byte caps, concurrency limits and a plan-cost check if useful. Say when results are truncated.
8. Ask a clarifying question when a term or period is ambiguous.
9. Show the SQL, assumptions and filters with the answer. Compute figures in SQL, not in the model's prose.
10. Evaluate by comparing result sets on fixed data with known-correct queries, including unanswerable and cross-tenant requests.

## Watch out for
- Valid SQL with join fan-out returns confident wrong totals.
- `LIMIT` bounds returned rows, not the work performed.
- Database error messages and cell values are untrusted text and may reveal data or contain instructions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Write and cross-tenant attempts are refused by the database itself, limits are shown to stop a runaway query, and accuracy is reported on the evaluation set.
