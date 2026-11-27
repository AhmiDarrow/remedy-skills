---
name: multi-tenant-isolation
version: 1.0.1
description: >
  Audit a multi-tenant application for cross-tenant reads and writes across queries, caches, jobs, files, search and exports. Use when reviewing SaaS isolation or after a report of seeing another customer's data.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - backend
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: multi-tenant-isolation
  official: true
  security_flags: []
---

# Multi Tenant Isolation

## When to use
Several customers share code and some storage, and one must never reach another's data. If a real leak was reported, preserve logs and tell the incident owner before changing code.

## Steps
1. Write down where tenant identity comes from. It must be derived from the authenticated session and verified membership, never trusted from a header, path or body alone.
2. List every tenant-owned table and store, then every way in: API, GraphQL resolvers, admin tools, webhooks, jobs, reports, imports, websockets.
3. Check enforcement is structural: a scoped repository, ORM default scope or database row security. Search for raw SQL and the calls that bypass the scope.
4. Check lookups by ID, bulk operations and nested references. Creating a record that points at another tenant's parent ID is also a leak. Composite keys including tenant ID can enforce this in the database.
5. With PostgreSQL row security, confirm the application role is not superuser, lacks BYPASSRLS and does not own the tables (or FORCE ROW LEVEL SECURITY is set). With pooled connections, set tenant context per transaction.
6. Follow the data out of the database: cache keys, search filters, vector indexes, object keys and signed links, queue payloads, export files, logs and emails.
7. Check unique constraints and error messages that reveal another tenant's records exist.
8. Add a two-tenant test fixture: for each endpoint, tenant A tries read, list, update and delete on B's objects, and expects denial with B's data unchanged.
9. Report each finding with file, request path, impact and fix. Cross-tenant read or write is normally critical. Check that support access is time-limited and audited.

## Watch out for
- Background jobs often lose request context and run unscoped.
- A tenant prefix on object keys isolates nothing unless access is checked or policy enforced.
- Single-tenant test data lets every unscoped query pass.
- Probe only test tenants you are authorised to use, never real customers' records.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every entry point and secondary store is marked verified, failing or untested, and cross-tenant denial tests run for the verified ones.
