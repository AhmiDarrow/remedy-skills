---
name: docx-template-fill
version: 1.0.0
description: >
  Fill a Word template, once or per spreadsheet row, without breaking layout or mixing records. Use for house-template letters, certificates, reports and mail merges.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - word-processing
  - templates
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: docx-template-fill
  official: true
  domain: docs
  security_flags: []
---

# Docx Template Fill

## When to use
An existing template must be populated with specific values.

## Steps
1. List every placeholder, searching body, tables, headers, footers, text boxes and footnotes. Unzip a copy and inspect the XML if some do not show up in the library.
2. Identify the mechanism: content controls, merge fields, or plain tokens such as `{{name}}`.
3. Collect values in a small data file and match them one to one with placeholders. Report missing and unused ones.
4. Replace in a way that handles tokens split across several runs: join the paragraph's run text to locate the token, put the value in the first affected run, and trim the others so formatting survives. A templating library that handles this is preferable if installed.
5. For repeating rows, clone the template row, then remove the sample row.
6. Remove optional sections as whole paragraphs, including their headings.
7. Save as a new .docx (convert a .dotx properly; renaming is not enough).
8. For one file per spreadsheet row: read IDs and postcodes as text, agree what blank fields produce, get approval on samples (typical, longest, most blanks), use unique filenames with a row ID, write a row-to-file manifest, and also search outputs for "None", "nan" and "NaT". This produces files; sending is the user's step.
9. Render to PDF, view every page, then search the output text for `{{`, `}}`, "TODO", sample names and leftover instructional text.

## Watch out for
- Template metadata and old headers may carry a previous client's name.
- Long values push signature blocks to a new page; test with the longest realistic input.
- Format dates, currency and decimals before insertion to the recipient's convention.
- Sorting one data column without the others puts one person's details in another's letter; check sampled files against a single source row.
- Never reuse the previous output file as the next template.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The rendered file has no placeholders or sample data, layout matches the template, and every value matches the data file.
