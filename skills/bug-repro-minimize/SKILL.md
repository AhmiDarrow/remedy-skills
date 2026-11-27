---
name: bug-repro-minimize
version: 1.0.0
description: >
  Turn a vague or elaborate failure into the smallest reliable reproduction. Use when a bug needs too many steps, a large project or real user data to trigger.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - debugging
  - reproduction
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - grep
metadata:
  source: library
  library_id: bug-repro-minimize
  official: true
  domain: testing
  security_flags: []
---

# Bug Repro Minimize

## When to use
Nobody can fix efficiently what takes ten minutes and a customer's whole workspace to show.
## Steps
1. Capture the original failure exactly: command or clicks, full output, versions, OS, config. Reproduce it once as reported before changing anything.
2. Define the failure signature (error text and location, or the specific wrong value) so you do not drift onto a different bug while shrinking.
3. Copy the setup somewhere disposable. Never reduce the user's only copy of data.
4. Remove one dimension at a time: UI by calling the underlying function, network by a recorded response, database by a few rows, concurrency by a single worker. Rerun after each removal.
5. When a removal makes the bug vanish, restore it and note it: that element is involved.
6. For large inputs, option lists or test sequences, automate halving with a script that exits 0 only on that signature; keep order. When neither half fails alone, split into smaller chunks and remove one at a time.
7. Pin sources of variation: random seed, clock, locale, timezone, ordering.
8. Express the result as one command or a short test with inline data, run it several times, and record the failure rate.
9. Replace any personal or confidential values with synthetic ones and confirm it still fails.
## Watch out for
- Accepting any red output as the same bug.
- Removing several things at once and not knowing which mattered.
- A reproduction that relies on leftover state such as caches or a local database; verify from a clean directory.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh checkout can run one short command or test that shows the recorded failure signature, with no private data and a known reproduction rate.
