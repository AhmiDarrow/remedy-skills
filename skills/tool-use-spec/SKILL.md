---
name: tool-use-spec
version: 1.0.1
description: >
  Specify the contract for a tool a language model can call, including schema, side effects, authorisation, errors and tests. Use when adding a function or tool to an assistant or agent.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - tools
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: tool-use-spec
  official: true
  security_flags: []
---

# Tool Use Spec

## When to use
A model will call code, and wrong, repeated or malicious calls must be handled.

## Steps
1. Read the underlying function or API: what it changes, who may call it, limits and failure modes. Offer a task-level tool, not a raw pass-through to a database, shell or HTTP client.
2. Name it for the action. Describe when to use it, when not to, and how it differs from neighbouring tools.
3. Define a strict input schema with types, units, formats, enums, bounds and required fields, rejecting unknown ones. Supply user identity and tenant from the session, never from model arguments.
4. Validate again in code. For paths, resolve the real path and check it stays under an allowed root; for URLs, check the resolved address and every redirect against internal ranges.
5. Classify the effect: read, reversible write, irreversible, spends money or sends externally. The application, not the model, enforces approval, showing the exact arguments that will run.
6. Define bounded output: only needed fields, pagination or truncation that says so, and ids for follow-up calls. Treat returned external text as untrusted data.
7. Define errors with a code, a plain cause, whether retry can help and what to change. Omit secrets and stack traces.
8. Set timeouts and rate limits. For writes, accept an idempotency key or provide a way to check whether an uncertain call happened. Define cancellation and partial failure.
9. Specify an audit record with caller, arguments redacted as needed, approval and result.
10. Test the handler with invalid, out-of-scope and duplicate calls, then test model tool selection on requests that should and should not use it.

## Watch out for
- Optional parameters with dangerous defaults, such as an empty filter meaning all records.
- Believing a "confirmed: true" argument written by the model.
- Success returned before an asynchronous action has finished.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Schema, effect class, errors and limits are written, and tests show unauthorised, unapproved and repeated calls cannot cause unintended effects.
