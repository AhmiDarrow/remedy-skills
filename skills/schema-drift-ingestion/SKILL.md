---
name: schema-drift-ingestion
version: 1.0.0
description: >
  Make ingestion detect and handle added, missing, renamed or retyped columns in incoming files and feeds. Use when an upstream format change broke or silently corrupted a load.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - pipelines
  - ingestion
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: schema-drift-ingestion
  official: true
  domain: data
  security_flags: []
---

# Schema Drift Ingestion

## When to use
Data arrives from a source you do not control and its shape can change without notice.

## Steps
1. Write the expected contract: columns by name, type, nullability, units, date format, encoding, delimiter and key.
2. Land the raw payload unchanged, with source, arrival time and checksum, before parsing, under access and retention rules suited to its contents.
3. Compare each batch's observed schema to the contract before transforming.
4. Decide per change type. New column: keep in raw, report, do not break. Missing required column: stop. Type change or unparseable values above zero tolerance: quarantine and stop. New category value: map to explicit unknown and report. Rename: treat as missing plus new until a person confirms.
5. Map columns by header name, never by position, and fail on duplicate headers.
6. Parse with explicit types. Read identifiers as text so leading zeros and long numbers survive.
7. State date formats and time zones; do not let a parser guess day and month order per file.
8. Watch for same-type drift using value ranges and null rates: units, currency or scale can change with an identical schema.
9. Version the contract and record which version processed each batch.
10. Keep fixture files for each drift case and test them.

## Watch out for
- Loaders that autodetect types from the first rows change their mind between files.
- Automatically adding every new column to curated tables can publish sensitive fields.
- Coercing bad values to NULL makes the load succeed and the report wrong.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each drift fixture produces its intended outcome, and a stopped batch can be reprocessed from raw after the contract is updated.
