---
name: release-checklist
version: 1.0.1
description: >
  Run a pre-release gate on the exact commit to be shipped: tree state, versions, tests, package contents and rollback. Use when asked whether a project is ready to release or tag.
author: Remedy Official
license: Apache-2.0
tags:
  - release
  - ci
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: release-checklist
  official: true
  security_flags: []
---

# Release Checklist

## When to use
A release is about to be tagged, built or published.

## Steps
1. Read the project's release notes for maintainers, scripts and release workflow. Their steps take priority; this gate checks them.
2. Fix the candidate: branch, commit hash and intended version. Check `git status`, unpushed and missing remote commits, and that the tag and registry version do not already exist.
3. Check every version location agrees and the changelog entry covers changes since the last tag, including breaking changes and upgrade steps.
4. Run the project's full gate on that commit: tests, lint, types and build. Record commands and results. Confirm hosted checks, if used, ran on the same hash. Count skipped tests.
5. Build the artifact from a clean checkout with locked dependencies. List its contents for missing assets and for secrets, debug files or local paths.
6. Install it in a clean environment and exercise the main path. Test upgrade from the previous release, including data migrations and updater metadata.
7. Check release prerequisites without printing values: signing identity and expiry, publishing access, target channel and required configuration.
8. State rollback: how to withdraw or supersede, which migrations cannot be reversed, and who decides.
9. Produce a table of pass, fail or not run with evidence, then the remaining commands in order, marking irreversible ones. Do not tag, push or publish without an explicit request.

## Watch out for
- Testing the working tree while releasing a different commit.
- Ignored local files making the build work only on this machine.
- A tag push triggering publication immediately.
- Fixing a blocker and reusing earlier results; the candidate has changed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every gate has a result tied to the candidate hash, blockers and unrun checks are explicit, and the remaining release steps are listed.
