---
name: literature-database-search
version: 1.0.0
description: >
  Run a reproducible search of scholarly literature with defined terms, databases and inclusion rules. Use for a literature review or a "what has been studied on this" question.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - academic
kind: native
status: discovered
tools:
  - web.search
  - web.fetch
  - write
metadata:
  source: library
  library_id: literature-database-search
  official: true
  domain: docs
  security_flags: []
---

# Literature Database Search

## When to use
The user needs coverage of published research they can describe and repeat, not a few interesting papers.

## Steps
1. Write the question and split it into 2 to 4 concepts. For each, list synonyms, older terms, spelling variants and any controlled subject headings.
2. Join synonyms with OR inside a concept and join concepts with AND. Adjust syntax per database.
3. Choose at least two sources suited to the field, plus preprint servers if the topic moves quickly. Ask which databases the user's library gives them.
4. Set inclusion and exclusion rules before reading results: years, languages, study types, populations.
5. Test the query against 3 to 5 papers you know belong. If it misses one, find the missing term.
6. Log database, exact query string, date and hit count for every run.
7. Screen titles and abstracts, then full texts, recording one reason for each full-text exclusion.
8. Snowball from the strongest included papers: their references backward and their citing papers forward.
9. Deduplicate by DOI, then by normalised title and year.

## Watch out for
- Never cite a paper you have not located. Every entry needs a resolvable record.
- Reading only abstracts misrepresents methods and effect sizes; label which items were abstract only.
- This is not automatically a systematic review. That term implies a protocol and screening standards you should not claim unless followed.
- Do not bypass paywalls; point to library access or legitimately open copies.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A search log lets someone rerun every query, and each included item has a verified record and an access level.
