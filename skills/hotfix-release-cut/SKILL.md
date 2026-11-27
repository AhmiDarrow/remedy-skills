---
name: hotfix-release-cut
version: 1.0.0
description: >
  Ship an urgent fix from the released version without dragging unreleased work along, then carry it back. Use when production or a shipped build needs a patch while the main branch has moved on.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - release
  - hotfix
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
  - todo
metadata:
  source: library
  library_id: hotfix-release-cut
  official: true
  domain: git
  security_flags: []
---

# Hotfix Release Cut

## When to use
Users are on version X, main holds half-finished work, and something cannot wait.
## Steps
1. Establish the exact released commit from the tag or the version reported by the running build, not from memory.
2. Reproduce the fault on that commit.
3. Branch from it (`git switch -c hotfix/x.y.z vX.Y.Z`).
4. Make the narrowest fix with a regression test. If main already fixed it, bring that commit with `git cherry-pick -x` and check it does not depend on unreleased code.
5. Review the full difference since the release (`git diff vX.Y.Z..HEAD`); every line should serve the fix or the version bump.
6. Bump the patch version everywhere the project records it, and write the notes.
7. Build with the same pipeline as a normal release and test upgrading from the broken version. Urgency does not remove the smoke test.
8. Ask before tagging, publishing or deploying.
9. Merge or cherry-pick the fix into main and into other maintained release branches, resolving differences deliberately. Verify with a test on each.
10. Check the original symptom is gone in the published build.
## Watch out for
- Releasing from main "because it is nearly the same".
- Forgetting the forward port, so the next normal release reintroduces the bug.
- Reusing or moving an existing tag; publish a new version.
- An update feed or latest marker pointing backwards when patching an older line.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The patch release differs from the previous one only by the intended changes, is verified in published form, and the fix exists on every maintained branch.
