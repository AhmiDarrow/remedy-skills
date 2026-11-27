---
name: autofill-friendly-forms
version: 1.0.0
description: >
  Make login, address and checkout forms work with browser autofill, password managers and mobile keyboards. Use when saved details fill the wrong fields or phones show the wrong keyboard.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - forms
  - accessibility
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: autofill-friendly-forms
  official: true
  domain: frontend
  security_flags: []
---

# Autofill Friendly Forms

## When to use
Password managers fail on sign-in, address autofill scrambles fields, or one-time codes cannot be filled from the keyboard suggestion.

## Steps
1. Read each form's rendered HTML, not only the component source, and confirm real `form`, `label`, `input` and submit button elements.
2. Give every field a stable `name`, `id` and the right `autocomplete` token: `username`, `current-password`, `new-password`, `one-time-code`, `name`, `email`, `tel`, `street-address` or `address-line1`, `postal-code`, `country`, `cc-number`, `cc-exp`.
3. Prefix with `shipping` or `billing` where both appear.
4. Choose `type` and `inputmode` by data: `type="email"`, `type="tel"`, and for digit strings such as codes use `type="text" inputmode="numeric"`.
5. Add `autocapitalize`, `spellcheck="false"` and `enterkeyhint` where they help.
6. Keep a one-time code in a single input; if boxes are a visual requirement, still back them with one field.
7. Allow paste everywhere and offer a show-password toggle that does not clear the value.
8. Handle autofill in state: read values on input and change events and again at submit.
9. For password change forms include the username field, visually hidden if necessary, so the manager updates the right entry.
10. Test with at least two browsers and one mobile device using fake test data; the user types any real credentials.

## Watch out for
- `type="number"` strips leading zeros, adds spinners and changes on scroll; it is wrong for codes, cards and postal codes.
- `autocomplete="off"` on login fields is often ignored and annoys users where it works.
- Splitting names or phone numbers into many boxes defeats autofill and excludes valid formats.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
In the tested browsers saved test profiles fill each field correctly in one action, the intended keyboard appears on mobile, and the submitted values match what is shown.
