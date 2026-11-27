---
name: graphql-schema-review
version: 1.0.1
description: >
  Review a GraphQL schema and resolvers for field-level authorization, query cost abuse, N+1 loading, nullability and breaking changes. Use when schema or resolver changes are about to ship.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - graphql
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: graphql-schema-review
  official: true
  security_flags: []
---

# Graphql Schema Review

## When to use
Types, fields or mutations are being added or changed.

## Steps
1. Diff the schema and list changed types with their resolvers and data sources.
2. Trace authorization to the data layer. A field can be reached through many parents and through global `node` lookups, so a check on the top-level query alone is insufficient.
3. Check mutations verify ownership of every id in the input and allowlist writable fields.
4. Find resolvers inside lists that query per item. Batch with a data loader created per request; a shared loader can serve one user's cached data to another. The batch function must return results in key order, with gaps for misses.
5. Bound cost: lists paginated with a maximum page size, plus depth and complexity limits that account for page size. Consider aliases and batched operations, which can repeat a login attempt many times in one HTTP request.
6. Review nullability: a non-null field that errors nulls its nearest nullable parent. Mark non-null only what can always be produced.
7. Check design: mutation inputs and payloads that can gain fields, expected business errors modelled consistently, specific types over free-form JSON.
8. Compare with the published schema using the project's checker. Removed fields, new required arguments and tighter nullability break clients; new enum values can too. Deprecate with a reason and measure field use before removal.
9. Check production error masking, and report findings with the query that demonstrates each.

## Watch out for
- Disabling introspection is not access control.
- Rate limiting by HTTP request misses expensive single queries.
- Responses cached without the viewer in the key.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each changed field has its authorization path and data-loading behaviour verified or reported, limits are confirmed, and breaking changes are listed.
