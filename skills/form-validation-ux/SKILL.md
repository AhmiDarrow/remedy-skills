---
name: form-validation-ux
version: 1.0.1
description: >
  Fix form validation so errors appear at the right moment, are announced, map server responses to fields and never lose input or double-submit. Use when users get stuck or confused on a form.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - ux
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: form-validation-ux
  official: true
  security_flags: []
---

# Form Validation Ux

## When to use
An existing or new form has noisy, late, vague or inaccessible errors.

## Steps
1. Read the form, its validation library and the server's rules and error format. Client checks help the user; the server still validates everything.
2. Align rules. Remove client rules stricter than the server that reject real names, plus-addressed emails, spaces in phone numbers or international postcodes.
3. Set timing: do not flag a field while it is first being typed. Validate on leaving it or on submit, then revalidate as the user corrects it. Run cross-field checks when both have values.
4. Keep submit enabled in general and explain what is wrong on press; a silently disabled button gives no clue.
5. Give each field a visible label. Put the message beside it, link it with `aria-describedby`, set `aria-invalid`, and use text as well as color.
6. On failed submit, focus the first invalid field, or an error summary with links when the form is long.
7. Map server field paths (including array items) to inputs. Show unmapped and form-wide errors in a visible summary; never drop them.
8. Handle network failure, timeout, expired session, 409 and 429 without clearing input.
9. While submitting, block repeat sends including the Enter key, show progress, and always restore the button on every outcome. For creating or paying, also use a server idempotency key.
10. Test with keyboard only, autofill, pasted values with surrounding spaces, slow network and a rejected server response.

## Watch out for
- An older asynchronous check (username taken) overwriting the result for newer input; match responses to the current value.
- Trimming or reformatting passwords.
- Native browser bubbles and custom messages both firing.
- A timeout does not prove the server failed, so a blind retry can create duplicates.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Client and server errors appear on the right fields with focus and announcement, input survives every failure, and rapid double submission sends one effective request.
