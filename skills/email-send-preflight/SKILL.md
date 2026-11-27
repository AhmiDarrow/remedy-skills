---
name: email-send-preflight
version: 1.0.0
description: >
  Check recipients, thread, attachments and claims immediately before an email goes out. Use before sending any message that is external, sensitive, widely addressed or hard to take back.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - email
  - safety
kind: native
status: discovered
tools:
  - mail.list
  - mail.send
  - read
metadata:
  source: library
  library_id: email-send-preflight
  official: true
  domain: personal
  security_flags: []
---

# Email Send Preflight

## When to use
A draft is ready and a mistake would be costly.

## Steps
1. Show the final From, To, Cc, Bcc, subject, body and attachment list together.
2. Resolve each recipient to a full address and compare with prior correspondence. Same display names and look-alike domains are the usual traps.
3. Decide reply versus reply-all versus new message. Check for mailing lists and group addresses hiding many people.
4. Read the quoted history and forwarded attachments as if the newest recipient were reading them.
5. Open each attachment: right version, no hidden sheets, comments, tracked changes or other people's data.
6. Match the text against attachments: any "attached" without a file, dead link or private-access share.
7. Verify names, dates, times with zone, amounts and commitments against their sources.
8. Search for placeholders and drafting notes.
9. Suggest Bcc when recipients should not see each other, then ask for explicit approval of this exact version. Any edit means showing it again.
10. Send once, then confirm the result from the tool response.

## Watch out for
- If sending times out, check the sent folder before retrying to avoid duplicates.
- Approval to draft is not approval to send.
- Recall features are unreliable; treat sending as irreversible.
- Never include passwords in mail, and never change payment instructions on the strength of an incoming email.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user approved the exact final message and the send is confirmed, or nothing was sent and the open issue is stated.
