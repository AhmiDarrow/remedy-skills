---
name: rag-retrieval-evaluation
version: 1.0.0
description: >
  Measure whether a retrieval system returns the right passages using a labelled question set, recall at k and failure categories. Use when tuning search for a RAG application or before changing it.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - rag
  - evaluation
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - grep
metadata:
  source: library
  library_id: rag-retrieval-evaluation
  official: true
  domain: llm
  security_flags: []
---

# Rag Retrieval Evaluation

## When to use
Answers depend on retrieved passages and there is no number showing whether retrieval works.

## Steps
1. Evaluate retrieval separately from answer generation.
2. Collect questions from real logs where permitted. Add paraphrases, exact identifiers, acronyms, multi-document questions and some with no answer in the corpus.
3. Label relevant evidence by document and text span, not by chunk id, so labels survive rechunking.
4. If a model drafts questions from passages, edit them by hand; they tend to reuse the passage's words and inflate scores.
5. Pool the top results of several retrieval methods when labelling, so relevant passages the current system misses are found.
6. Record the configuration: index snapshot, chunking, embedding model, filters, k.
7. Compute recall at k (or hit rate where one passage suffices), plus MRR or nDCG for ordering. Measure at the candidate stage and at what actually reaches the prompt.
8. For each miss, locate the loss: not ingested, parsed badly, split across chunks, filtered out, not in candidates, ranked low, or dropped by the context limit.
9. Change one thing, rerun, and list questions that improved and regressed.
10. Keep a held-out portion and add production failures over time.

## Watch out for
- Raising k raises recall but may bury the evidence and add cost.
- Test with real user permissions; an evaluation run as an administrator hides access filters, and leaked restricted passages are a failure, not a hit.
- With few questions, a small score change is noise.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A repeatable command prints retrieval metrics per question category, and each miss has an assigned failure stage.
