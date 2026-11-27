---
name: orm-n-plus-one-fix
version: 1.0.0
description: >
  Find endpoints that issue one query per row through an ORM and fix them with the right loading strategy and a query-count test. Use when a list page slows down as its row count grows.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: orm-n-plus-one-fix
  official: true
  domain: backend
  security_flags: []
---

# Orm N Plus One Fix

## When to use
Response time grows with the number of items returned, or logs show the same query repeated with different ids.

## Steps
1. Turn on SQL logging or a query counter in development and call the slow endpoint with 1 row and with 50. A count that grows with rows confirms it.
2. Group the logged statements by shape and map each repeated one to the line that triggers it. Look at serializers, templates, computed properties and permission checks, not only the handler.
3. Choose per relation. To-one: join in the same query (`select_related`, `joinedload`, `include` or the ORM's equivalent). To-many: a second query with `IN (...)` (`prefetch_related`, `selectinload` or equivalent). Check the names for the installed ORM version.
4. For counts and sums, aggregate in one grouped query instead of loading children to count them.
5. For resolvers that cannot see the whole list, such as GraphQL fields, batch with a per-request data loader.
6. Rerun with 1 and 50 rows and compare both query count and total time.
7. Add a test asserting the query count stays constant as rows increase.
8. Where the ORM allows it, make unexpected lazy loads raise in tests for this path.

## Watch out for
- Joining two to-many relations at once multiplies rows (10 comments times 10 tags is 100 rows per post) and can be slower than the original.
- Filtering or re-ordering a prefetched relation in a loop usually issues new queries and discards the prefetch.
- A data loader cached across requests leaks one user's data to another.
- Very large `IN` lists have driver or planner limits; paginate the parent query first.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The query count is the same for 1 and 50 rows, a test enforces it, and measured time improved.
