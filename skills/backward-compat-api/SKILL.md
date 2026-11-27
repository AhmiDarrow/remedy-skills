---
name: backward-compat-api
version: 1.0.1
description: >
  Evolve a published API without breaking existing clients by classifying each change, using expand and contract, and testing old clients. Use when adding or changing fields, parameters or behaviour.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - release
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
  library_id: backward-compat-api
  official: true
  security_flags: []
---

# Backward Compat Api

## When to use
Callers you cannot upgrade in lockstep use an API you need to change. For removing something on a schedule, use the deprecation skill after this.

## Steps
1. Write the change as before and after requests and responses, including defaults, errors and ordering.
2. Classify it from both directions. Usually safe: a new endpoint, a new optional request field with the old behaviour as default, a new response field. Breaking: removing or renaming, changing type or unit, a new required input, tighter validation, changed default, different status or error code.
3. Check the risky "additive" cases: a new response enum value, a field that can now be null or absent, longer ids, changed sort order or page size. Strict clients fail on these.
4. Learn what real clients do: read your own SDKs and consumer code, and sample logged requests for inputs that stricter rules would reject.
5. Prefer expand then contract: add the new form beside the old, accept both, define which wins when both arrive, keep them consistent in storage, then migrate callers.
6. Add a new version only when both shapes cannot coexist. State how long the old one lives and who maintains it.
7. Run the previous release's contract tests or client against the new server, and diff the API description with a breaking-change checker if the project has one.
8. Record the change in the changelog with any action a caller must take.

## Watch out for
- Same schema, different meaning: switching cents to whole units passes every diff tool.
- Fixing a bug that clients rely on is still a break; measure before changing.
- During rolling deploys old and new servers answer the same client, and a rollback must read data the new code wrote.
- Old mobile releases stay in use long after an update ships.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each change is labelled safe, risky or breaking with the reason, old-client tests were run or named as missing, and every break has a coexistence or versioning plan.
