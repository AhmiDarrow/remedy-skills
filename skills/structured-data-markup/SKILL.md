---
name: structured-data-markup
version: 1.0.0
description: >
  Add schema.org structured data in JSON-LD that matches visible page content, then validate it. Use when pages should describe products, articles, events or businesses to search engines.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - seo
  - schema
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - web.fetch
  - bash
metadata:
  source: library
  library_id: structured-data-markup
  official: true
  domain: frontend
  security_flags: []
---

# Structured Data Markup

## When to use
A page type could be described in machine-readable form.

## Steps
1. Identify the page's main entity and the matching schema.org type.
2. Fetch the target search engine's current documentation for that type: required and recommended properties, eligibility and policy. These change, and some result features get restricted or withdrawn.
3. Search the templates for existing markup, including plugin output, to avoid duplicates.
4. Generate JSON-LD in a `script type="application/ld+json"` element from the same data that renders the page.
5. Include only facts a visitor can see. Use absolute URLs and ISO 8601 dates with time zone where time matters.
6. Serialise with a JSON library and escape `<` so user content cannot close the script element.
7. Check the rendered output parses as JSON for several real records, including ones with missing fields; omit empty properties.
8. Run the schema.org validator and the engine's own tester, or ask the owner to.

## Watch out for
- Review or rating markup for reviews that are not shown, not genuine, or self-serving where policy forbids it.
- Stale price or availability hard-coded in the template.
- Telling the user valid markup guarantees a rich result.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Rendered markup parses and validates for sampled pages and every value matches visible content.
