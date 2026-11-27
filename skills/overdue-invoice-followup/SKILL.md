---
name: overdue-invoice-followup
version: 1.0.0
description: >
  Reconcile unpaid invoices and draft staged, factual payment reminders for the user to send. Use when a small business has money owed and needs a calm follow-up process.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - small-business
  - finance
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - mail.list
  - calendar.create_event
metadata:
  source: library
  library_id: overdue-invoice-followup
  official: true
  domain: content
  security_flags: []
---

# Overdue Invoice Followup

## When to use
Invoices are past due or about to be.

## Steps
1. Build an ageing list: invoice number, client, amount, currency, due date, days overdue, last contact.
2. Reconcile against payments, credits and part payments before chasing anyone.
3. Check the thread for disputes, delivery problems or agreed new dates; handle those first.
4. Confirm the invoice reached the right billing contact with any required order reference.
5. Draft by stage: friendly reminder, firmer follow-up with a date, then a final notice stating only steps the user will actually take.
6. Each draft lists invoice number, amount outstanding, due date and approved payment route.
7. Mention late fees or interest only if terms and applicable law support them; have that checked.
8. Log promises and set follow-up dates. The user sends, and decides on escalation or collection.

## Watch out for
- Chasing a paid invoice.
- Changing bank details because an incoming email asked; verify through a known contact, since this is a common fraud.
- Threats, public shaming or contacting unrelated third parties.
- Totalling mixed currencies.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The list matches payment records, disputed items are separated, and each remaining invoice has a staged unsent draft and next date.
