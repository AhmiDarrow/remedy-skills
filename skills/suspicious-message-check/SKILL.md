---
name: suspicious-message-check
version: 1.0.0
description: >
  Judge whether a text, email, call, QR code or job offer is a scam, and verify it without touching it. Use when someone asks if a message, caller or offer is genuine.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - scam
  - safety
kind: native
status: discovered
tools:
  - read
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: suspicious-message-check
  official: true
  domain: personal
  security_flags: []
---

# Suspicious Message Check

## When to use
Something unexpected asks for money, data, a login, a code, an install or urgent action.

## Steps
1. First ask what has already happened: clicked, entered details, paid, installed, shared a code or allowed remote access. If any, switch to damage control at once: contact the bank or provider on a known number.
2. Ask for pasted text or a screenshot. Do not open its links, attachments or QR targets, even with `web.fetch`, and do not call or reply to its numbers. Use web tools only to find official sites and public scam warnings, and keep the person's details out of searches.
3. Identify the ask and the pressure: deadline, threat, prize, secrecy, a relative in trouble, a changed payment account, a request to move to another app.
4. Read the real sender address and the host of any link: the text after `//` up to the next `/`, ignoring anything before an `@`. Read it from the right to find the registered domain, usually the last two labels, or three under endings such as `.co.uk`. Look for swapped letters and a brand name placed in a subdomain.
5. Verify through a separate route: the number on the card, an address typed by hand, an old saved contact. For family emergencies, call the person or use an agreed family question.
6. For job offers, check the vacancy on the employer's own site. Upfront fees, equipment cheques, tasks that need deposits and moving parcels or money are serious red flags.
7. Give a verdict of likely scam, suspicious, or verified through a named independent route, with the clues. Say how to report it locally.

## Watch out for
- Clean spelling, a matching caller ID, a correct name or an old thread prove nothing; all can be faked or stolen.
- A familiar voice can be imitated.
- One-time codes are never to be read out or forwarded to someone who contacts you.
- Calling something safe because nothing looked wrong.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The person has a verdict with reasons and either an independent verification route or a clear instruction not to engage.
