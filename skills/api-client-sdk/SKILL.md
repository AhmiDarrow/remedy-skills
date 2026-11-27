---
name: api-client-sdk
version: 1.0.1
description: >
  Generate or refresh a typed API client from an OpenAPI description, reviewable and safe for its consumers. Use when building or updating an SDK or hand-maintaining request types has drifted.
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
  library_id: api-client-sdk
  official: true
  security_flags: []
---

# Api Client Sdk

## When to use
Callers need a typed client for an HTTP API that has an OpenAPI description, or an existing generated client is stale.

## Steps
1. Find how the client is produced today: `grep` build scripts and CI for the generator name, its config file and pinned version. Reuse them. A different generator or version rewrites every file and hides the real change.
2. Validate the description with the project's linter and compare it with the running API for the endpoints that matter. Fix the source, never the generated output.
3. Check what drives naming: missing or duplicate `operationId` values give unstable method names. Inline anonymous schemas produce throwaway type names; move them to named components.
4. Generate into a dedicated directory from a clean state, so deleted operations leave no orphan files. Do not mix hand-written code into it.
5. Put authentication, base URL, timeouts, retries and error mapping in a thin hand-written wrapper. Retry only idempotent calls.
6. Read the diff of the public surface: removed or renamed methods and types, newly required parameters, changed nullability, new enum values.
7. Compile or type-check the client and its real consumers, then smoke-call the critical operations against a local or test server, including one error response and one paginated one.
8. Choose the version bump from step 6, write migration notes for each break, and commit or package as the repository already does. Publishing waits for the user's approval.

## Watch out for
- Hand edits in generated files vanish on the next run.
- Strict enum decoding in clients can crash when the server adds a value.
- Optional and nullable are different; check how the generator represents each.
- A type check proves nothing about what the server actually returns.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The client regenerates reproducibly with the pinned tool, consumers type-check, the smoke calls ran with results shown, and breaking changes are listed or stated as none.
