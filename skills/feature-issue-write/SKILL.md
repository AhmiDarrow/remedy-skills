---
name: feature-issue-write
version: 1.0.0
description: >
  Write a feature or task issue that someone without your context can pick up and finish. Use when filing work into a tracker for later, for a teammate or for a delegated worker.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - issues
  - planning
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - write
metadata:
  source: library
  library_id: feature-issue-write
  official: true
  domain: docs
  security_flags: []
---

# Feature Issue Write

## When to use
An idea or follow-up must survive outside the current conversation. For defect reports use a bug template instead.
## Steps
1. Search open and closed issues first (`gh issue list --state all --search "terms"` where GitHub is used) and link or extend an existing one.
2. Title it with the outcome and the area: "Export keeps folder structure", not "Export improvements".
3. State who is affected and what they cannot do today, with a concrete example.
4. Describe the wanted behaviour from outside. Include sample input and output where format matters.
5. Give starting points in the code by file and symbol name, which age better than line numbers, plus any constraint a newcomer would violate.
6. List what is explicitly not part of this issue.
7. Write how completion is checked: commands to run or a short manual scenario.
8. Remove references to "as discussed" and restate the decision. Strip private data, tokens and personal details from pasted logs.
9. Show the draft to the user and create it only after they approve.
## Watch out for
- Prescribing an implementation without saying why, so the assignee cannot choose better.
- Bundling three requests into one issue that can never be closed.
- Pasting a whole chat transcript in place of a summary.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A reader with only the issue and the repository can say what to change, where to begin and how to prove it is finished.
