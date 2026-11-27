---
name: lora-finetune-preparation
version: 1.0.0
description: >
  Decide whether fine-tuning is justified, then prepare clean, split, correctly formatted data and a baseline for an adapter run. Use when someone wants to fine-tune a language model.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - fine-tuning
  - data
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - grep
metadata:
  source: library
  library_id: lora-finetune-preparation
  official: true
  domain: llm
  security_flags: []
---

# Lora Finetune Preparation

## When to use
A user plans a LoRA or similar fine-tune, usually for a format, style or narrow task.

## Steps
1. Collect failing examples from the current best prompt. Missing or changing facts call for retrieval; consistent behaviour or format gaps may suit fine-tuning.
2. Build an evaluation set and score the base model with a good prompt, including few-shot examples. This is the bar.
3. Confirm the right to use the data and the base model's licence. Remove secrets and personal data; a trained model can reproduce them.
4. Write examples that match production inputs and the exact output wanted, including cases where it should refuse or say information is missing.
5. Deduplicate, check contradictions, and balance categories deliberately. Review a random sample by hand.
6. Split by source or topic so near-copies do not cross into validation or test.
7. Render with the base model's chat template, decode the tokens and verify special tokens, end-of-turn markers and which tokens contribute to loss.
8. Report token lengths and fix examples that would be truncated.
9. Run a tiny overfit trial to validate the pipeline. Estimate memory, time and cost, and get approval before the full run.
10. Compare adapter with baseline on the same held-out set, including general tasks that might have degraded.

## Watch out for
- Training on one template and serving with another quietly ruins results.
- Falling training loss does not show improvement on the task.
- An adapter depends on its base model revision; record it, and retest after merging or quantizing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
There is a recorded baseline, a verified rendered dataset with clean splits, and a defined score the adapter must beat.
