---
name: email-template-review
version: 1.0.1
description: >
  Review HTML email templates for client rendering, plain-text parts, escaping of user data, safe links and unsubscribe handling. Use before shipping or changing a transactional or bulk email.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - email
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: email-template-review
  official: true
  security_flags: []
---

# Email Template Review

## When to use
A template or the code that renders and sends it is new or changed.

## Steps
1. Find the template, its render code, subject line, sample data and required clients. Note whether it is transactional or marketing.
2. Check escaping for every variable by context: body, attributes, URLs. Find raw-output syntax and trace whether users control the value. Reject line breaks in anything used in headers such as subject, name or reply-to.
3. User-controlled text in an email from your domain is a phishing tool: limit and neutralise names or messages that mail programs may auto-link.
4. Check security links: HTTPS, base URL from server config (not the request Host header), single-use expiring tokens, and no state change on a plain GET, since mail scanners open links.
5. Rendering: table layout for structure where old clients matter, critical styles inline, constrained fluid width, no scripts, forms or external stylesheets. Classic Outlook on Windows ignores much modern CSS.
6. Images need width, height and alt text; the message must make sense with images blocked.
7. Accessibility: `lang`, `role="presentation"` on layout tables, readable text size and contrast, descriptive links, real text instead of text in images.
8. Check the plain-text part carries the same facts and working links. Keep HTML small; some clients clip large messages (Gmail at about 102 KB).
9. For marketing mail, check consent basis, working unsubscribe, `List-Unsubscribe` headers (one-click for bulk senders) and required sender identification; legal duties vary by country.
10. Render with empty, very long and hostile sample values. List clients actually tested. Send test mail only to addresses the user approves.

## Watch out for
- Dark mode in some clients recolors the message and can make logos or buttons vanish.
- Click tracking that rewrites login or reset links and passes tokens through a third party.
- A browser preview presented as client testing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Findings are ranked with file and line, hostile sample values render harmlessly, the text part is complete, and untested clients are named.
