---
name: expense-categorize
version: 1.0.1
description: >
  Categorise an expense list or bank export, total it by category and flag duplicates, odd amounts and unclear items. Use when someone shares transactions and asks where the money went or needs them sorted for records.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - finance
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: expense-categorize
  official: true
  domain: personal
  security_flags: []
---

# Expense Categorize

## When to use
A pasted list, CSV or statement export needs consistent categories and reliable totals.

## Steps
1. Work on a copy. Ask the purpose (personal view, reimbursement, accountant), the period and any existing category list.
2. Inspect the file: delimiter, encoding, header rows, decimal separator, day-month order, currency, and whether spending is negative or in a separate debit column.
3. Record row count and net sum before changing anything.
4. Separate transfers between own accounts, card repayments, cash withdrawals and savings moves; counting them double-counts spending. Net refunds against their original category.
5. Define a short category list with one rule each, then apply merchant rules consistently. Save the merchant-to-category table for next time.
6. Marketplaces, supermarkets and payment processors can hide mixed purchases. Put unclear rows in "needs review" and ask in one batch; do not guess.
7. Compute totals with a script in `bash`, never by mental arithmetic. Keep currencies separate unless the user gives rates or the file shows converted amounts.
8. Flag same-amount repeats close together, changed recurring prices, unfamiliar merchants and unusually large items. For an unrecognised charge, suggest contacting the bank promptly.
9. Reconcile: category totals plus excluded rows must equal the starting net. Then report totals, largest merchants and open questions.

## Watch out for
- Two identical rows may be two real purchases; flag, do not delete.
- Whether something is deductible or reimbursable depends on local rules or policy. Leave that to the policy, tax authority or accountant.
- Echoing full account or card numbers in output.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every row is categorised, excluded or marked for review, and the totals reconcile to the original sum.
