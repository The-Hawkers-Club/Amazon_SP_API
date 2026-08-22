# The Hawkers Club USA LLC — SP-API Documentation Archive Incident Response Plan

**Scope:** This repo's own material — 422 PDFs of Amazon's copyrighted SP-API documentation,
republished on a **public** GitHub repo — and anything that must never land in it: credentials,
live seller data, or Amazon API response bodies. This repo holds no OAuth tokens and makes no
Amazon API calls itself; the live integration's own incident-response posture is
`amzn-api-integration`'s, not this document's.
**Owner:** [Hannah / named security owner] · **Last reviewed:** [DATE]

_Filled in once the same question is answered on the sibling archive
(`Amazon_Ads_API/PLAN/specs/SPEC-doc-archive-truth.md`, Question 1, pending). This document reuses
that answer rather than naming a different Incident Lead for the same estate — see
`docs/03-status.md` and `START-HERE.md` for why the brackets below are visible rather than filled._

## 1. Roles
- **Incident Lead** — [name]: coordinates response, decisions, and any external notification.
- **Technical Responder** — [name]: investigates, contains, and remediates.
- (For a small team, one person may hold both roles; a backup contact is named.)

## 2. Monitoring & detection
- The hourly `com.thc.amzn-api-doc-citations` guard (`spapi_doc_guard.py converge`) is the one
  standing automated check on this repo's own integrity: it detects a re-captured, renamed, or
  corrupted PDF (sha256 drift) and a citation in `../amzn-api-integration` that no longer resolves.
  It is a content-integrity control, not a security control, and does not detect credential leakage.
- Because this repo is **public**, any credential or live-data artifact committed to it must be
  treated as compromised the moment it is pushed — GitHub's own secret-scanning and any crawler
  that has indexed the repo since its public capture date (2026-07-04) are both out of our control.
- No client or seller data is ever expected here. If any file matching seller/order/PII shapes
  (order IDs, buyer names, addresses, financial data) is found in this repo, treat it as a data
  incident under this plan even though the file's origin would be `amzn-api-integration`'s.

## 3. Response steps
1. **Detect & triage** — confirm what was exposed: a credential, live seller/order data, or neither
   (a mis-scoped PDF is not, by itself, an incident — Amazon's own documentation is expected here).
2. **Contain** — if a credential was committed, rotate it immediately at its source
   (`amzn-api-integration`'s secrets manager; this repo never holds a live credential to rotate).
   If live data was committed, remove it from the working tree and from git history
   (`git filter-repo` / BFG), and note that a public repo's history may already be crawled —
   removal reduces exposure, it does not guarantee erasure.
3. **Report to Amazon**, if the exposure involves Amazon Information under the Data Protection
   Policy — notify **security@amazon.com within 24 hours** of detection, describing what happened,
   what was exposed, and remediation status. This mirrors the Ads-side attestation
   (`Amazon_Ads_API/docs/04-incident-response-plan.md:3`) rather than duplicating a separate
   commitment.
4. **Eradicate & recover** — confirm the offending content is gone from the default branch and,
   where feasible, from history; confirm the archive's own integrity guard (`verify --index`)
   still passes afterward.
5. **Notify** affected parties as required by contract, Amazon's policy, or applicable law.
6. **Post-incident review** — document root cause, timeline, and corrective action (e.g. a
   `.gitignore` rule, matching the existing `_THC-*.md` exclusion at `.gitignore:4-5`, if the cause
   was a specific file pattern).

## 4. Preventive controls (standing)
- No credential, access token, or client/seller data is ever committed here — this repo's only
  legitimate content is Amazon's published documentation PDFs and the markdown guides listed in
  `START-HERE.md`.
- The citation-integrity guard runs hourly and is the one automated check that would notice this
  repo's content silently changing shape.
- Extracted PDF text (the sidecars `spapi_doc_guard.py index` produces) is written **outside** this
  git repo, in the container's `.claude/spapi-index/`, specifically so a future automation mistake
  cannot commit derived Amazon text into a public tree.

## 5. Contacts
- Amazon security reporting: **security@amazon.com**
- Internal escalation: [Incident Lead contact], [backup contact]
