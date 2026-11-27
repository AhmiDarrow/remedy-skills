---
name: terraform-state-surgery
version: 1.0.0
description: >
  Move, rename or detach resources in Terraform or OpenTofu state without destroying real infrastructure. Use when refactoring modules makes a plan want to delete and recreate existing resources.
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
  - edit
  - grep
metadata:
  source: library
  library_id: terraform-state-surgery
  official: true
  domain: ops
  security_flags: []
---

# Terraform State Surgery

## When to use
Resources need a new address, must move between configurations, or should stop being managed while continuing to exist.

## Steps
1. Check the tool and version and confirm the backend and workspace. Make sure nobody else or any pipeline will run meanwhile.
2. Back up state with `terraform state pull` into a protected location outside the repository, because state can contain secrets.
3. Get a baseline plan and settle unrelated changes first.
4. For renames and module moves within one configuration, add `moved` blocks. They are reviewable and apply for every consumer.
5. To stop managing a resource without deleting it, use a `removed` block with `destroy = false` where the installed version supports it, otherwise `terraform state rm <address>`.
6. To move between two configurations, import into the destination and remove from the source in one controlled window, so exactly one state owns it at the end.
7. Quote addresses that contain `count` or `for_each` keys; syntax differs between shells.
8. Run `terraform plan` and read every line. A pure move shows no create or destroy.
9. Apply only a saved plan the owner has seen.

## Watch out for
- `state rm` followed by an apply with the code still present creates a duplicate.
- Editing the state JSON by hand risks corrupting serial and dependency data.
- `force-unlock` is only for a lock whose owner is confirmed dead; breaking a live lock allows concurrent writes.
- Switching `count` to `for_each` changes every instance address, so each needs a mapping.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The plan for every affected configuration shows no unintended create, replace or destroy, and each real resource is tracked by exactly one state or deliberately by none.
