---
name: medical-bill-review
version: 1.0.0
description: >
  Check a medical or dental bill against what happened and what the insurer processed before paying. Use when a healthcare bill is confusing, high or unexpected.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - health
  - money
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: medical-bill-review
  official: true
  domain: personal
  security_flags: []
---

# Medical Bill Review

## When to use
A bill has arrived and the person is unsure it is right. Billing systems differ greatly by country and plan.

## Steps
1. Request an itemised bill with service dates and billing codes if the one received is a summary.
2. Collect the insurer's explanation of benefits or statement for the same dates, the plan document, receipts for amounts already paid and any estimate or consent signed.
3. Match each line across bill and insurer statement by date, provider and code. Mark matched, missing from insurer, or differing.
4. Flag duplicates, wrong dates, services the person does not recall, wrong personal or policy details, and payments not credited.
5. Check whether the insurer has finished processing. A bill sent before that may not reflect the final amount.
6. Ask by phone or in writing about each flag; log date, name and reference. Ask that the account be held while under review and get that confirmed.
7. Ask the provider about financial assistance, payment plans or self-pay pricing where relevant.
8. For coverage disagreements, find the appeal route and deadline in the insurer's documents.

## Watch out for
- An explanation of benefits is usually not a bill.
- Ignoring the due date while disputing; collections may continue unless a hold is confirmed.
- Guessing what a code means or whether care was necessary; ask the billing office.
- Paying through a link or number in an unverified message.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every line is matched or has a logged query, and the amount to pay or contest is stated with its due date.
