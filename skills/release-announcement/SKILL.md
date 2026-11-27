---
name: release-announcement
version: 1.0.1
description: >
  Write a product release announcement for blog, email or in-app that leads with user impact and states availability and required actions. Use when a shipped or imminent release needs to be told to users.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - product
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - bash
metadata:
  source: library
  library_id: release-announcement
  official: true
  domain: content
  security_flags: []
---

# Release Announcement

## When to use
Users should hear about a release. This is the message, not the full changelog.

## Steps
1. Verify what is actually in the release from the tag or release diff, changelog and merged work. Exclude unmerged, flagged-off or delayed features.
2. Confirm availability: version, platforms, plans, regions and staged rollout timing. Say when not everyone has it yet.
3. Pick the one to three changes that matter most to readers. For each, say what they can now do, with a real example or screenshot.
4. Put breaking changes, required actions, deadlines, security updates and removed features near the top, naming who is affected and how to tell.
5. Describe fixes by the symptom users saw. Disclose security details only to the extent already approved for release.
6. Give how to get or enable it and link tested documentation or upgrade steps.
7. Adapt by channel: blog has context and examples; email goes to affected people with a subject naming the news; in-app text is a sentence or two with one dismissible link.
8. Check each claim in the released build, especially speed or compatibility statements, which need measurements.
9. List known issues and where to report problems, then hand over drafts. Publishing and sending are the user's actions, timed after the release is really available.

## Watch out for
- Announcing before downloads or rollout are live.
- Burying a forced migration under new features.
- Internal ticket names and component jargon.
- Screenshots containing test or customer data.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each statement matches the shipped build, affected users can see what to do and by when, links work, and every channel draft is ready for approval.
