---
name: llm-judge-calibration
version: 1.0.0
description: >
  Build a model-based grader and validate it against human labels, bias probes and held-out data before trusting its scores. Use when automating evaluation of open-ended outputs.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - evaluation
  - prompting
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: llm-judge-calibration
  official: true
  domain: llm
  security_flags: []
---

# Llm Judge Calibration

## When to use
Output quality cannot be checked by exact match and someone wants a model to score it.

## Steps
1. First replace anything checkable in code: format, length, required ids, executable tests.
2. Define one criterion per judge, with pass and fail descriptions and boundary examples. Prefer pass/fail over a 10-point scale.
3. Have a person label a varied set including real failures and borderline cases. Where possible, double-label some to see how often people disagree.
4. Split into examples for developing the judge prompt and a held-out set for validation.
5. Give the judge the input, the output and the reference or source needed to verify it. Ask for a short evidence-based critique followed by a verdict in a fixed format.
6. Compare with human labels using a confusion matrix; report true-pass and true-fail rates separately.
7. Probe biases: longer or confident answers, formatting, presence of a reference answer, and, for pairwise judging, swap positions and check consistency.
8. Include outputs containing text aimed at the grader and confirm it is treated as data.
9. Repeat runs to measure verdict instability.
10. Pin model and prompt versions, and revalidate when either changes. Periodically audit fresh samples.

## Watch out for
- High overall agreement is meaningless if nearly everything passes and the judge misses most failures.
- Tuning the judge on the validation examples overstates its accuracy.
- A model grading its own outputs may share their blind spots.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Held-out agreement, including the failure detection rate, meets a bar set in advance, and known disagreement types are documented.
