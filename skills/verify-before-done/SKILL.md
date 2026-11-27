---
name: verify-before-done
version: 1.0.0
description: >
  Prove a task is actually finished with fresh evidence matched to each claim before reporting it. Use before saying that something is fixed, passing, installed, sent or complete.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - agent-workflow
  - verification
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - jobs
  - computer.snapshot
  - todo
metadata:
  source: library
  library_id: verify-before-done
  official: true
  domain: tooling
  security_flags: []
---

# Verify Before Done

## When to use
At the end of any task, and before commit, merge or hand-over steps that rely on success.
## Steps
1. Reread the original request and later corrections. List each requirement separately.
2. For each, name the evidence that would show it, at the level of the claim: "compiles" needs a build, "bug fixed" needs the original reproduction now passing, "UI works" needs the running screen exercised, "installed" needs the installed copy run.
3. Gather it after the last edit. Results from before a change are stale.
4. Read exit codes and the output itself. Check test counts, skips and warnings; zero tests collected can look like success. A pipe may report only the last command's status, so use `pipefail` or run the command alone.
5. Do not chain a commit or merge behind a check in a way that proceeds on failure. Run the check, inspect it, then act.
6. For background jobs, confirm they finished rather than merely started.
7. Inspect the final diff and status for unintended or missing files.
8. Confirm effects at the destination: read the written record, query the service, open the produced file.
9. Report per requirement: verified with what, not verified and why, or not done.
## Watch out for
- "Should work now" standing in for a run.
- Weakening or skipping a test to get a pass, without saying so.
- Reporting someone else's or a delegated worker's claim as your own observation.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every requirement carries fresh evidence or is openly labelled unverified or unfinished.
