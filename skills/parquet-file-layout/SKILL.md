---
name: parquet-file-layout
version: 1.0.0
description: >
  Organise Parquet datasets with sensible partitioning, file and row-group sizes, sorting and types. Use when lake queries are slow, tiny files pile up, or scans read far more than they need.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - storage
  - performance
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: parquet-file-layout
  official: true
  domain: data
  security_flags: []
---

# Parquet File Layout

## When to use
You are writing or reorganising columnar files that other queries will scan repeatedly.

## Steps
1. List the main query filters and columns read; the layout should serve those.
2. Inspect the current state: file count, size distribution, rows and row groups, and column types. DuckDB's `parquet_metadata()` and `parquet_schema()` or a Parquet library will show them.
3. Partition only on low-cardinality columns that queries filter on, such as date. Avoid user ids and fine-grained timestamps.
4. Aim for files of roughly hundreds of megabytes where volume allows, and adjust to the engine's guidance. If partitions are tiny, coarsen the scheme.
5. Sort within files by a common filter column so row-group min and max statistics can skip data.
6. Set row-group size deliberately: very small groups add overhead, very large ones reduce skipping and need more memory to write.
7. Store real types: timestamps with a defined time zone meaning, decimals for money, no numbers as strings.
8. Pick a compression codec that every reader supports and compare on your data.
9. Compact into a new location, verify counts and checksums, then switch readers. Delete old files only with approval.
10. Time the representative queries and compare bytes read before and after.

## Watch out for
- Rewriting files in place while jobs read them yields missing or duplicate rows; use a table format with atomic commits if the project needs that.
- Files in one dataset with differing column types fail late or read as nulls.
- In table formats, deleting data files by hand corrupts table metadata; use the format's maintenance commands.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Representative queries read measurably less and run faster, file sizes are within the target range, and row counts match the original.
