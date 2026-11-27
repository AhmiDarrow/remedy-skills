---
name: feature-request-triage
version: 1.0.0
description: >
  Turn a pile of feature requests into grouped underlying needs with evidence and honest responses. Use when ideas arrive from many channels faster than anyone can evaluate them.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - product
  - feedback
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - todo
metadata:
  source: library
  library_id: feature-request-triage
  official: true
  domain: data
  security_flags: []
---

# Feature Request Triage

## When to use
Requests sit in tickets, chats and sheets with duplicates and no decisions.

## Steps
1. Gather into one table with source, date, requester segment and original wording.
2. Restate each as the job the person is blocked on. A requested button is one proposed answer.
3. Cluster by job, keeping links back to every original.
4. Count distinct accounts, not messages, and note segments, revenue tier or churn risk only where data shows it.
5. Check whether the product already does it; then it is a discoverability or docs problem. Route bugs to the bug process.
6. Assign a status: investigate, planned, not now, or declined, with a one-line reason.
7. For "investigate", name the open question and who will ask it.
8. Draft replies per status for the owner to send, and set a review date for "not now".

## Watch out for
- Ranking by who shouts loudest or posts most often.
- Merging requests that share words but solve different problems.
- Replies implying a promise ("on our radar, coming soon").
- Silently dropping declined items so they return as new.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each request links to one need with a status and reason, and counts reflect unique requesters.
