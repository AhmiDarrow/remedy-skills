---
name: prompt-eval-harness
version: 1.0.1
description: >
  Build a regression suite for a prompt or agent with labelled cases, deterministic checks and repeated runs. Use when changing prompts, tools or models and needing to know what got worse.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - testing
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: prompt-eval-harness
  official: true
  security_flags: []
---

# Prompt Eval Harness

## When to use
Model behaviour is judged by eyeballing a few replies and changes keep breaking earlier ones.

## Steps
1. Write down the behaviours that matter and which failures are unacceptable.
2. Start with about 10 to 30 cases from real failure types and normal use: edge input, missing information, requests that should be declined or clarified, and hostile text in documents. Use synthetic or scrubbed data.
3. Give each case properties, not one golden reply: valid schema, required fact, forbidden string, correct tool and arguments, and no tool call where none is allowed.
4. Check in code where possible. Use a model grader only for what code cannot judge, and compare it with human labels before gating on it.
5. Run the same rendered prompt and settings as the application. Stub tools with recorded results so no test sends, deletes or buys anything.
6. Record per case the output, check results, model identifier, prompt version, parameters, latency and token use. Confirm cost before large paid runs.
7. Repeat variable cases several times and report pass rate. Require all runs to pass for safety-critical cases; set other thresholds from a baseline.
8. Compare candidate with baseline case by case, read new failures, and add each future production failure as a case. Keep a few held-out cases that are not tuned against.

## Watch out for
- An average score can rise while a critical case breaks.
- Temperature zero does not guarantee identical output.
- Exact-text matching fails harmless rewording and passes nothing useful.
- A provider can change behaviour behind a moving model alias.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
One command produces per-case results, the baseline is saved, and a deliberately bad prompt change makes the suite fail.
