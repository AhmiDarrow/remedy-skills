---
name: json-schema-design
version: 1.0.1
description: >
  Design a strict, bounded schema in JSON Schema, Zod or Pydantic with valid and invalid fixtures. Use when defining the shape of an API body, config file, message or structured output.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - data
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: json-schema-design
  official: true
  security_flags: []
---

# Json Schema Design

## When to use
Data crossing a boundary needs a defined and enforced shape.

## Steps
1. Collect real or realistic samples, including the oddest ones, and `grep` the code that consumes them. Samples show what happens; the owner decides what is allowed.
2. Check the library or draft version in use, since keywords and defaults differ.
3. Specify each field's type, presence and nullability separately: optional, nullable and empty are three things.
4. Bound strings, numbers, arrays, maps, nesting and total payload size. Keep money and large ids out of floating-point numbers.
5. For variants, use a discriminator field with one closed object per variant rather than many optional fields.
6. Decide about unknown fields: reject for requests and config to catch typos; tolerate in consumers that must survive additions. Know the default: Zod objects strip unknown keys and Pydantic models ignore them unless configured. In JSON Schema, `additionalProperties: false` does not see properties from sibling `allOf` branches; later drafts offer `unevaluatedProperties`.
7. Decide about coercion. Lax modes may turn `"5"` into a number; use strict parsing where that matters.
8. Confirm `format` is actually enforced; many JSON Schema validators treat it as annotation by default.
9. Write valid fixtures and one invalid fixture per constraint, assert the failing path, and run them.

## Watch out for
- Regexes with nested repetition can hang on hostile input; bound length first.
- Cross-field rules and authorization do not follow from a valid shape.
- Tightening a schema over stored data rejects old records; test against them.
- Error messages that echo whole inputs may log secrets.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every field has stated type, presence and bounds, valid fixtures pass, each invalid fixture fails for its intended reason, and compatibility with existing data is checked.
