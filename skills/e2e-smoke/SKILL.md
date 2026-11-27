---
name: e2e-smoke
version: 1.0.1
description: >
  Define or run a short smoke check of the most critical user journeys against a specific build or deployment. Use when asked whether a deploy or release candidate basically works.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - e2e
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - web.fetch
metadata:
  source: library
  library_id: e2e-smoke
  official: true
  security_flags: []
---

# E2E Smoke

## When to use
A fast go or no-go signal is needed, not full regression coverage.

## Steps
1. Pick one to three journeys whose failure would block release, such as sign in, perform the core action and see it saved. Keep the run to a few minutes.
2. Confirm the target environment and verify the running version or commit through a version endpoint, header or build label. A pass against the old build means nothing.
3. Check health first: pages and key APIs respond, static assets load, migrations finished, background worker alive.
4. Run existing smoke tests, or write a short script or checklist with an expected result at every step. Cross real boundaries: persist data and read it back in a new request, and confirm one asynchronous job completes.
5. Use a labelled test account and test data. Against production, default to read-only; get explicit approval for any write, and never trigger real payments or messages to real people.
6. Clean up what was created, using the application's own paths.
7. On failure save step, time, screenshot or response, request ID and relevant logs. Rerun once to classify, and report both results.
8. Report go or no-go with version, environment, steps passed and what was not covered.

## Watch out for
- A 200 status can be an error page or a cached shell; assert on content.
- Retrying until green hides an intermittent deployment fault.
- A cached session can skip a broken login.
- Smoke success says nothing about load, edge cases or other browsers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every chosen journey has a recorded pass or fail against a confirmed version, test data is cleaned or listed, and exclusions are stated.
