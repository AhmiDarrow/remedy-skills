---
name: contract-test-api
version: 1.0.1
description: >
  Add contract tests between an API and its consumers so breaking request or response changes fail before deployment. Use when separately released services or clients keep breaking each other.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - api
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: contract-test-api
  official: true
  security_flags: []
---

# Contract Test Api

## When to use
Producer and consumers change or deploy independently.

## Steps
1. Inventory consumers and the fields, status codes and error shapes each really uses, from code and logs. Note old mobile or external clients you cannot update.
2. Choose by situation. Known internal consumers: consumer-driven contracts such as Pact. Public or unknown consumers: a versioned OpenAPI or protocol schema with response validation and a breaking-change diff. Use what the repository already has.
3. For consumer-driven tests, exercise the real client code against the contract mock, specify only what the consumer needs, and match types or patterns rather than incidental values.
4. Verify the provider against those contracts with the real routing and serialisation. Create each named provider state with controlled data; stub only downstream services.
5. For schemas, validate actual responses in provider tests, so the document cannot drift, and compare the new schema with the released one using a breaking-change checker such as `oasdiff` or, for Protobuf, `buf breaking`.
6. Include errors, authentication failure, nulls, optional fields and pagination.
7. Check compatibility against versions currently deployed, not just the latest branch. A Pact broker with deployment records and `can-i-deploy` does this.
8. Run in CI on both sides and block the merge or deploy. Prove it by removing a used field on a throwaway branch.

## Watch out for
- Exact-value contracts that fail whenever test data changes.
- A new enum value, newly required request field or tighter validation can break clients even though nothing was removed.
- Contracts do not test business correctness or performance.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A deliberately breaking change fails the check, critical interactions are verified against the real provider, and uncovered consumers are listed.
