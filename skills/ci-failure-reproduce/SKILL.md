---
name: ci-failure-reproduce
version: 1.0.0
description: >
  Reproduce a job that fails in CI but passes locally by closing the environment gap one difference at a time. Use when a pipeline is red and the same command is green on a developer machine.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - testing
  - ci
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: ci-failure-reproduce
  official: true
  domain: ops
  security_flags: []
---

# Ci Failure Reproduce

## When to use
A CI job fails and "works on my machine". Not for tests that fail at random on the same commit and same runner; that is flakiness.

## Steps
1. Read the log upward from the final error to the first warning or failed command. The last line is often only the shell reporting an exit code.
2. Record what the runner used: OS image, tool versions, the exact command, env var names, checkout depth and commit SHA. Check whether CI tested a merge commit with the base branch instead of your branch head; if so, merge the base locally first.
3. Start clean: a fresh clone into an empty directory finds uncommitted, ignored or generated files you were silently relying on.
4. Install the way CI does, from the lockfile (`npm ci`, `pip install -r` with pins, `cargo build --locked`).
5. Run inside the same container image if the job has one, with `CI=true` and the same non-secret variables.
6. Close the remaining gaps one at a time: filename case (Linux is case-sensitive, default Windows and macOS volumes are not), CRLF endings, timezone and locale, CPU count and memory limit, no TTY, test order, network egress.
7. If it only fails on the runner, add a temporary diagnostic step that prints versions, `df -h`, free memory and the directory listing. Never dump the whole environment.
8. Fix the cause, remove the diagnostics, and confirm on the real pipeline.

## Watch out for
- A shallow clone breaks anything that reads tags or history, such as version stamping or changed-file detection.
- A process killed with exit code 137 usually means it was killed for memory, not that the test logic failed.
- A restored cache can carry stale output. Run once with a new cache key before blaming the code.
- Rerunning until green hides the difference instead of finding it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failure was reproduced outside the main pipeline or pinned to a named runner difference, and the fixed commit passes CI without diagnostic steps.
