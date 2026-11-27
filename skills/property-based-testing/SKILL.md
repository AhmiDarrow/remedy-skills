---
name: property-based-testing
version: 1.0.0
description: >
  Test invariants over generated inputs and keep the shrunk counterexamples as regression cases. Use when code such as parsers, serialisers or calculations has too many inputs for hand-picked examples.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - property-testing
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: property-based-testing
  official: true
  domain: testing
  security_flags: []
---

# Property Based Testing

## When to use
Examples cover what you thought of. Generators cover what you did not.
## Steps
1. Use the project's library or the usual one for the language: Hypothesis, fast-check, proptest, jqwik. Check the installed version's API.
2. Choose properties stronger than "does not crash": round trip (decode of encode equals original), invariance (sorting keeps the same items), idempotence (normalising twice equals once), agreement with a slow simple version, or relations between outputs for related inputs.
3. Build generators that produce valid domain values by construction. Filtering random junk wastes runs and skews coverage.
4. Add a second generator for invalid input and assert it is rejected cleanly.
5. Make edge values reachable: empty, huge, duplicates, Unicode including combining marks, negative zero, NaN where the type allows.
6. Run it and inspect the distribution with the library's statistics or classification features to confirm interesting cases occur.
7. On failure, read the shrunk example and decide whether the code, property or generator is wrong.
8. Pin each real counterexample as an explicit example test and keep the printed seed or replay data.
9. Bound the run count so the normal suite stays fast; run longer separately.
## Watch out for
- Re-implementing the function inside the property.
- Narrowing the generator to make a real bug go away.
- Stateful or time-dependent code without reset between cases.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Properties run in the suite, the generator is shown to reach edge cases, and each failure found is fixed or recorded with its counterexample.
