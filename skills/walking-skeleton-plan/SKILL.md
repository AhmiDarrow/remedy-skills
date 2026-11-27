---
name: walking-skeleton-plan
version: 1.0.0
description: >
  Plan the thinnest end-to-end path through a new system and build it before any layer is fleshed out. Use when starting a new app or subsystem with several parts that must connect.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - architecture
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: walking-skeleton-plan
  official: true
  domain: tooling
  security_flags: []
---

# Walking Skeleton Plan

## When to use
Several components (UI, service, store, worker, packaging) have never talked to each other. Integration is the unknown, so do it first.
## Steps
1. Name one trivial user action that touches every component, for example "type a title, save it, restart, see it listed".
2. List each boundary that action crosses: process, network, file format, database, auth, installer. Each must be real in the skeleton, not mocked.
3. Cut everything the action does not need: validation beyond not crashing, styling, extra fields, options.
4. Build in path order and run after each hop. Hardcoding is fine inside a component; faking the connection between two components is not.
5. Include the delivery path: the build command, the packaged artifact or deployed instance, and one automated test that drives the whole action.
6. Run the action from a clean checkout on a second directory or machine to expose undeclared dependencies.
7. Record what is hardcoded in a short list, each item tied to the later slice that replaces it.
8. Only then grow features, keeping the end-to-end test green after every slice.
## Watch out for
- Polishing the storage layer for a week before the UI can reach it.
- A skeleton that runs only from the development server; packaging surprises then arrive at release time.
- Choosing an action so trivial it skips the riskiest boundary. If login or a native bridge is the scary part, route through it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A single automated or scripted run performs the chosen action through every real boundary, from a clean checkout, using the same build form users will get.
