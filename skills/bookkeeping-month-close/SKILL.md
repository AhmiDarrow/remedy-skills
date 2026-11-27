---
name: bookkeeping-month-close
version: 1.0.0
description: >
  Run a small-business month-end close checklist covering reconciliations, missing documents and questions for the accountant. Use when books must be tidied and checked each month.
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
  - bash
  - write
  - todo
metadata:
  source: library
  library_id: bookkeeping-month-close
  official: true
  domain: data
  security_flags: []
---

# Bookkeeping Month Close

## When to use
A month has ended and records need to be complete enough to trust.

## Steps
1. Confirm the period, accounting basis used and the previous close's ending balances.
2. Collect statements for every bank, card, payment processor and loan account.
3. Reconcile each to its statement ending balance; list unmatched items instead of forcing a plug entry.
4. For processor payouts, separate gross sales, fees, refunds and holds from the net deposit.
5. Find duplicates, uncategorised entries, and transfers recorded as income or expense.
6. Match expenses to receipts and list what is missing, with who can supply it.
7. Review open receivables and payables and compare each account with the prior month for unexplained swings.
8. Write questions on owner draws, asset purchases, payroll and sales tax for the accountant. Save reports, and lock the period only on the user's approval.

## Watch out for
- Editing already closed or filed periods without telling the accountant.
- Guessing categories with tax effect.
- A zero difference achieved by offsetting two errors.
- Copying account numbers into notes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each account reconciles or has an itemised difference, and missing documents and accountant questions are listed with owners.
