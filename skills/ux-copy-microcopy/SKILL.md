---
name: ux-copy-microcopy
version: 1.0.1
description: >
  Write or revise interface strings such as labels, buttons, hints, confirmations and empty states, with consistent terms and localisation-safe phrasing. Use when UI wording is vague, inconsistent or missing.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - writing
  - ux
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: ux-copy-microcopy
  official: true
  domain: design
  security_flags: []
---

# Ux Copy Microcopy

## When to use
A screen or flow needs words that tell people what things are and what happens next.

## Steps
1. Walk the flow and list every string with `grep` in templates and message catalogs, including placeholders, tooltips, toasts, emails it triggers and accessible names. Record where each appears.
2. For each screen note who is there, what they are trying to do and what they might fear (cost, data loss, publishing).
3. Build a small glossary: one name per object and action. Check what the product and its docs already call them.
4. Label buttons with the outcome, usually verb plus object ("Delete project", "Send invoice"). Avoid "OK", "Submit" and "Yes" where a specific verb fits. Match the dialog title to its button.
5. Keep instructions where they are needed. Format requirements go in visible helper text before the user types, not only in a placeholder or after failure.
6. Write link text and icon-button names that make sense out of context. Keep the visible label inside the accessible name.
7. State consequences that are true: check the code for what is actually deleted, charged, shared or reversible.
8. Respect existing voice and case rules. Cut apologies, jokes in stressful moments and blame on the user.
9. Make strings translatable: whole sentences with named variables, proper plural forms, no concatenated fragments, and room for longer languages.
10. Present a table of current, proposed and reason; edit the files once agreed, keeping translation keys stable or flagging changed sources.

## Watch out for
- "Cancel" as both the dismiss button and the action (cancelling a subscription) is ambiguous; name both outcomes.
- Copy promising something the code does not do.
- Changing strings that tests or automation select by text without updating them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every string in the flow is inventoried and either kept or replaced with a reason, terms match the glossary, consequences are verified, and layout and tests affected by the changes are checked or listed.
