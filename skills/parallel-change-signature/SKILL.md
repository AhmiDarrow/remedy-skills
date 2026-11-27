---
name: parallel-change-signature
version: 1.0.0
description: >
  Change a widely used function, type or interface through expand, migrate and contract so the build never breaks. Use when a signature change has too many callers to update in one safe step.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - refactoring
  - compatibility
kind: native
status: discovered
tools:
  - grep
  - read
  - edit
  - bash
metadata:
  source: library
  library_id: parallel-change-signature
  official: true
  domain: backend
  security_flags: []
---

# Parallel Change Signature

## When to use
Dozens of callers, several teams or external consumers, and a big-bang edit would conflict with everyone.
## Steps
1. Find all callers and implementers, including tests, mocks, generated code and dynamic calls.
2. Expand: add the new form beside the old (new method, optional parameter, overload or adapter). Implement the logic once; make the old form delegate to the new.
3. Choose defaults in the old path that reproduce current behaviour exactly, and test that.
4. For interfaces with outside implementers, provide a default implementation or a second interface so they still compile.
5. Mark the old form deprecated with the language's mechanism and a message naming the replacement.
6. Migrate callers in reviewable batches by area. Each batch builds and passes alone.
7. Block new uses of the old form with a lint rule or an allowlist test that only shrinks.
8. Contract: when search and, for runtime paths, a usage log show no remaining use, delete the old form and the temporary glue.
## Watch out for
- Two independent implementations that drift during migration.
- A new optional parameter whose default quietly changes behaviour for existing callers.
- Never finishing: record the contract step as a tracked task when you expand.
- Removing a public symbol that external users still need without a versioning decision.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every commit built and passed, all callers use the new form, and the old one is deleted or has a recorded removal condition.
