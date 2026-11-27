---
name: embedding-model-migration
version: 1.0.0
description: >
  Switch embedding models or index settings with a parallel index, change capture, side-by-side evaluation and rollback. Use when upgrading embeddings behind live search.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - rag
  - migration
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - todo
metadata:
  source: library
  library_id: embedding-model-migration
  official: true
  domain: llm
  security_flags: []
---

# Embedding Model Migration

## When to use
A vector index must be rebuilt because the embedding model, dimension, preprocessing or distance metric is changing.

## Steps
1. Record current model, version, dimension, metric, normalization, input template and chunking. Never mix vectors from different models in one comparable field, even if dimensions match.
2. Check the new model's input limit, prefixes for queries versus documents, languages, licence and data handling.
3. Confirm the source text is still available to re-embed; estimate tokens, time, cost and extra storage, and get approval.
4. Test on a sample first against the labelled retrieval set.
5. Create a separate index or column, tagging each record with model version and content hash.
6. Start capturing live creates, updates and deletes before the backfill, writing them to both.
7. Backfill resumably in batches with rate limits. Apply a result only if the content hash still matches, so late jobs cannot restore old or deleted text.
8. Reconcile ids and hashes between old and new indexes.
9. Compare retrieval metrics, latency and permission filtering. Recalibrate any similarity threshold, since scores are not comparable across models.
10. Switch query embedding and index together under one flag, ramp, and keep the old pair updated until rollback is no longer needed. Delete it only with approval.

## Watch out for
- Switching the index but not the query encoder gives plausible-looking, poor results.
- Embedding caches keyed without model version return old vectors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new index reconciles with the source, passes the retrieval comparison, and rollback has been exercised.
