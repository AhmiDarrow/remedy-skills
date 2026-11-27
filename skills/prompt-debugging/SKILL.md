---
name: prompt-debugging
version: 1.0.0
description: >
  Fix a prompt that behaves badly by reproducing the exact rendered request, grouping failures and changing one thing at a time. Use when a model ignores instructions or gives inconsistent results.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - prompting
  - debugging
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: prompt-debugging
  official: true
  domain: llm
  security_flags: []
---

# Prompt Debugging

## When to use
A model-backed feature gives wrong output and edits so far have been guesswork.

## Steps
1. Capture the exact request sent: system and user text after templating, history, tools, retrieved context, model id and sampling settings. Bugs often sit in the rendering.
2. Check for empty variables, truncation, duplicated blocks and instructions that contradict each other or the examples.
3. Run the failing input several times to get a failure rate.
4. Collect failures and passing cases into a small fixed set, and group failures by pattern.
5. Ask whether a capable person given only this text could do the task. Add missing audience, purpose, definitions, edge-case rules and what to do when unsure.
6. Separate instructions from data with clear delimiters.
7. Explain the reason behind important rules and describe the wanted behaviour, rather than stacking capitals and "never".
8. Inspect examples: models copy their length, order and wording. Use varied ones or describe the pattern.
9. Move work that needs certainty, such as arithmetic, filtering or authorization, into code.
10. Change one thing, run the whole set repeatedly, compare rates, and keep the diff only if it helps without new failures.

## Watch out for
- A patch naming the single failing input does not generalize.
- Prompts that only grow accumulate conflicting rules; remove ones with no measured effect.
- Asking the model why it failed yields a hypothesis to test, not a diagnosis.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failure rate on the fixed set improved across repeated runs with no regressions, and the prompt change and results are recorded.
