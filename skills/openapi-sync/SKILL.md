---
name: openapi-sync
version: 1.0.1
description: >
  Bring an OpenAPI description back in line with the implemented routes and flag breaking changes. Use when the spec has drifted from the code or an endpoint changed without a spec update.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - docs
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: openapi-sync
  official: true
  security_flags: []
---

# Openapi Sync

## When to use
The API description and the running service no longer agree, or you need to prove they do.

## Steps
1. Find the source of truth: annotations or schemas that generate the file, or a hand-written file the code follows. Check CI. For generated specs, edit the source and regenerate with the pinned command.
2. Keep a copy of the published version as the baseline.
3. Inventory real routes from the router or framework route listing, including mounted prefixes, and compare method and path with the spec in both directions. Decide with the owner whether internal routes belong.
4. For each shared operation compare parameters, required fields, types, nullability, enums, auth requirements, status codes, error bodies and pagination against handlers and validators.
5. Where code and spec disagree, decide which is the intended behaviour. A code bug should be reported, not written into the contract.
6. Run the project's spec validator or linter, and send test requests to a local server for the changed operations, checking responses against the schemas.
7. Diff against the baseline with a breaking-change checker if one is available, and also review by hand for removed operations, renamed `operationId`, new required inputs and changed meaning.
8. List breaking changes with the caller action needed, and add a CI check that fails on future drift.

## Watch out for
- Generators omit what they cannot infer: middleware errors, auth and headers.
- A huge reorder-only diff hides real changes; keep output ordering stable.
- OpenAPI 3.0 and 3.1 express nullability differently; stay in the file's version unless asked to upgrade.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The spec validates, route inventories match apart from listed exclusions, changed operations were checked against real responses, and breaking changes are reported.
