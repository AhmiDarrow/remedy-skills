---
name: fixture-factory
version: 1.0.1
description: >
  Replace repeated, brittle test setup with small factories that build valid data and expose only what each test cares about. Use when a new required field breaks many tests or setup hides intent.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: fixture-factory
  official: true
  security_flags: []
---

# Fixture Factory

## When to use
Tests repeat large object literals or share one fixture that everything depends on.

## Steps
1. Search for repeated construction of the same types and for shared fixtures that many tests tweak. Run the tests to get a baseline.
2. Use the project's factory library if it has one; otherwise a plain function with overrides is enough.
3. Make the default the smallest valid object. Build it fresh per call, including nested lists and maps, and type overrides so misspelled fields fail.
4. Keep defaults boring and deterministic: sequences for unique values, fixed dates and clock, obviously fake names and `example.com` addresses.
5. Name meaningful variants for domain states (`expired`, `adminUser`) instead of piles of flags. A variant must set all fields that state requires.
6. Separate building in memory from saving to the database, and create related records only when needed.
7. Values a test asserts on must be set visibly in that test, not inherited from a default.
8. Migrate a few representative files, check the same assertions still run and pass in random or isolated order, then migrate the rest if the readability gain holds.

## Watch out for
- Random data makes failures hard to reproduce; if used, print and allow setting the seed.
- Factories that silently build deep object graphs make tests slow and obscure.
- Factory logic copying production calculations lets both be wrong together.
- Tests of invalid input must still be able to bypass validity.
- Do not seed fixtures from real user records.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Migrated tests show only relevant differences, pass individually and together, and a new required field can be defaulted in one place.
