---
name: tax-document-gather
version: 1.0.0
description: >
  Assemble the documents and figures needed for a personal tax return or an accountant, and show what is missing. Use when tax season starts or an accountant asks for paperwork.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - money
  - paperwork
kind: native
status: discovered
tools:
  - read
  - write
  - glob
  - mail.list
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: tax-document-gather
  official: true
  domain: personal
  security_flags: []
---

# Tax Document Gather

## When to use
A return needs preparing and the evidence is scattered. This is collection, not tax advice.

## Steps
1. Confirm country, region, tax year (it may not match the calendar year) and who is filing. Get the deadline from the tax authority's own site.
2. Ask for last year's return and accountant checklist; each source on it is a candidate this year.
3. Ask about changes: job, self-employment, rental income, sales of assets, foreign accounts or income, marriage, separation, children, home purchase or sale, study, large medical or charitable spending.
4. Build a checklist grouped into identity, income, interest and investments statements, business records, possible deductions with proof, payments already made.
5. Search folders with `glob` and mail with `mail.list` for issued statements. Record filename and issuer next to each row.
6. Mark each row received, requested, expected later with date, or not applicable with reason.
7. Create a list of questions for the professional wherever deductibility or treatment is uncertain.
8. Share through the accountant's secure channel; the person uploads or sends.

## Watch out for
- Corrected statements arriving after the first version; keep both and label them.
- Totalling documents in mixed currencies without a stated method.
- Identity numbers and statements sent by ordinary email.
- Declaring something deductible. List it as a question.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every checklist row has a status, every received item has a file, and open tax questions are listed for a qualified person.
