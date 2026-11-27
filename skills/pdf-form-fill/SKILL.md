---
name: pdf-form-fill
version: 1.0.0
description: >
  Fill a PDF form from information the user provides and verify it renders in common viewers. Use for fillable applications and flat forms that need text placed on them.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - pdf
  - forms
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: pdf-form-fill
  official: true
  domain: docs
  security_flags: []
---

# Pdf Form Fill

## When to use
The user wants a form completed and will review and submit it themselves.

## Steps
1. Detect the type: list form fields with an installed PDF library (for example pypdf `get_fields()`), or note that the page is flat or scanned.
2. Render the pages and map internal field names to visible labels; names like `Text17` mean nothing by themselves.
3. For checkboxes and radio buttons, read each field's allowed export values rather than assuming "Yes".
4. Collect answers. List missing ones and ask; never invent a plausible value.
5. Leave signatures, sworn declarations, government ID numbers, bank and card details, and passwords for the user to enter themselves.
6. Fill a copy. For flat forms, place text at measured coordinates and test one page first.
7. Render the result to images and inspect for clipped text, shrunken fonts, wrong boxes and blank-looking fields. Viewers differ if field appearances are not regenerated.
8. Give the user a field-by-field list of entries, blanks and assumptions to approve.
9. Flatten only after approval and only if the recipient wants a non-editable file.

## Watch out for
- Dynamic XFA forms often fail in general libraries and many viewers; use a viewer that supports them and fill manually.
- Date formats and character limits vary per field.
- A value can be stored yet invisible, so checking field data alone is not enough.
- Legal or tax questions on a form need the user's or a professional's answer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The rendered copy shows every entry in the right place, user-only fields are listed as theirs to complete, and nothing has been submitted.
