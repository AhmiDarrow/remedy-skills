---
name: contributor-guide-write
version: 1.0.0
description: >
  Write a CONTRIBUTING file that takes a newcomer from clone to accepted pull request. Use when outside contributions arrive broken or maintainers repeat the same setup advice.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - open-source
  - onboarding
kind: native
status: discovered
tools:
  - read
  - glob
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: contributor-guide-write
  official: true
  domain: docs
  security_flags: []
---

# Contributor Guide Write

## When to use
A repository accepts contributions but its real rules live in maintainers' heads and CI files.

## Steps
1. Read CI workflows; they hold the true list of checks. Read recent pull request reviews for repeated feedback.
2. State which contributions are welcome and which need an issue first, such as new features or dependencies.
3. Give setup commands and test them in a clean copy.
4. Give the single local command, or short list, that reproduces CI, with expected duration and any checks that cannot run locally.
5. Describe branch, commit and pull request conventions the project actually enforces.
6. Say how review works: who looks, realistic response expectations, and what gets a change closed.
7. Include licensing terms for contributions only as the maintainer decides them; ask about sign-off or agreements.
8. Link security reporting to a private channel and keep it out of public issues.

## Watch out for
- Aspirational rules the codebase itself breaks.
- Duplicating the README, which then drifts; link instead.
- Inventing response-time promises or a code of conduct contact nobody monitors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Setup and check commands ran from a clean copy, every CI check is covered, and policy statements are confirmed by a maintainer.
