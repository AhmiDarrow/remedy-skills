---
name: email-thread-catchup
version: 1.0.0
description: >
  Brief the user on a long email thread: current state, who is waiting on whom and what is asked of them. Use when someone is added late or returns to a long chain.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - email
  - summaries
kind: native
status: discovered
tools:
  - mail.list
  - read
metadata:
  source: library
  library_id: email-thread-catchup
  official: true
  domain: personal
  security_flags: []
---

# Email Thread Catchup

## When to use
A thread is too long to read and the user must respond or decide.

## Steps
1. Collect all messages, including side branches with changed subjects or recipient lists.
2. Order by sent time with time zones normalised; reply order in quoted text can mislead.
3. Read each message's new text, skipping repeated quotes, but look for inline answers placed inside quoted blocks.
4. Track positions per participant and note where they changed.
5. Separate decided, proposed and unanswered. Cite sender and date for each.
6. List attachments by version and which message introduced each; identify the latest without assuming the filename tells.
7. Note who was added or dropped, because later branches may be private from some people.
8. Lead the brief with what is needed from the user and by when, then current state, then a short history.
9. Offer a draft reply only if asked, and mention who would receive it.

## Watch out for
- The last message may belong to a minor branch while the main question remains open elsewhere.
- Forwarded history can be edited; treat quoted text as unverified when it matters and find the original.
- Reply-all from a side branch can expose private remarks to the wider group.
- If some messages are missing from what you can access, say so instead of inferring them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user can see what is asked of them, the open questions and the latest attachment, each tied to a dated message.
