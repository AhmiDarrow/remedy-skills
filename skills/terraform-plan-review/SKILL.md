---
name: terraform-plan-review
version: 1.0.1
description: >
  Review a Terraform or OpenTofu plan for replacements, data loss, public exposure and permission growth before apply. Use when a plan or infrastructure pull request needs approval.
author: Remedy Official
license: Apache-2.0
tags:
  - iac
  - devops
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: terraform-plan-review
  official: true
  security_flags: []
---

# infrastructure-as-code Plan Review

## When to use
Someone is about to apply infrastructure changes.

## Steps
1. Confirm repository commit, directory, workspace, variables, account and region, and state backend with locking. A plan for the wrong environment can look reasonable.
2. Prefer the saved plan that will be applied. If creating one is approved, run `plan -out=<file>`. Planning refreshes state and runs providers and external data sources, so do not plan untrusted code with real credentials.
3. Read `show <file>`, and use `show -json` to list `resource_changes` and their actions. Plan files and JSON can contain secrets in clear text; keep them out of Git and chat and delete copies afterward.
4. Count creates, updates, deletes and replacements. A delete with a create means replacement; check the order and the attribute marked as forcing it.
5. For databases, disks, buckets, keys, DNS and networks, determine what data or identity is lost, downtime, and whether deletion protection, final snapshots and tested backups exist.
6. For renames or module moves, expect `moved` blocks rather than destroy and create. Question unexplained changes that suggest drift or a provider upgrade, and review lock file changes.
7. Check exposure: ingress from `0.0.0.0/0` or `::/0`, public addresses, public storage, disabled encryption or logging.
8. Check permissions: wildcards, trust policies, cross-account principals, role passing and identity grants that allow escalation.
9. Examine values known only after apply, provisioners, cost-bearing resources and quota effects.
10. Give a verdict per risk with resource address and evidence. Do not apply. If code or state changes, require a new plan.

## Watch out for
- Reading only the summary line; one replacement can be the production database.
- Reviewing one plan and applying a fresh, different one.
- `-target` hiding dependent changes.
- Assuming `prevent_destroy` protects a resource whose block has been removed from the code.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every delete and replacement is explained, exposure and permission changes are assessed, blockers and unknowns are listed, and no apply was run.
