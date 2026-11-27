---
name: budget-snapshot
version: 1.0.1
description: >
  Build a one-month picture of income, bills, everyday spending and goals from figures the user provides. Use when someone asks where their money goes or whether they can afford their month.
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
metadata:
  source: library
  library_id: budget-snapshot
  official: true
  domain: personal
  security_flags: []
---

# Budget Snapshot

## When to use
The user wants a clear view of their monthly money. This organises their figures; it is not financial advice and needs no bank logins.

## Steps
1. Ask for the period, currency and household scope. Accept typed figures or an export the user supplies; ask them to remove account and card numbers. Never ask for passwords, and never sign in to or scrape a bank site.
2. List take-home income by source and date. For irregular income, use a cautious baseline such as the lowest typical month and show better months separately.
3. List fixed commitments with due dates.
4. Convert non-monthly costs to monthly amounts: weekly times 52 divided by 12, fortnightly times 26 divided by 12, annual divided by 12. Prompt for insurance, vehicle, school, gifts, repairs and subscriptions.
5. Group variable spending. From statements, exclude transfers between own accounts, count card purchases or the card payment but not both, and net off refunds.
6. Add debt payments and savings goals as separate lines, noting arrears.
7. Show income minus outgoings, with the arithmetic and each figure marked actual or estimate. If an actual balance does not match, show an unexplained line.
8. Check timing: a month can total positive and still run short before payday. Lay due dates against paydays.
9. If there is a gap or goal, show one to three options with their monthly effect, leaving the choice to the user.
10. If essentials are not covered, or rent, mortgage, energy or tax is in arrears, put that first and suggest a free accredited debt advice service. Save the file only where the user wants it.

## Watch out for
- Filling gaps with "typical" spending presented as theirs.
- Forgetting annual bills, then calling the surplus spare.
- Moralising about purchases.
- Recommending investments, loans or other financial products.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Totals add up from dated or estimated lines, irregular costs and payday gaps are visible, unknowns are listed, and no sensitive details were stored unasked.
