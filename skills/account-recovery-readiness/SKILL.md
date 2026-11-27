---
name: account-recovery-readiness
version: 1.0.0
description: >
  Make sure key personal accounts can still be recovered if a phone, number, email or password is lost. Use before travel or a phone change, or when checking for lockout risk.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - tech-help
  - accounts
kind: native
status: discovered
tools:
  - read
  - write
  - todo
metadata:
  source: library
  library_id: account-recovery-readiness
  official: true
  domain: personal
  security_flags: []
---

# Account Recovery Readiness

## When to use
Someone wants to know they will not be locked out of email, banking, cloud storage or their password manager.

## Steps
1. List the accounts that would hurt most to lose, starting with primary email, platform accounts, password manager, phone carrier and banking. No passwords go in the list.
2. For each, the person views the security page and reports sign-in method, two-step methods, recovery email and phone, and recovery codes.
3. Draw the dependencies: which account resets which. Look for loops, such as the password manager's second step living only inside itself.
4. Run a loss scenario for each: phone gone, number gone, home inaccessible, email suspended. Mark where no route remains.
5. Add a second independent method where offered, such as a spare security key, passkey on another device or printed codes.
6. Store codes offline somewhere safe that does not depend on the lost item.
7. Remove stale numbers and old addresses.
8. Set up official emergency or legacy access for a trusted person if wanted, then verify one recovery route without signing out of the only working session.

## Watch out for
- A recovery address at an old employer or school.
- Used or regenerated codes making the printed sheet invalid.
- Testing recovery in a way that triggers a lockout waiting period.
- Never ask for codes, keys or master passwords in chat.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each critical account survives the loss of the phone on paper, with dated recovery methods and no circular dependency.
