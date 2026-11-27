---
name: pagination-standard
version: 1.0.1
description: >
  Add stable server-side list pagination with a total ordering, opaque cursors and an enforced page size limit. Use when a list endpoint returns everything or pages skip and repeat rows.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - backend
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
  library_id: pagination-standard
  official: true
  security_flags: []
---

# Pagination Standard

## When to use
A list endpoint or query needs to return results in pages.

## Steps
1. Ask how clients use the list: jump to a page number, scroll onward, or sync everything. Check the codebase's existing pagination convention and follow it.
2. Prefer keyset cursors for large or frequently changing data. Offset is acceptable for small, mostly static lists needing page numbers.
3. Define a total order ending in a unique column, such as `(created_at, id)`. Handle nullable sort columns explicitly.
4. Write the next-page condition to match the order exactly. For both descending: `(created_at, id) < (:t, :id)`. Mixed directions need the expanded OR form.
5. Add an index matching filters then sort columns, and confirm with the query plan on realistic volume.
6. Make the cursor opaque and versioned, carrying the sort values and bound to the filters and sort. Validate it as untrusted input and reapply authorization on every page.
7. Set a default and maximum page size on the server; define handling of zero, negative and excessive values.
8. Fetch one extra row to detect another page. Make total counts optional if expensive.
9. Test duplicate timestamps across a page boundary, inserts and deletes between requests, an empty result, the last page and a tampered cursor. Document the contract.

## Watch out for
- Truncating timestamp precision in the cursor skips or repeats rows.
- Sorting by a mutable field such as last update lets items move between pages, so a full sync can miss them.
- Filtering after fetching a page returns short or empty pages that clients read as the end.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Walking all pages of seeded data with tied sort values returns every expected row exactly once, the maximum is enforced, and bad cursors get a clear client error.
