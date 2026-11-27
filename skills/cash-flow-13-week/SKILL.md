---
name: cash-flow-13-week
version: 1.0.0
description: >
  Build a 13-week cash forecast from real balances, expected receipts and payments, then compare it with actuals. Use when a small business needs to see a cash squeeze coming.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - small-business
  - finance
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: cash-flow-13-week
  official: true
  domain: data
  security_flags: []
---

# Cash Flow 13 Week

## When to use
The owner needs week-by-week visibility of cash, which a profit report does not give.

## Steps
1. Start with the reconciled available cash on a stated date, listing restricted or tax-reserved money separately.
2. Make weekly columns for thirteen weeks and rows for receipts and payments.
3. Place receipts in the week cash is likely to arrive, using each customer's payment history; label unsigned sales separately and leave them out of the base case.
4. Place payroll, rent, suppliers, loan payments, tax dates, and annual or quarterly bills in their real weeks. Scan a year of statements for irregular ones.
5. Compute opening + receipts - payments = closing, carried forward with formulas.
6. Mark weeks below the owner's minimum buffer.
7. Add a downside case such as the largest customer paying late.
8. Each week enter actuals, explain big variances and roll forward one week.

## Watch out for
- Booking invoices on their issue or due date as if paid.
- Counting a credit line as cash.
- Overtyping formulas with numbers.
- Giving financing or tax advice; take those questions to an accountant.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Opening cash ties to a dated statement, formulas roll correctly, low weeks are flagged and assumptions are listed.
