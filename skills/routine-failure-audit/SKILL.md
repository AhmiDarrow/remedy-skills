---
name: routine-failure-audit
version: 1.0.0
description: >
  Review existing scheduled routines to find broken, stale, noisy or risky ones. Use when outputs stop arriving, notices are ignored or routines have accumulated.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - routines
  - maintenance
kind: native
status: discovered
tools:
  - routines.list
  - read
  - glob
metadata:
  source: library
  library_id: routine-failure-audit
  official: true
  domain: tooling
  security_flags: []
---

# Routine Failure Audit

## When to use
The user is unsure whether their automations still work or still matter.

## Steps
1. List all routines with schedule, purpose and whether enabled.
2. For each, find evidence of recent runs: run history if available, output files and their dates, delivered notices. A listed routine is not proof that it runs.
3. Compare expected run times with evidence and mark missed or late ones; consider the machine being asleep and time zone changes.
4. Read recent outputs for quiet failures: empty reports, the same content repeated, "could not access" buried in success text, an expired date range.
5. Check every path, account, URL and person referenced still exists.
6. Review permissions in the wording: anything that sends, deletes, pays or posts unattended gets flagged.
7. Find overlaps competing for the same files or reporting the same facts.
8. Ask which outputs the user actually used in the last month.
9. Recommend per routine: keep, fix with specific new wording, reduce frequency, or retire. Apply changes only with approval, and verify the next run.

## Watch out for
- A succeeded run status can accompany a useless result.
- Fixing instructions without clearing corrupted saved state repeats the failure.
- Deleting is harder to undo than disabling; prefer disabling when unsure.
- If your tools cannot edit or disable a routine, give the user the exact steps instead of claiming it was changed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every routine has run evidence or is marked unverified, plus a recommendation, and approved changes are confirmed in the list.
