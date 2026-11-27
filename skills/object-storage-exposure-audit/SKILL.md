---
name: object-storage-exposure-audit
version: 1.0.0
description: >
  Audit object storage buckets for public or over-shared access across account settings, policies, ACLs and shared links. Use when checking that no private data is reachable from the internet.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - cloud
  - storage
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - web.fetch
metadata:
  source: library
  library_id: object-storage-exposure-audit
  official: true
  domain: security
  security_flags: []
---

# Object Storage Exposure Audit

## When to use
You own storage buckets and need to know exactly what outsiders can reach.

## Steps
1. Enumerate buckets across every account, project and region, with an owner and intended audience for each.
2. Check account or organisation-wide public access blocks, then per-bucket overrides.
3. For each bucket, read all access paths: bucket policy, legacy ACLs, per-object ACLs where enabled, access points, CDN origin access and cross-account grants.
4. Treat grants to "all users" and to "any authenticated user" as public; the second means any account on that provider, not your staff.
5. Verify from outside with no credentials: request a known object and try listing. Only test your own buckets.
6. For intended public content, confirm only that content is in the bucket and listing is off. Prefer a private bucket behind a CDN with origin authentication.
7. Review how presigned or shared-access URLs are generated: lifetime, who can request them, whether they end up in logs.
8. Check versioning, encryption, access logging and lifecycle rules.
9. Present changes with the consumers each could break, apply after approval, and retest from outside.

## Watch out for
- Blocking public access instantly breaks websites and downloads that relied on it; check request logs first.
- A private bucket can still leak through a public CDN that serves all its paths.
- Old versions and backup copies may hold data removed from the current object.
- If sensitive data was public, review logs for access and escalate instead of quietly fixing it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every bucket has a stated audience that matches an unauthenticated test result, and any past exposure found has been reported to the owner.
