---
name: js-number-precision-bugs
version: 1.0.0
description: >
  Fix JavaScript bugs from floating point numbers, large integer IDs and silent type coercion. Use when IDs change in transit, totals are off, or comparisons behave oddly.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - javascript
  - debugging
  - data
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: js-number-precision-bugs
  official: true
  domain: backend
  security_flags: []
---

# Js Number Precision Bugs

## When to use
Values differ slightly between server and client, or identifiers from another system stop matching.
## Steps
1. Log the raw wire text next to the parsed value. If digits change at `JSON.parse`, the integer exceeds `Number.MAX_SAFE_INTEGER` (2^53 - 1).
2. For identifiers, transport them as strings from the producer. Converting to `BigInt` after parsing is too late because precision is already lost.
3. Check database drivers: 64-bit and decimal columns are returned as strings by some and lossy numbers by others. Read the installed driver's setting.
4. When mixing `BigInt`, note arithmetic with Number throws, and `JSON.stringify` throws on BigInt unless you serialize it yourself.
5. For decimal quantities, store integer minor units or use a decimal library; do not patch with `toFixed`, which returns a string and has its own binary rounding surprises.
6. Compare computed floats with a tolerance scaled to the magnitude, not bare `===` and not a blind `Number.EPSILON`.
7. Replace `parseInt` on user input with a strict check: `parseInt("12abc")` gives 12, while `Number("")` gives 0. Reject empty strings, then use `Number.isFinite` or `Number.isSafeInteger`.
8. Watch bitwise operators: `x | 0` truncates to 32 bits and corrupts timestamps in milliseconds.
9. Add tests with the boundary values: 9007199254740993 as a string ID, 0.1 + 0.2, negative zero, NaN and an empty field.
## Watch out for
- `NaN` is not equal to itself and passes through arithmetic silently until it reaches storage as null.
- Default `Array.prototype.sort` compares as strings, so 10 sorts before 9; pass a comparator.
- Fixing only the client leaves other consumers of the same API still losing digits.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The boundary tests pass end to end, from wire format through storage and back, with identical values.
