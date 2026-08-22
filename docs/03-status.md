# Project status — this archive's role posture

_Last updated: 2026-08-21_

This repo is **not** an integration — it is the offline documentation archive a **live** SP-API
integration cites by filename. The integration itself lives in
[`The-Hawkers-Club/amzn-api-integration`](https://github.com/The-Hawkers-Club/amzn-api-integration)
(`src/spapi/`, `src/spine/`). Everything on this page is sourced from that repo's own probes and
decision log, cited line by line, not re-probed here.

## The connection is live and good

**12 of 12 probed endpoints returned 2xx against a real seller connection**, 1,018 distinct field
paths observed (`amzn-api-integration/docs/SPAPI-SURFACE-INVENTORY.md:17-27`, verified 2026-07-26).

| Surface | API | Works |
|---|---|---|
| Account + marketplace participations | Sellers v1 | ✅ |
| Orders + order items | Orders v0 | ✅ |
| Transactions (v2024) + event groups + events (v0) | Finances | ✅ |
| FBA inventory summaries | FBA Inventory v1 | ✅ |
| Listings (own catalogue) | Listings Items 2021-08-01 | ✅ |
| Catalog items | Catalog Items 2022-04-01 | ✅ |
| Competitive pricing + item offers | Product Pricing v0 | ✅ |
| Reports (list + download) | Reports 2021-06-30 | ✅ |

## Role posture — what is granted and what is not

| Role | Held? | Evidence |
|---|---|---|
| **Inventory & Order Tracking** | ✅ Held | `GetShipmentDetails` (needs Amazon Fulfillment alone) → 403; the PO family (needs AF **or** I&OT) → 200. Reproduced 3× (`amzn-api-integration/DECISIONS.md:2651-2654`, 2026-07-27). |
| **Amazon Fulfillment** | ❌ Not held | Same probe as above; the 403/200 split isolates AF as the missing role. |
| **Brand Analytics** | ❌ Not held, and **PARKED by founder ruling OQ5** | *"Phase 3 (Data Kiosk vendor analytics) deferred; revisit before analytics phase. Do not apply for the role now."* (`amzn-api-integration/DECISIONS.md:1872`, OQ5, 2026-07-04). This page records the standing decision; it does not propose requesting the role. |
| **Restricted Data Token (RDT) / PII** | ❌ Not held | Buyer geography and `ShippingAddress.Name` are readable without an RDT; street address (`AddressLine1`) and buyer email are genuinely absent without one (`amzn-api-integration/docs/SPAPI-SURFACE-INVENTORY.md:92-101`, corrected 2026-07-27). |

## App model

Public-unlisted app model. Production carries **`APP_STATE=draft`**
(`amzn-api-integration/src/config/env.ts:82`, `appIsDraft: () => process.env.APP_STATE !== 'published'`).
Whether a draft app can be granted an additional role without publishing first was recorded as
UNVERIFIED and a 5-minute console check in `amzn-api-integration/DECISIONS.md:2657` — that question
belongs to `amzn-api-integration`, not to this archive.

## Measured rate limits — the spread that shapes any backfill design

Read from `x-amzn-RateLimit-Limit` on real responses; present on all 12 probed endpoints
(`amzn-api-integration/docs/SPAPI-SURFACE-INVENTORY.md:62-76`, 2026-07-26).

| Operation | req/sec | Note |
|---|---|---|
| `getOrders` | **0.0167** (~1/min) | 30× slower than the old 0.5 default assumed |
| `getMarketplaceParticipations` | 0.016 | 31× slower than assumed |
| `getAccount`, `getOrderItems`, `listTransactions`, `listFinancialEventGroups`, `listFinancialEvents`, `getCompetitivePricing`, `getItemOffers` | 0.5 | matches the old default |
| `getInventorySummaries`, `searchCatalogItems` | 2.0 | 4× faster than assumed |
| `searchListingsItems` | 5.0 | 10× faster than assumed |

The spread is ~300×, which is why a single global rate-limit default is wrong: `getOrders` at one
request per minute is the constraint that shapes any backfill design. Single-seller observation,
not a published contract — `observeHeader` stays authoritative at runtime
(`amzn-api-integration/docs/SPAPI-SURFACE-INVENTORY.md:76-77`).

## This repo's own posture

- **424 tracked files: 422 PDFs, `.gitignore`, `README.md`.** No source tree, no package manifest,
  no CI. Its job is reference material, guarded by the citation-integrity loop
  (`AMZN API/.claude/checks/spapi_doc_guard.py converge`, hourly).
- **GitHub visibility:** `The-Hawkers-Club/Amazon_SP_API` is **public**
  (unauthenticated `api.github.com` → HTTP 200, `"private": false`, checked live 2026-08-21) — see
  `README.md` for the founder ruling on whether it should stay that way.
- **Archive capture date:** all 422 PDFs share a single capture pass, 2026-07-04
  (`git log`, PDF `/CreationDate` metadata). See [`05-archive-index.md`](05-archive-index.md) for
  the full listing and [`06-coverage-report.md`](06-coverage-report.md) for which SP-API versions
  production now calls are and are not documented at that capture date.
