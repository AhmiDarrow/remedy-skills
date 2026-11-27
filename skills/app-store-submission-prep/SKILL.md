---
name: app-store-submission-prep
version: 1.0.0
description: >
  Prepare an iOS or Android release for store review by checking builds, metadata, privacy declarations and reviewer access. Use before submitting an app or after a rejection.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - mobile
  - release
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - web.fetch
  - todo
metadata:
  source: library
  library_id: app-store-submission-prep
  official: true
  domain: ops
  security_flags: []
---

# App Store Submission Prep

## When to use
A first submission or significant update is going to a mobile app store.

## Steps
1. Fetch the current official review guidelines and technical requirements, including minimum target SDK or required Xcode version. These change; do not rely on memory.
2. Check identifiers, version and strictly increasing build number, signing, and that the release artefact (Android App Bundle or iOS archive) installs and runs from a testing track.
3. Compare privacy declarations with the code and every bundled SDK: data collected, linked identity, tracking, permission purpose strings, Apple privacy manifests and the Play data safety form.
4. Check policy-sensitive flows: account deletion inside the app where accounts can be created (Google Play also requires a web link for requesting deletion), purchase rules for digital goods, restore purchases, subscription terms, sign-in options, user content moderation and reporting.
5. Provide reviewers a working demo account and notes for hardware-dependent or region-locked features. The user enters credentials into the store console.
6. Verify screenshots and description match the build, with sample data only, and that support and privacy policy links load.
7. Complete age rating and export compliance questions with the owner.
8. Choose staged or manual release and note what would halt it.
9. After rejection, quote the cited guideline, reproduce what the reviewer saw, then fix or reply with evidence.
10. Stop for the user before pressing submit.

## Watch out for
- A reviewer hitting a dead test server or a login wall is a common avoidable rejection.
- Debug menus, placeholder text or references to unfinished features invite rejection.
- Losing the signing key or credentials can block updates; confirm where they are held without printing them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A checklist shows each item verified against the actual build and current rules, open owner decisions are listed, and nothing was submitted without approval.
