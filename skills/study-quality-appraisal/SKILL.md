---
name: study-quality-appraisal
version: 1.0.0
description: >
  Assess how far a research study's design supports its conclusion. Use when someone says "a study shows" and the user needs to know how much to trust it.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - academic
kind: native
status: discovered
tools:
  - web.fetch
  - read
  - web.search
metadata:
  source: library
  library_id: study-quality-appraisal
  official: true
  domain: docs
  security_flags: []
---

# Study Quality Appraisal

## When to use
A single study or a handful of them is being used to justify a belief or action.

## Steps
1. Read methods and results before the abstract's conclusion. State if you only have the abstract.
2. Name the design: randomised experiment, cohort, case-control, cross-sectional, qualitative, simulation, meta-analysis. Say which claims it can bear; observational designs do not alone establish cause.
3. Record who was studied, how they were selected and how many dropped out, then compare with the population the user cares about.
4. Check the comparison: what was the control, was assignment concealed, was outcome assessment blinded where it could be.
5. Look for a preregistration or protocol and compare the planned primary outcome with the one headlined.
6. Report effect size with its interval, in practical units, beside any p-value.
7. Note multiple comparisons, post-hoc subgroups and unmeasured confounders.
8. Read funding and conflict statements, then search for replications, critiques and systematic reviews.
9. Summarise: what it supports, what it does not, and the main reason for caution.

## Watch out for
- "No significant difference" in a small study is not evidence of no difference.
- A meta-analysis inherits the flaws and publication bias of its inputs.
- Do not attack every study with a generic limitations list. Name the flaw that could change this result and how.
- For health questions, this informs a conversation with a clinician; it is not advice about the user's care.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user has a plain statement of what the study can and cannot support, tied to specific design features.
