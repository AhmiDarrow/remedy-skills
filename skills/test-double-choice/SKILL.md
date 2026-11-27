---
name: test-double-choice
version: 1.0.0
description: >
  Choose between real objects, fakes, stubs, spies and mocks, and keep doubles honest against the real thing. Use when tests are brittle from mocking or need to isolate a slow or external dependency.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - mocking
  - design
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - write
  - bash
metadata:
  source: library
  library_id: test-double-choice
  official: true
  domain: testing
  security_flags: []
---

# Test Double Choice

## When to use
Tests break on every refactor, or pass while the real integration is broken.
## Steps
1. For each dependency ask whether the real one is fast, deterministic and free of outside effects. If so, use it.
2. For databases or queues, consider a disposable real instance before faking query behaviour.
3. Otherwise choose by what the test must observe: a stub to supply an input, a fake (working in-memory version) for stateful collaborators, a spy or mock only when the outgoing call is itself the behaviour, such as "an email is requested once".
4. Wrap third-party clients in a thin interface you own and double that, not the vendor's surface.
5. Use signature-checked doubles where the language offers them (such as `autospec` in Python's mock) so renamed methods fail.
6. Assert on outcomes and meaningful arguments, not call order or incidental calls.
7. Make doubles able to fail: timeout, error response, partial result.
8. Write one shared behaviour test run against both fake and real implementation, with the real run in a slower tier.
9. Reset shared doubles between tests.
## Watch out for
- Recorded responses that go stale, and recordings containing tokens or personal data.
- Mocks returning mocks several levels deep, a sign the design needs a seam.
- Patching the name where it is defined instead of where it is looked up.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each double has a stated reason, key fakes are checked against the real behaviour, and a behaviour-preserving refactor no longer breaks the tests.
