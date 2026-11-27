---
name: ios-dynamic-type
version: 1.0.0
description: >
  Make iOS screens adapt to Dynamic Type including accessibility sizes, without truncation or overlap. Use when iOS text ignores the system size setting or large text breaks layouts.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - ios
  - accessibility
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: ios-dynamic-type
  official: true
  domain: frontend
  security_flags: []
---

# Ios Dynamic Type

## When to use
Users who enlarge text see clipped labels, fixed-height rows or no change at all.

## Steps
1. `grep` for `.font(.system(size:`, `UIFont.systemFont(ofSize:` and fixed frame heights around text.
2. In SwiftUI use text styles such as `.body` and `.headline`. For custom fonts use `Font.custom(_:size:relativeTo:)`.
3. In UIKit use `UIFont.preferredFont(forTextStyle:)` or `UIFontMetrics` to scale custom fonts, and set `adjustsFontForContentSizeCategory = true`.
4. Replace fixed heights with padding and minimum heights; set `numberOfLines = 0` or remove line limits on important text.
5. At accessibility sizes switch horizontal rows to vertical, using `dynamicTypeSize.isAccessibilitySize` with `AnyLayout` or `ViewThatFits`, or the trait collection in UIKit.
6. Scale spacing and icons that should grow with text using `@ScaledMetric` or `UIFontMetrics.scaledValue`.
7. Make screens scroll, including onboarding and sheets that fit only at default size, and keep primary buttons reachable.
8. For bars with fixed space, support the large content viewer.
9. Check with previews, Xcode's environment overrides and a device at the smallest, default and largest accessibility sizes on the narrowest supported phone, with a long translation.

## Watch out for
- `minimumScaleFactor` shrinks text back down and defeats the user's setting.
- Capping with `.dynamicTypeSize(...)` is a last resort for specific controls, never the app root.
- Text baked into images does not scale.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every in-scope screen has been viewed at the largest accessibility size with all text readable, no overlap, and all actions reachable by scrolling.
