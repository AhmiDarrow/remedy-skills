---
name: frontend-a11y
version: 1.0.1
description: >
  Audit and fix the highest-impact accessibility defects in web UI code: semantics, names, keyboard operation, focus, images and errors. Use when auditing a page or component or fixing a report.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - a11y
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
  - computer.navigate
  - computer.snapshot
  - computer.key
metadata:
  source: library
  library_id: frontend-a11y
  official: true
  security_flags: []
---

# Frontend A11Y

## When to use
Web UI code needs checking against WCAG (default 2.2 AA) or someone cannot operate it.

## Steps
1. Scope the critical user flows and components. Run the project's accessibility lint or tests, and axe or Lighthouse on rendered states if available, including opened menus, dialogs and errors.
2. `grep` for common defects: click handlers on `div` or `span`, `outline: none` without a replacement, positive `tabindex`, `aria-hidden` around focusable content, inputs without labels, images without `alt`.
3. On a local or test build (on a live site, stop and ask before anything that submits, buys, sends or deletes), do each flow by keyboard only: everything reachable and operable, logical order, visible focus, no trap, focus not hidden under sticky bars, focus restored after overlays close.
4. Prefer native `button`, `a href`, `input`, `select` and `dialog`. A role adds no behaviour; if a custom widget is unavoidable, follow the ARIA Authoring Practices keyboard pattern or reuse a tested component.
5. Inspect the accessibility tree: each control has a correct role, state and a name that includes its visible label. Decorative images get `alt=""`; informative ones describe purpose.
6. Check headings, landmarks, `lang`, page title, table headers, and that dynamic results and errors are announced.
7. Check contrast, 200% zoom, 320 CSS pixel reflow and reduced motion.
8. Fix blockers of a task first, ideally in the shared component, and add a regression test that queries by role and name.
9. Re-run checks and report what still needs a screen reader or a human judgement.

## Watch out for
- A clean automated scan covers only part of the criteria and cannot judge whether names make sense.
- `aria-label` replaces visible text for assistive technology and is unreliable on generic elements.
- `role="menu"` on site navigation promises arrow-key behaviour that is usually not there.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The scoped flows work by keyboard, fixed controls expose correct names and states, automated checks were re-run, and untested items are listed.
