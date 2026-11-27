---
name: bug-report-template
version: 1.0.1
description: >
  Turn a vague complaint or observation into a clear bug report with environment, exact steps, expected and actual behaviour, evidence and impact. Use when filing or rewriting an issue someone else must act on.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - docs
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: bug-report-template
  official: true
  security_flags: []
---

# Bug Report Template

## When to use
"It doesn't work" needs to become something a developer can act on.

## Steps
1. Look for the project's issue template and `read` it. Use its fields.
2. Pull what is already known from the conversation, screenshots and logs before asking. Then ask only for gaps: what they were doing, what they saw, what they expected.
3. Collect environment: app version or commit, operating system, browser or device, relevant settings, account role, time with zone, and any request or error ID. Run only read-only version commands.
4. Write steps from a stated starting condition, one action each, with exact inputs using invented data.
5. State expected behaviour with its basis (documentation, previous version, specification, or the reporter's expectation) and actual behaviour with the exact error text.
6. Record reproduction honestly: tried by whom, how many of how many attempts, or not reproduced. Note where it does not happen.
7. Note when it last worked and what changed, as observations.
8. Attach the smallest useful log excerpt or screenshot with tokens, cookies, emails and personal data removed, including from images and URLs.
9. Give impact in facts: who is affected, what is blocked, data loss or security exposure, and workaround. Suggest severity using the project's scale and leave priority to the owner.
10. Title it as symptom plus condition. Keep one bug per report, search for duplicates, and show the draft; the user files it or approves filing.

## Watch out for
- A guessed cause written as fact; put it under a separate hypothesis line.
- A suspected security vulnerability posted publicly; direct it to the project's private reporting channel.
- Paraphrasing error messages, which prevents searching.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Someone with no prior context can follow the report, unknown fields say unknown, reproduction status is stated, sensitive data is removed, and the draft is ready for the user to file.
