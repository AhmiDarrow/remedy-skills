---
name: record-deduplication-matching
version: 1.0.0
description: >
  Find and merge duplicate records with normalization, blocking, scored matching, human review and reversible merges. Use when customer, product or contact lists hold the same entity more than once.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - cleaning
  - matching
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: record-deduplication-matching
  official: true
  domain: data
  security_flags: []
---

# Record Deduplication Matching

## When to use
Records lack a shared reliable key and the same real thing appears under different spellings or sources.

## Steps
1. Define when two records are the same entity, with hard examples: family members sharing an email, franchise branches, product size variants.
2. Work on a copy. Keep original values and add normalized columns: trimmed, case-folded, consistent Unicode form, standardized phone and address parts. Apply provider-specific email rules only where known to be correct.
3. Resolve exact matches on strong identifiers first, after excluding placeholders such as `test@example.com`, `000000` or "N/A".
4. Generate candidate pairs with several blocking rules (postcode plus name prefix, phone, domain) rather than comparing every pair.
5. Score pairs on separate field comparisons, using string similarity for names. Treat conflicting strong identifiers as evidence against.
6. Set two thresholds: auto-merge, human review, and reject below. Label a random sample in each band and measure precision; estimate missed matches by sampling pairs under looser blocking.
7. Check clusters for chaining: A matches B and B matches C while A and C clearly differ. Split or review large clusters.
8. Choose surviving values per field with stated rules (verified, most recent, source priority).
9. Store a mapping from old ids to surviving id plus pre-merge rows, repoint references, and get approval before changing the live system.

## Watch out for
- A false merge exposes one person's data to another and is much worse than a missed duplicate.
- Empty fields comparing equal inflate scores.
- Deleting losers without a mapping breaks foreign keys and makes undo impossible.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Measured precision on a labelled sample meets the agreed bar, no oversized cluster is unreviewed, and a sample merge can be reversed.
