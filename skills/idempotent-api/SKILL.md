---
name: idempotent-api
version: 1.0.1
description: >
  Make a state-changing API operation safe to retry with idempotency keys or natural unique keys, including concurrent duplicates. Use when retries or double clicks can create repeat orders or charges.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - reliability
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
  library_id: idempotent-api
  official: true
  security_flags: []
---

# Idempotent Api

## When to use
A client may repeat a request without knowing whether the first one succeeded.

## Steps
1. Trace all effects of the operation: database writes, messages, emails, external calls.
2. Prefer natural idempotence if available: a unique business key, a client-chosen resource id or a conditional state change. Otherwise accept an idempotency key header generated once per user intention and reused on retries.
3. Scope keys by account and operation. Store a fingerprint of the meaningful request fields; reject the same key with a different request.
4. Claim the key atomically with a unique constraint before doing work. A read followed by an insert lets two requests through.
5. When the effect is only local, commit the claim, the change and the saved response in one transaction.
6. For external effects, keep states such as in progress, succeeded and failed, plus recovery points. Pass a derived idempotency key downstream. Publish messages through an outbox written in the same transaction.
7. Define the concurrent duplicate response: wait briefly or return a conflict that says to retry. Replay the stored status and body after completion.
8. Decide which failures are stored. A validation error or transient failure before any effect may release the key; an unknown outcome must be reconciled, not run again blindly.
9. Recover claims abandoned by a crash with a lease and a check of what actually happened.
10. Set a retention period longer than the longest client or queue retry, document it for clients, and test parallel duplicates, a changed payload, and a crash between each effect and the saved result.

## Watch out for
- An in-memory key store that fails with several instances or after restart.
- Generating a new key inside the retry loop.
- Cached responses revealing data across accounts or after access was removed.
- Believing a key table alone makes an external charge exactly once.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Parallel and repeated requests yield one effect, crash recovery is tested, and key rules and retention are documented.
