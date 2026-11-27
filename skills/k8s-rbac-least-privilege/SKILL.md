---
name: k8s-rbac-least-privilege
version: 1.0.0
description: >
  Review Kubernetes roles, bindings and service accounts for excess permissions and escalation paths, then narrow them safely. Use when auditing cluster access or an app asks for cluster-admin.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - kubernetes
  - access
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
  - write
metadata:
  source: library
  library_id: k8s-rbac-least-privilege
  official: true
  domain: security
  security_flags: []
---

# K8S Rbac Least Privilege

## When to use
Service accounts, CI deployers or people hold broad cluster permissions that nobody has justified.

## Steps
1. List ClusterRoleBindings and RoleBindings with their subjects. Start with anything bound to `cluster-admin`, to `system:authenticated`, `system:unauthenticated` or a `default` service account.
2. For each non-human subject, run `kubectl auth can-i --list --as=system:serviceaccount:<ns>:<name>` in each relevant namespace.
3. Flag powerful grants: wildcards; the verbs `escalate`, `bind` and `impersonate`; reading secrets (list and watch return contents too); creating pods or workload controllers, which lets the creator mount that namespace's secrets and use its service accounts; `pods/exec`; `nodes/proxy`; writing RBAC objects or admission webhooks.
4. Find what each workload really calls from API audit logs if enabled, otherwise from its documentation and code.
5. Write namespaced Roles with explicit resources and verbs. Use `resourceNames` where the target is fixed, noting it cannot restrict create.
6. Give each app its own service account, and set `automountServiceAccountToken: false` where it never calls the API.
7. Apply the new binding, check required actions with `can-i`, then remove the broad one after the owner approves.
8. Watch for forbidden errors through scheduled jobs and a full deploy.

## Watch out for
- Permissions accumulate across all bindings, so adding a narrow role changes nothing until the broad one is gone.
- A RoleBinding to a ClusterRole grants it only in that namespace; a ClusterRoleBinding grants it everywhere.
- Removing your own admin path before testing another one can lock you out.
- Cloud identity mappings may grant cluster access outside RBAC listings.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No workload keeps an unjustified wildcard or cluster-admin binding, required calls succeed, and one removed permission is shown to be denied.
