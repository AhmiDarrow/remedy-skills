---
name: hybrid-search-reranking
version: 1.0.0
description: >
  Combine keyword and vector retrieval with rank fusion, correct filtering and an optional reranker, measured for quality and latency. Use when vector search misses exact terms or ranks poorly.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - rag
  - search
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: hybrid-search-reranking
  official: true
  domain: llm
  security_flags: []
---

# Hybrid Search Reranking

## When to use
Semantic search fails on codes, names or error strings, or the right passage is retrieved but not near the top.

## Steps
1. Run the labelled retrieval set on keyword-only and vector-only to see which questions each wins. Create the set first if none exists.
2. Use the search engine already in the stack if it offers full text and vectors.
3. Check keyword analysis for the content: language stemming, case, and tokens such as `ERR_42`, version numbers and file paths. Add an exact field if needed.
4. Check vector settings: matching distance metric, required query and document prefixes for the embedding model, and no silent input truncation.
5. Apply tenant, permission and date filters inside both searches. With approximate vector indexes, filtering afterwards can return too few results.
6. Fuse with reciprocal rank fusion: sum 1 / (k + rank) across lists, with k around 60 as a common start. Raw keyword and cosine scores are on different scales and should not simply be added.
7. Deduplicate by chunk and limit near-identical neighbours from one document.
8. Add a cross-encoder or other reranker over the top candidates only if ordering is the measured problem. Note its input length limit and whether it sends text to an outside service.
9. Tune candidate depth and final k on development questions, then confirm on held-out ones.
10. Report recall, ranking metric and p95 latency for each stage.

## Watch out for
- A reranker cannot recover a passage that candidate retrieval never returned.
- Comparing approximate vector results with exact search tells you how much recall the index settings are losing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen pipeline beats both single methods on held-out questions within the latency budget, with filters verified in both branches.
