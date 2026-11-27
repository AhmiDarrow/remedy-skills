---
name: data-quality-checks
version: 1.0.0
description: >
  Add targeted checks for freshness, volume, uniqueness, nulls, references and business rules to a dataset, with clear failure actions. Use when bad data reaches reports before anyone notices.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - quality
  - pipelines
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: data-quality-checks
  official: true
  domain: data
  security_flags: []
---

# Data Quality Checks

## When to use
A table or feed matters to decisions or downstream systems and currently has no automated guard.

## Steps
1. List who uses the dataset and which wrong values would hurt them most. Check those first.
2. Profile history: row counts per load, null rates, distinct values, ranges, arrival times, including weekdays, month end and holidays.
3. Use the project's existing test framework (dbt tests, a validation library or SQL assertions) before adding another.
4. Write checks in layers: schema and types; primary key unique and not null; referential matches; allowed values and ranges; freshness of the newest event time as well as load time; volume against comparable periods; reconciliation to the source; domain rules such as header total equals sum of lines.
5. Assign each check an action: block publication, quarantine offending rows, or warn.
6. For blocking checks, validate in staging and swap in only on pass, leaving the last good version visible with its date.
7. Derive thresholds from history and note why each was chosen.
8. Make a failure message show the check, period, expected and actual values, and a query returning sample bad rows.
9. Run the checks over past data to see how often they would have fired, and tune.
10. Inject known bad rows in a test to prove each blocking check fails.

## Watch out for
- Dozens of noisy warnings train people to ignore the one that matters.
- A check that passes on zero rows hides an empty load.
- Silently dropping bad rows makes totals wrong with no trace; count and keep quarantined records.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Injected faults are caught with the intended action, historical replay shows a tolerable alert rate, and each alert has an owner.
