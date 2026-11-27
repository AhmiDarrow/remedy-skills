---
name: search-indexing
version: 1.0.1
description: >
  Build in-app keyword search and keep its index in step with the database, with permissions and measured relevance. Use when adding search or when results are missing, stale, leaked or badly ranked.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - search
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
  library_id: search-indexing
  official: true
  security_flags: []
---

# Search Indexing

## When to use
An application needs search over its own records, or its current search misbehaves.

## Steps
1. Collect 20 or more real or representative queries with the results that should appear, including typos, partial words, codes, names and every language used. This is the relevance test set.
2. Note data size, freshness need and features required. Start with the database's full-text search if it covers them; add a separate engine only for a stated gap.
3. Define the indexed document: fields, weights, language analyzers, exact-match fields for identifiers, and filter fields such as tenant and visibility.
4. Enforce permissions inside the search query, not by filtering one page afterwards. Never accept tenant filters from the client.
5. Sync through committed changes, using an outbox, change stream or database-maintained index rather than a best-effort second write. Handle deletes, permission changes and edits to related records that are copied into the document.
6. Version each update so an older event cannot overwrite a newer one.
7. Write a resumable full rebuild into a new index, apply changes arriving during it, verify counts and test queries, then switch an alias or pointer.
8. Run the test set, record the rank of expected results, and tune one setting at a time.
9. Monitor indexing lag, failures and zero-result queries without logging sensitive search text unnecessarily.

## Watch out for
- Default stemming and stop words can destroy product codes and short names.
- Counts, facets and suggestions can leak hidden records.
- A user who just saved an item expects to find it; show indexing delay honestly or read it directly.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The test queries meet an agreed result, create, edit, delete and revoke reach search within the stated lag, and a rebuild has been run successfully.
