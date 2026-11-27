---
name: terraform-import-existing
version: 1.0.0
description: >
  Bring hand-created cloud resources under Terraform or OpenTofu control using import blocks until the plan is clean. Use when infrastructure was built in a console and needs to become code.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - terraform
  - infrastructure
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - web.fetch
metadata:
  source: library
  library_id: terraform-import-existing
  official: true
  domain: ops
  security_flags: []
---

# Terraform Import Existing

## When to use
Real resources exist that no state manages.

## Steps
1. Inventory what to import with read-only listing commands, and confirm no other state or tool already owns any of it.
2. Order by dependency and start with a small group that is cheap to get wrong.
3. Look up each resource type's import ID format in the provider documentation for the pinned version. IDs vary: names, ARNs, paths or composite strings.
4. Write `import` blocks with `to` and `id`.
5. Where supported, run `terraform plan -generate-config-out=generated.tf` for a draft, targeting a file that does not yet exist.
6. Clean the draft: remove computed or default noise and conflicting arguments, replace literal IDs with references, and add variables only where values really differ.
7. Plan repeatedly until the result is imports only. Treat every proposed update as a difference to explain: fix the code to match reality unless the owner wants reality changed.
8. Search especially for forced replacement markers.
9. Apply the reviewed saved plan, run plan again, and expect no changes.
10. Add `prevent_destroy` to data stores.

## Watch out for
- Many providers split one console object into several resources (rules, policies, attachments). Importing the parent leaves the rest unmanaged or, with inline blocks, in conflict.
- Some arguments cannot be read back, such as passwords, so plans may show perpetual differences.
- Provider defaults can silently differ from the live setting and get applied.
- Generated code and state may contain sensitive values; review before committing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All listed resources are in state, a fresh plan reports no changes, and nothing was replaced during the import.
