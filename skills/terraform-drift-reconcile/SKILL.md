---
name: terraform-drift-reconcile
version: 1.0.0
description: >
  Detect infrastructure that changed outside code, decide per difference whether to adopt or revert it, and add scheduled drift checks. Use when a plan shows changes nobody wrote.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - terraform
  - drift
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - grep
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: terraform-drift-reconcile
  official: true
  domain: ops
  security_flags: []
---

# Terraform Drift Reconcile

## When to use
Live resources and code disagree, often after a console fix during an incident.

## Steps
1. Plan from the exact commit last applied, so unapplied code changes are not mistaken for drift.
2. Run `terraform plan -refresh-only` to see how reality differs from state, then a normal plan to see what apply would do about it.
3. For each difference find who or what changed it, using cloud audit logs.
4. Classify: emergency fix to adopt into code; unauthorised or accidental change to revert; value owned by another system, such as an autoscaler's desired count; or provider noise from an upgrade.
5. Treat unexplained changes to access policies, firewall rules or logging as possible security incidents and tell the owner before reverting, since reverting can destroy evidence.
6. Adopt by editing code until the plan is clean. Use `ignore_changes` only for named attributes another system legitimately owns.
7. Revert through a reviewed apply, checking for replacement and downtime first.
8. Schedule a read-only `terraform plan -detailed-exitcode`: 0 no changes, 1 error, 2 changes present. Notify on 1 and 2.

## Watch out for
- Applying immediately can undo the fix that is keeping production up.
- A refresh-only apply updates state but not your code, so the next plan can still revert the change.
- Plan shows drift only for managed resources and tracked attributes; new unmanaged resources are invisible.
- Plan output can contain secrets, so restrict where the scheduled job publishes it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every difference has a recorded decision, the plan is clean, and the scheduled check has run once.
