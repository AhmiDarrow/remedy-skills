---
name: bug-intake-triage
version: 1.0.0
description: >
  Triage a queue of incoming bug reports into severity, priority, owner area and next action. Use when new or unlabelled issues have piled up and nobody knows which matter.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - triage
  - issues
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: bug-intake-triage
  official: true
  domain: tooling
  security_flags: []
---

# Bug Intake Triage

## When to use
There is a backlog of reports of mixed quality and limited time to fix them.
## Steps
1. Pull the list with age, labels and comment count. Work oldest-unlabelled and most-recent first, so both neglected and breaking items surface.
2. Scan all new items once for emergencies: data loss, security exposure, crash on start, broken install or update. Raise these immediately, before finishing the pass.
3. For each report extract version, platform, steps, expected and actual. Note what is missing.
4. Score severity (harm when it happens) separately from priority (when to fix it, given how many hit it, workaround, and release timing).
5. Check whether it still exists: compare the reported version with the fix history, and reproduce if it takes only minutes.
6. Assign exactly one next action: fix now, reproduce, ask reporter (with specific questions), duplicate of N, expected behaviour (explain), or decline with a reason.
7. Group duplicates by fingerprint (exact error string, top in-project frame, first bad version), not by similar wording or a generic message such as "timeout". Merge only if one fix would resolve both, keep the report with the best reproduction, and carry unique platform or log details into it.
8. Look across the batch for several reports sharing a release or component; that pattern outranks any single report.
9. Present proposed labels, replies and closures as a table. Apply or post them only after the user approves.
## Watch out for
- Letting an angry tone raise severity or a calm one lower it.
- Requesting "more info" without saying which command output or file you need.
- Closing as cannot-reproduce after testing only a different version or OS than reported.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every item in the batch has a severity, a priority and one next action, and any data-loss or security reports were escalated separately.
