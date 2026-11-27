---
name: docs-api-examples
version: 1.0.1
description: >
  Add tested request and response examples to API documentation for the calls integrators get wrong. Use when readers cannot make a first successful call or examples have drifted from the API.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - api
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
  library_id: docs-api-examples
  official: true
  security_flags: []
---

# Docs Api Examples

## When to use
Reference docs list fields but do not show how real calls fit together.

## Steps
1. Choose the targets from evidence: authentication, the first useful call, support questions, frequent 4xx errors, and flows that need several calls in order.
2. Read the handler, validation rules and tests so each example reflects actual behaviour. Note where this disagrees with the description file.
3. For each, give a complete `curl` request with method, URL, headers and body, stating which shell its quoting is for, then the status, relevant headers and body.
4. Use obvious placeholders such as `$API_TOKEN`, `api.example.com` and sample people like Test User. Never paste captured traffic without replacing every identifier and secret.
5. Show the errors a caller can act on: invalid input, missing permission, conflict and rate limit, each with the fix.
6. For multi-step flows, show which response value feeds the next request. Cover the pagination loop with its stop condition and safe retry with an idempotency key where supported.
7. Run every example against a local or test server in document order and paste the real, redacted output. Mark any trimmed response.
8. Wire the checks into tests: validate example bodies against the schema or replay them in CI.

## Watch out for
- Examples that depend on data the reader does not have; include the call that creates it.
- Running create or delete examples against production.
- Schema-valid examples that business rules reject.
- One huge example with every optional field hides what is required.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each documented example was executed successfully or produced the documented error on a test server, contains no real secret or personal data, and is checked automatically or the gap is stated.
