---
name: file-upload-secure
version: 1.0.1
description: >
  Harden a file upload and download feature: authorization, size limits, type validation, storage keys, processing isolation and safe serving. Use when adding or reviewing any place users can upload files.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - backend
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: file-upload-secure
  official: true
  security_flags: []
---

# File Upload Secure

## When to use
Untrusted users supply files that your system stores, processes or serves back.

## Steps
1. Trace every path from upload to download, including direct-to-storage links, imports by URL, thumbnails and admin viewers.
2. Check authorization on upload, list, download, replace and delete, against the object's owner and tenant, not just a logged-in session.
3. Cap size at the proxy and the application while streaming, plus per-user quota and file count. For direct uploads, constrain size in the signed policy where the storage supports it (a presigned POST can bound length; do not assume a presigned PUT does), and verify the stored object before accepting it.
4. Allowlist the extensions the feature needs. Treat the client's content type as a claim; check the content and, for images, decode and re-encode.
5. Generate the storage key server-side. Keep the original name only as metadata, sanitised before it appears in a header. Store outside any web root or executable path.
6. Parse in an isolated, resource-limited worker. For archives, reject entries that escape the target folder or are links, and cap expanded size, entry count and nesting.
7. If files are shared between users, hold them as pending until any malware scan passes.
8. Serve with `Content-Disposition: attachment` unless inline display is required, `X-Content-Type-Options: nosniff` and a content type you chose. Serve user content from a separate origin. Use short-lived signed links for private files.
9. Test with oversize, renamed executable, HTML and SVG with script, traversal name, archive bomb sample made locally and another user's file ID.

## Watch out for
- SVG and HTML served inline on your main origin run script as your site.
- Magic bytes match polyglot files too; they are one check, not proof.
- Image metadata can carry location; strip it if files are shared.
- Image and document libraries have their own flaws; keep them patched.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each abuse test is rejected or rendered harmless with recorded results, and downloading another user's file is denied.
