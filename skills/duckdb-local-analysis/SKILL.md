---
name: duckdb-local-analysis
version: 1.0.0
description: >
  Analyse large CSV, JSON or Parquet files locally with DuckDB SQL, with explicit typing and verified loading. Use when files are too big or awkward for a spreadsheet or in-memory dataframe.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - analysis
  - sql
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: duckdb-local-analysis
  official: true
  domain: data
  security_flags: []
---

# Duckdb Local Analysis

## When to use
You have data files on disk and want to query, join or summarise them without setting up a database server.

## Steps
1. Check availability with `duckdb --version` (or the project's Python package) and ask before installing. Treat the source files as read-only.
2. Peek first: `DESCRIBE SELECT * FROM 'data.csv';` and a small `LIMIT`.
3. Do not trust sniffed types for identifiers, dates or mostly-empty columns. Use `read_csv` with explicit options such as `types`, `delim`, `header` and `dateformat`, or `all_varchar = true` and cast yourself.
4. Count what loaded and compare with the file, allowing for headers and quoted multiline fields. Do not use `ignore_errors` without reporting how many rows were dropped and why.
5. Read many files with a glob, adding `filename = true` for lineage and `union_by_name = true` when columns differ in order or presence.
6. Profile with `SUMMARIZE SELECT * FROM ...;`.
7. For repeated work, load into a `.duckdb` file or convert once with `COPY (...) TO 'out.parquet' (FORMAT parquet);`.
8. Use `TRY_CAST` to find bad values and list them before excluding any.
9. For memory pressure, set `memory_limit` and a temp directory, and select only needed columns.
10. Save the SQL as a script that reproduces every number reported.

## Watch out for
- Shell quoting differs between PowerShell and POSIX shells; run a `.sql` file to avoid mangled quotes.
- Row order is not guaranteed without `ORDER BY`.
- Type detection from a sample can fail far down a file or between files.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A saved script rebuilds the results from the untouched inputs, and loaded, rejected and filtered row counts are reported.
