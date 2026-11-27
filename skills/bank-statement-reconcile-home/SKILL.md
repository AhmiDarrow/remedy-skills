---
name: bank-statement-reconcile-home
version: 1.0.0
description: >
  Reconcile household bank and card statements against receipts to catch errors, duplicates and unknown charges. Use for a monthly money check or when a balance looks wrong.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - money
  - records
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: bank-statement-reconcile-home
  official: true
  domain: personal
  security_flags: []
---

# Bank Statement Reconcile Home

## When to use
The person wants confidence every transaction is real and accounted for.

## Steps
1. Take exported statements or CSV files for one closed period. Keep originals unchanged and work on a copy.
2. Check completeness: opening balance plus credits minus debits equals closing balance. If not, rows are missing, duplicated or signed wrongly; fix that before anything else.
3. Detect sign conventions and date formats per bank, especially day-month order.
4. Pair transfers between own accounts, including card repayments, so they are not counted as spending or income.
5. Match receipts and expected bills by amount and a small date window. Pending and posted entries are the same purchase.
6. List unmatched items: unknown merchant, repeated amount, changed subscription price, expected refund not arrived, foreign fees.
7. For unknowns, check the statement descriptor and ask others in the household before calling it fraud.
8. For a charge nobody recognises, tell the person to contact the bank at once using the number on the card; reporting windows matter.

## Watch out for
- Small test charges before larger fraudulent ones.
- Merchant names that differ from the shop sign.
- Spreadsheet imports dropping leading zeros or swapping dates.
- Never ask for online banking passwords or full card numbers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Balances tie out to the statement, and each unmatched transaction has an explanation or a reporting action.
