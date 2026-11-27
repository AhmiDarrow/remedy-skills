---
name: dataset-anonymization-share
version: 1.0.0
description: >
  Prepare a dataset for sharing by minimising and de-identifying it, then testing re-identification risk. Use before sending real records to partners, researchers, test environments or the public.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - data
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - owner.notify
metadata:
  source: library
  library_id: dataset-anonymization-share
  official: true
  domain: security
  security_flags: []
---

# Dataset Anonymization Share

## When to use
Data about people is about to leave its original controlled context.

## Steps
1. Confirm purpose, recipient, permission to share and whether a legal or ethics review is required. Ask whether aggregates or synthetic data would be enough.
2. Work on a copy in a restricted location, not in a repository.
3. Classify every column: direct identifier, quasi-identifier (birth date, postcode, sex, job, timestamps, location), sensitive attribute, or harmless.
4. Drop columns the purpose does not need.
5. Remove direct identifiers. If linkage across tables is needed, use random tokens or a keyed hash with the key withheld, and call the result pseudonymised, not anonymous.
6. Generalise quasi-identifiers: age bands, coarser areas, shifted or truncated dates.
7. Measure group sizes over quasi-identifier combinations. Suppress or merge groups below the agreed minimum (k), and check that sensitive values within a group are not all the same.
8. Inspect free text, filenames, IDs with embedded meaning, image metadata, row order and rare outliers.
9. Consider what the recipient could join with. For public release of statistics, consider differential privacy with expert help.
10. Document transformations and residual risk, and obtain the data owner's approval before the user sends it.

## Watch out for
- Unsalted hashes of emails or phone numbers can be reversed by guessing.
- A few location points or timestamps can single out a person.
- Releasing two filtered versions allows subtraction to reveal individuals.
- Passing k-anonymity does not make data safe from every inference.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The export contains only justified columns, group-size results meet the agreed threshold, residual risk is written down and the owner approved release.
