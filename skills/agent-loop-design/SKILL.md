---
name: agent-loop-design
version: 1.0.0
description: >
  Design a tool-using agent loop with a verifiable goal, state, error feedback, approval points and stop conditions. Use when building an agent or fixing one that loops, stalls or claims false success.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - agents
  - architecture
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: agent-loop-design
  official: true
  domain: llm
  security_flags: []
---

# Agent Loop Design

## When to use
An application lets a model choose actions over several steps.

## Steps
1. Confirm an agent is needed. If steps are known in advance, write a fixed workflow with model calls inside it.
2. Define the task contract: inputs, allowed effects and how completion is verified by evidence such as a test result or a read-back.
3. Start with one agent and a small set of distinct tools.
4. Return tool errors to the model with what failed and what can be changed, while keeping secrets out.
5. Record every call and result with ids. Persist state outside the conversation so a crash can resume.
6. Make side effects idempotent or check state before retrying; after a timeout the action may have happened.
7. Put permission checks and approvals in the harness, with each approval tied to the exact action and arguments.
8. Set limits on steps, time and spend, sized from observed successful runs. Detect repeated identical calls and no progress.
9. Define distinct end states: done and verified, blocked needing a person, failed, and stopped by limit. Report partial effects.
10. Support cancellation, including child processes.
11. Test with tool stubs that fail, return empty or huge results, or contain misleading text. Judge final state and side effects over repeated runs, and read traces of failures to find the first bad step.

## Watch out for
- The model saying "done" is not verification.
- Requiring one exact tool sequence in tests rejects valid solutions; assert outcomes and forbidden actions.
- Adding a rule per failure often hides an unclear tool or missing information in results.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each end state is reachable in a test, a retried write does not duplicate, and success is reported only with checkable evidence.
