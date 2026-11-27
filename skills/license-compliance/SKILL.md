---
name: license-compliance
version: 1.0.1
description: >
  Inventory third-party licences in what a project ships and flag obligations or unknowns for review. Use before distributing, selling or open-sourcing software with dependencies.
author: Remedy Official
license: Apache-2.0
tags:
  - legal
  - deps
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
  - write
  - web.fetch
metadata:
  source: library
  library_id: license-compliance
  official: true
  security_flags: []
---

# License Compliance

## When to use
Someone needs to know which licences travel with a product. This is an inventory and flagging task, **not legal advice**; a qualified person decides on obligations and conflicts.

## Steps
1. Establish how it is used and delivered: internal only, hosted service, shipped binary, mobile app, library or source release. Note the project's own licence.
2. Read manifests, lock files, existing NOTICE files, vendored and copied code, container base images, system packages, fonts, icons, media, datasets and model files. Package scanners miss many of these.
3. Use a scanner matching the ecosystem, such as `pip-licenses`, `cargo deny check licenses` or `go-licenses`. Run it against the resolved environment; ask before installing a tool.
4. Separate what ships from development and test tools, checking whether any of those copy code into the output.
5. Verify unclear, custom, missing and high-impact entries against the licence file of the exact version. Metadata can be wrong.
6. Record package, version, SPDX identifier or "unknown", source, shipped or not, modified or not and how it is linked.
7. Group for review: permissive; file or library level copyleft (such as MPL or LGPL); strong or network copyleft (such as GPL or AGPL); source-available or use-restricted terms; no licence or unknown. No licence does not mean free to use.
8. Read dual licence expressions carefully: OR offers a choice, AND applies both.
9. Draft the attribution file from actual licence and NOTICE texts, preserving copyright lines.
10. List questions for legal review with the facts, and add a repeatable check for new dependencies.

## Watch out for
- Assuming a hosted service has no obligations; AGPL has terms about network use.
- Missing licence changes between versions.
- Guessing a licence from the package's reputation.
- Replacing or removing notices to tidy the list.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Everything shipped has a versioned entry with a verified or unknown status, flagged items have a named question, and the report says which areas were not scanned.
