---
name: training-loss-debugging
version: 1.0.0
description: >
  Debug a model that will not learn, diverges or produces NaN loss using small controlled checks in a fixed order. Use when neural network training behaves wrongly.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - ml
  - debugging
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - jobs
metadata:
  source: library
  library_id: training-loss-debugging
  official: true
  domain: data
  security_flags: []
---

# Training Loss Debugging

## When to use
Loss is flat, explodes, turns NaN, or training looks fine while predictions are useless.

## Steps
1. Fix seeds, record library versions and shrink to a configuration that reproduces quickly.
2. Decode a real batch just before the model: inputs and labels aligned, ranges and normalization right, padding and masks correct.
3. Check the initial loss. For balanced C-class cross-entropy it should be near ln(C).
4. Verify the loss's expected input: many cross-entropy functions take raw logits, so an extra softmax weakens learning. Check output and target shapes for silent broadcasting.
5. Overfit one tiny batch with augmentation and regularization off. If loss will not approach zero, suspect the model, loss or optimizer wiring.
6. Confirm parameters are in the optimizer, not unintentionally frozen, and receive nonzero gradients. Check gradients are cleared each step unless deliberately accumulating.
7. Sweep learning rates across orders of magnitude; check warmup and schedule step units.
8. For NaN, find the first non-finite value using anomaly detection or hooks; check logs of zero, division, mixed-precision overflow and bad inputs. Test in full precision.
9. Check training and evaluation modes for dropout and batch normalization.
10. Re-enable one feature at a time.

## Watch out for
- Gradient clipping can hide an underlying fault.
- Check the free memory and ask before launching long or expensive runs.
- A very low loss suddenly may mean the label leaked into the input.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The tiny-batch test passes, the root cause is identified by a change that toggles the failure, and a short real run shows loss falling.
