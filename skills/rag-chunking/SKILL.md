---
name: rag-chunking
version: 1.0.1
description: >
  Design how documents are parsed, split and labelled for retrieval, then compare options on real questions. Use when building a retrieval index or when passages come back cut off or out of context.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - rag
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - grep
metadata:
  source: library
  library_id: rag-chunking
  official: true
  security_flags: []
---

# Rag Chunking

## When to use
Documents are being prepared for a retrieval-based application.

## Steps
1. Sample each document type, including the ugliest: PDFs with columns, tables, code, slides, chat threads and scanned pages.
2. Inspect parser output before choosing sizes. Check reading order, headings, tables, lists, repeated headers and footers, and silently empty pages. Fix extraction first.
3. Gather representative questions with the source span that answers each.
4. Split on structure: sections, then paragraphs, then sentences. Keep functions, list items with their introduction, and warnings with the step they apply to. For tables keep rows whole and repeat column headers.
5. Set size in tokens using the embedding model's tokenizer, and stay under its input limit, which some systems truncate silently. Treat a few hundred tokens as a starting experiment, not a rule.
6. Add overlap only where boundaries split meaning, and deduplicate overlapping hits at retrieval.
7. Store document id, version, title, heading path, location (page or anchor), update date, language, content hash and access control. Consider prefixing title and heading path to the embedded text.
8. If small passages match well but lack context, retrieve small and expand to the parent section within a token budget.
9. Make ingestion repeatable: stable ids, changed documents replace old chunks, deleted documents disappear.
10. Compare two or three configurations on the same questions by whether the answer span reaches the prompt within the context budget, then read the misses.

## Watch out for
- Comparing equal top-k across chunk sizes, which gives larger chunks much more context.
- Permissions filtered only after generation; enforce them at retrieval.
- Old and new document versions both indexed and contradicting each other.
- Pronouns and "see above" leaving a chunk meaningless alone.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Sampled chunks read correctly with a traceable source, updates and deletions work, and the chosen configuration has measured results on the question set.
