---
name: ci-pipeline-review
version: 1.0.1
description: >
  Review a CI pipeline for checks that can be skipped, falsely pass, leak secrets or waste time, with ranked fixes. Use when auditing CI config or when green builds still ship broken code.
author: Remedy Official
license: Apache-2.0
tags:
  - ci
  - devops
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: ci-pipeline-review
  official: true
  security_flags: []
---

# Ci Pipeline Review

## When to use
Someone wants an overall judgement on a pipeline. Deep work on caching, action pinning or outside pull requests can follow as separate tasks.

## Steps
1. Read every workflow file and included template, and list what runs on pull request, merge, tag, schedule and manual trigger.
2. Look at recent runs: duration per job, queue time, failure and rerun rates, and which jobs are mostly skipped.
3. Map required checks on the protected branch to current job names. Where permissions allow, compare with the actual branch rules. Note how a path filter or condition leaves a required check pending or counted as passed when skipped.
4. Hunt false greens: `continue-on-error`, `|| true`, pipes in shell steps without `pipefail`, test commands that succeed with zero tests, focused tests, and reports uploaded but never enforced.
5. Compare with how the project is verified locally: lint, types, tests, build, supported platform versions and a check of the packaged artifact. Name what CI never runs.
6. Check that deploy and release jobs depend on the checks and use the commit that was tested.
7. Check token permissions are minimal, secrets reach only jobs that need them, untrusted event text is not interpolated into scripts, and fork code cannot reach secrets.
8. Check reliability and speed: job timeouts, cancellation of superseded pull request runs but not in-progress deploys, locked dependency installs, parallel independent jobs and the longest dependency path.
9. Report by risk with file and line, evidence, fix and how to prove it. A good proof is a deliberate failing change that turns the required check red on a test branch; ask before pushing it, and confirm the push cannot trigger a deploy or release.

## Watch out for
- Renaming jobs without updating required check names.
- Recommending removal of a slow job without knowing what it catches.
- Printing secrets while debugging; masking does not cover transformed values.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each trigger's gates are mapped, false-pass and secret risks are listed with evidence, and unverified host settings are stated as unverified.
