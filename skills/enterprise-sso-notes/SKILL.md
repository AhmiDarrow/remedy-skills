---
name: enterprise-sso-notes
version: 1.0.1
description: >
  Plan or review a SAML single sign-on integration: metadata exchange, assertion validation, account linking, provisioning and certificate rollover. Use when a business customer asks for SSO or a SAML login fails.
author: Remedy Official
license: Apache-2.0
tags:
  - auth
  - enterprise
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: enterprise-sso-notes
  official: true
  security_flags: []
---

# Enterprise Sso Notes

## When to use
Your application is the SAML service provider and must trust a customer's identity provider. Misconfiguration is common, so use a mature, maintained library and never hand-parse or hand-verify XML.

## Steps
1. Exchange metadata per customer: your entity ID and assertion consumer service (ACS) URL; their entity ID, sign-on URL and signing certificates. Store each connection against exactly one tenant.
2. Require signed assertions. Verify against the certificate configured for that connection, never one taken from the response. Read identity data only from the element whose signature was verified, which is the defence against signature wrapping.
3. Also check Issuer, Audience, Destination, Recipient, the NotBefore and NotOnOrAfter window with small clock skew, and InResponseTo for logins you started. Record assertion IDs until expiry to reject replays. Disable external entities and DTDs.
4. Decide whether identity-provider-initiated login is needed. It has no InResponseTo to check, so leave it off unless a customer requires it. Allow only local or allowlisted RelayState targets.
5. Map users by connection plus a stable identifier, not a changeable email. Accept email domains only if verified for that tenant, so one customer's provider cannot sign in as another's user.
6. Choose provisioning: invite only, or just-in-time creation with a default low role. Define how group attributes map to roles. Login alone does not deprovision; use SCIM or a documented manual removal process, and set a session lifetime.
7. Plan certificate rollover by accepting two certificates at once, with an expiry alert.
8. Test with a staging identity provider: valid login, unsigned, tampered, expired, wrong audience, replayed, and a cross-tenant email. Keep a recovery admin login for when enforced SSO breaks.

## Watch out for
- The ACS request is a cross-site POST, so `SameSite=Lax` or `Strict` cookies holding request state are not sent.
- Logging whole responses puts personal data in logs.
- Single logout is unreliable across providers; do not depend on it for access removal.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The connection settings are documented per tenant, every rejection case above fails in a test or is listed as untested, and rollover and deprovisioning each have an owner.
