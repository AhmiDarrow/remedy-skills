---
name: money-calculations
version: 1.0.1
description: >
  Implement money arithmetic with exact types, explicit rounding, currency-aware precision and reconciling totals. Use when code handles prices, tax, discounts, splits, refunds or currency conversion.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - finance
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
  library_id: money-calculations
  official: true
  security_flags: []
---

# Money Calculations

## When to use
Totals are off by a cent, or code that computes amounts is being written or reviewed. Tax and accounting rules themselves need confirmation by a qualified person.

## Steps
1. `grep` the whole path for float types, `parseFloat`, `toFixed` and database float columns, including API serialization and exports.
2. Use integer minor units or a decimal type, with the currency stored beside every amount. Check each currency's minor unit in a maintained ISO 4217 source: not all have two decimals.
3. Construct decimals from strings or integers, not floats. In JSON, send amounts as strings or integers with a documented unit; keep integers within the language's safe range.
4. Write down, with the owner, where rounding happens and which mode: per line or per invoice, tax inclusive or exclusive, discount before or after tax. Do not rely on the library's default.
5. Keep rates and intermediate values at higher precision and round only at the defined points.
6. Allocate splits and prorations so parts sum exactly to the whole, distributing leftover units by a fixed rule.
7. For conversion, record rate, direction, source and time with the transaction. A round trip need not return the original.
8. Refund from the originally charged line amounts, not by recalculating at current prices or rates, and never beyond the remaining total.
9. Test halves, negatives, zero, large values, zero- and three-decimal currencies, many tiny lines, and invariants: parts equal total and refunds never exceed charge.

## Watch out for
- Formatting for display is not rounding for storage.
- Adding amounts in different currencies should raise an error.
- Changing rounding rules must not rewrite historical invoices.
- A payment provider may expect a different unit than your convention for some currencies; check its documentation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No binary floating point remains on the money path, rounding rules are written and approved, and the invariant and edge tests pass.
