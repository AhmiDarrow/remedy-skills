---
name: faq-generation
version: 1.0.1
description: >
  Build an FAQ from real user questions with direct, verified answers and a plan to keep them current. Use when support gets the same questions repeatedly or a launch needs an FAQ.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - support
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - web.fetch
metadata:
  source: library
  library_id: faq-generation
  official: true
  domain: content
  security_flags: []
---

# Faq Generation

## When to use
Recurring questions need one reliable place for answers.

## Steps
1. Gather questions from what exists: support threads, chat logs, site search terms, sales notes and community posts. Remove personal details. For a pre-launch product, label anticipated questions as predictions.
2. Group wordings of the same intent, count frequency, and keep the phrasing users use.
3. Select by frequency and cost of confusion, including blocking and money or data questions even if less common.
4. Where a question exists because the product or interface is unclear, report that fix; an FAQ entry is a stopgap.
5. Verify each answer against current behaviour or approved policy. Record its source and owner. Send unknown pricing, legal, security and roadmap answers to the owner instead of guessing.
6. Answer in the first sentence, with yes or no where honest, then conditions and exceptions, then steps or a link to the full procedure.
7. Write each answer to stand alone, since readers arrive from search.
8. Group by user task, not internal team, with short descriptive headings. If collapsible sections are used, keep them keyboard accessible with linkable entries.
9. Say how to get human help, and set review triggers: releases, policy or price changes and new support patterns.

## Watch out for
- Marketing questions nobody asked ("Why is the product so good?").
- Long procedures duplicated from documentation that will drift apart.
- Promising timelines or refunds the policy does not contain.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every entry traces to a real or labelled predicted question and a verified source, has an owner, and unanswered items are listed.
