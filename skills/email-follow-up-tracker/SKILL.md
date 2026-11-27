---
name: email-follow-up-tracker
version: 1.0.0
description: >
  Find sent requests and received promises that have gone quiet and prepare follow-ups. Use when the user asks who has not replied or what they are still waiting for.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - email
  - follow-up
kind: native
status: discovered
tools:
  - mail.list
  - mail.send
  - calendar.list_events
  - memory.search
  - write
metadata:
  source: library
  library_id: email-follow-up-tracker
  official: true
  domain: personal
  security_flags: []
---

# Email Follow Up Tracker

## When to use
Things are slipping because nobody is tracking replies.

## Steps
1. Set the lookback window and which kinds of thread count.
2. From sent mail, pick messages that asked a question, requested something or expected confirmation. Ignore thank-yous and information-only notes.
3. Check the whole thread, and search the person's address and topic for answers sent as new messages.
4. Check calendar entries and automatic replies that may explain silence or already resolve the item.
5. Also list promises others made ("I will send it Thursday") and ones the user made that are open.
6. Record per item: person, exact ask, date sent, expected date, status, next check.
7. Suggest timing from the real deadline and relationship rather than a fixed number of days.
8. Draft each follow-up in the same thread: restate the specific ask, give the date that matters, offer an easy way to answer. Keep blame out.
9. Show drafts and recipients; send only the ones the user approves one by one or as a reviewed list.

## Watch out for
- A reply may have arrived at another address or through another channel; ask before chasing something important.
- Repeated nudges to someone who has not engaged become harassment. After a couple, suggest another route or dropping it.
- Do not reply-all when only one person owes an answer.
- Stale trackers cause embarrassing follow-ups, so recheck the thread just before sending.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each open item has evidence that it is unanswered, a next date and, where wanted, a draft that has not been sent without approval.
