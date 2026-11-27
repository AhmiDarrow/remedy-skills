---
name: destructive-action-ux
version: 1.0.0
description: >
  Choose the right safeguard for delete, reset, revoke and bulk actions, favouring undo over habitual confirmation dialogs. Use when users lose data by accident or click through warnings.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
  - safety
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: destructive-action-ux
  official: true
  domain: design
  security_flags: []
---

# Destructive Action Ux

## When to use
A product has Are you sure dialogs everywhere, or one click can irreversibly destroy work.

## Steps
1. Inventory destructive and hard-to-reverse actions, noting what is lost, who else is affected, how often it is used and whether recovery truly exists. Check the backend rather than the button label.
2. Choose by tier. Reversible and personal: act immediately with Undo. Recoverable for a period: move to trash and say how long. Irreversible but contained: confirmation naming the object. Irreversible with wide impact: show consequences and require typing the name or re-authentication.
3. Make undo real by using soft delete or delaying the external effect until the window closes. Handle navigation and app close during that window.
4. Write the dialog with specifics: title as the action on the named object, body with counts and what also disappears, button labelled with the verb, never Yes or OK.
5. Place destructive controls away from frequent ones, style them distinctly with more than color, and do not make them the default focus.
6. For bulk actions show the exact number and a sample, especially when filters or select-all-matching are involved.
7. Offer a safer alternative where one exists, such as archive, disable or export first.
8. Handle partial failure by listing what was and was not affected.

## Watch out for
- Confirming routine actions trains people to dismiss the one that matters.
- An Undo in a short-lived toast is unreachable for many keyboard and screen reader users; provide a second recovery route.
- A client-side delay that never sends if the tab closes leaves the item undeleted although the screen said otherwise.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each inventoried action has an assigned tier, every offered undo or restore has been exercised end to end, and every remaining confirmation names the object and consequence.
