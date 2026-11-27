---
name: llm-structured-output
version: 1.0.0
description: >
  Get reliable structured data from a language model with schema constraints, validation, bounded repair and honest unknowns. Use when code parses model replies into JSON or typed objects.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - structured-output
  - reliability
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: llm-structured-output
  official: true
  domain: llm
  security_flags: []
---

# Llm Structured Output

## When to use
A program consumes model output and fails on malformed, missing or invented fields.

## Steps
1. Find the consumer and define only the fields it needs, with types, enums, units and which may be unknown.
2. Check the installed provider or runtime for native schema-constrained output or tool-call arguments, and which schema keywords it really enforces. Use it over prompt-only JSON.
3. Allow honesty in the schema: nullable fields, an `unknown` enum value or an `insufficient_information` result. Required fields with no escape invite fabrication.
4. Describe each field's meaning and edge cases; names alone are ambiguous.
5. Check the finish reason. Truncated output and refusals need their own paths, not JSON repair.
6. Parse with a real parser and validate against the schema in your code.
7. Add semantic checks: ids exist, totals add up, dates are ordered, quoted evidence appears in the input.
8. On failure, retry a fixed small number of times with the validation errors, then return an explicit failure to the caller.
9. Treat the values as untrusted input before they reach SQL, shell, HTML or any action.
10. Test with empty, ambiguous, very long, non-English and hostile inputs, repeating each, and record validity and field accuracy separately.

## Watch out for
- Schema-valid does not mean correct.
- Silently stripping text around JSON or filling defaults hides failures that should be counted.
- Placing a conclusion field before the evidence it depends on can encourage answers decided before extraction.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Invalid output cannot reach the consumer, truncation and refusal are handled, and measured field accuracy meets the stated bar.
