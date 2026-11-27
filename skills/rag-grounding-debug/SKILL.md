---
name: rag-grounding-debug
version: 1.0.0
description: >
  Trace a wrong or unsupported answer in a retrieval application to ingestion, retrieval, context assembly or generation. Use when a RAG assistant invents facts, cites wrongly or ignores documents.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - rag
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: rag-grounding-debug
  official: true
  domain: llm
  security_flags: []
---

# Rag Grounding Debug

## When to use
A specific question got a bad answer even though the system is supposed to answer from sources.

## Steps
1. Capture the failing trace: user turn, history, rewritten query, filters, retrieved ids with scores, the final assembled prompt, model settings and output.
2. Find the correct answer in the source documents yourself. If it is absent, outdated or contradicted, the corpus is the problem.
3. Check the parsed text, especially tables, columns, scanned pages, headers and footnotes.
4. Check the index holds the current version and no stale or deleted copies.
5. Run the query as logged. Follow-ups such as "what about that one" fail if history was not resolved into a standalone query.
6. Confirm the evidence survived reranking, deduplication and token trimming into the final prompt.
7. Check each chunk carries its title, section, date and source id, so the model can tell similar policies apart.
8. If the evidence was present, replay generation with only that passage, then with the full context, to separate distraction from instruction problems.
9. Require claims to cite provided ids, validate ids in code, and check that cited text supports the claim. Define the response when evidence is insufficient.
10. Fix the failing stage, rerun the case several times, and add it plus a no-answer variant to the evaluation set.

## Watch out for
- A valid citation id can still be attached to an unsupported sentence.
- "Answer only from context" reduces but does not eliminate use of model knowledge.
- Forcing refusals too hard makes answerable questions fail; measure both.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing stage is shown by trace evidence, the case passes repeatedly, and the no-answer case declines.
