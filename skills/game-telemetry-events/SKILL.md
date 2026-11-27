---
name: game-telemetry-events
version: 1.0.1
description: >
  Define a gameplay telemetry plan that starts from design questions, with typed events, sampling, validation, consent and retention limits. Use when instrumenting drop-off, balance or crash context.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - ops
  - privacy
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
  library_id: game-telemetry-events
  official: true
  domain: gaming
  security_flags: []
---

# Game Telemetry Events

## When to use
Design decisions need evidence from play.

## Steps
1. List the questions, the decision each informs and the calculation that would answer it. Drop events with no question.
2. Reuse the existing pipeline and naming. For each event give trigger, firing side (client or server), properties, types, units, allowed values and an example.
3. Add shared fields: event and schema version, build, platform, random session id, sequence number, and level or mode ids.
4. Define funnels with start, success, failure and abandon so missing ends are visible. Quitting or crashing often sends no event; derive it.
5. Minimise data: no names, emails, chat, free text, file paths with user names, precise location or hardware identifiers. A hashed identifier is still personal data if it can be linked. Use rotating or random ids where enough.
6. Do not collect before required consent. Respect opt-out, platform rules and extra protections for children; flag legal questions for review.
7. Aggregate or sample high-frequency events, sampling whole sessions when sequences matter, and record the rate.
8. Queue offline with size and age limits, send without blocking frames, and deduplicate by event id. Treat client data as forgeable.
9. Set retention, access and deletion per event.
10. Verify in a test environment: capture traffic through a full session, check schema and counts, and confirm opt-out sends nothing optional.

## Watch out for
- The same event name changing meaning between builds.
- Developer and bot sessions mixed into player data.
- Crash context dumping whole memory, logs or save files.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each event maps to a question with a typed schema, privacy and retention decisions, and test captures match the schema, or the unverified ones are listed.
