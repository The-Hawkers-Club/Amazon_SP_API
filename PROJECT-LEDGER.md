# Project Ledger — AMZN API/Amazon_SP_API

> Every project running in this repo, every open item under it, and every cross-referral ask it is
> waiting on. **Canonical open-items store.**

**Protocol:** OIL v5.5.0
**Page:** https://oil-web-production.up.railway.app/r/Amazon_SP_API
**Installed:** 2026-08-21 (oil-install.py)
**Last reconciled:** never — the first /wrap performs the first reconcile
**Next IDs:** PRJ-001 · OI-0002 · XA-001

## Portfolio

| ID | Project | Status | WS | 👤 | 🤖 | 🔗 | ⚪ | Open total | Oldest open | Last touched |
|----|---------|--------|----|----|----|----|----|-----------|-------------|--------------|
| PRJ-000 | Unfiled | STANDING | W0 | 0 | 0 | 0 | 1 | 1 | 2026-08-21 | 2026-08-21 |

**Reconciliation:** Σ project open totals = 1 · non-terminal rows in typed tables = 1 ✅

---

# PRJ-000 — Unfiled

> The mandatory residual. Items land here when their project is genuinely unclear, **with the reason
> recorded**. Never `DONE`; drained by filing its rows, not by closing them.

**Goal:** every item this repo carries is either owned by a real project, or sits here for a recorded
reason — nothing is silently lost.

| Item | Wk | Description | Type | Status | Opened | Updated |
|------|----|-------------|------|--------|--------|---------|
| OI-0001 | W0 | ⚪ **All 10 build steps in `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` are built.** `.claude/spapi-index/` holds a manifest row + text sidecar for all 422 PDFs; `docs/05-archive-index.md` and `docs/06-coverage-report.md` are generated (coverage's family-match window fixed to avoid Amazon's shared site-nav boilerplate false-positiving every family — see spec Items); the citation guard resolves 56 exact + 12 suffix + 2 glob, 0 dangling; `spapi_doc_guard.py`'s 13 unit tests and 10 named mutants are green (control GREEN, every mutant reddens exactly its predicted test); the hourly `com.thc.amzn-api-doc-citations` LaunchAgent is loaded and confirmed CLEAN end-to-end; `START-HERE.md`/`docs/01-04`/`README.md` describe this repo's actual (public) visibility. DoD block run verbatim from the spec: `bash /tmp/spapi-dod.sh > /tmp/spapi-dod.log 2>&1; echo "EXIT=$?" >> /tmp/spapi-dod.log` → **EXIT=0**. | ⚪ | `DONE` | 2026-08-21 | 2026-08-22 |

## Requests this repo has sent — XREPO OUTBOX

Work this repo has filed into ANOTHER repo's ledger. `SENT` means the instruction and their row exist; it does not mean they have executed it. It closes when their answer lands back here as a row.

<!-- MANAGED BY ~/.claude/tools/xrepo-relay.py — do not hand-edit rows in this table.
     Column order is fixed because the tool reads it back; a hand-edit that shifts a column
     silently changes what `inbox`/`answer`/`--check` believe. Add context in the linked
     markdown file instead, which is unbounded and is what the executor actually reads. -->

| ID | To | Ask | Status | Instruction | Answer | Sent | Answered |
|----|----|-----|--------|-------------|--------|------|----------|
| XR-OUT-001 | AMZN API/Amazon_Ads_API | Amazon_Ads_API is PRIVATE, not public — README:16 / START-HERE:26 are wrong, and this closes the UNVERIFIED visibility BLOCKER in your SPEC-doc-archive-truth | `DONE` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` (in AMZN API/Amazon_Ads_API) | `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` | 2026-08-21 | 2026-08-21 |
| XR-OUT-417 | AMZN API/amzn-api-integration | Push Amazon_SP_API doc surface to origin | `AWAITING AN ANSWER` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` (in AMZN API/amzn-api-integration) | — | 2026-08-22 | — · 🔁 balance 2026-08-22: was `SENT`, restamped `AWAITING AN ANSWER` — the recipient holds this open and has not answered; your side must not read as closed. |

## Incoming requests from other repos — XREPO INBOX

Another repo has filed work here. These are **buildable rows, not questions** — each is already authorized (RULE-L24). Execute it, then close the loop with `xrepo-relay.py answer --id <ID>`, which writes the answer back into the originating repo's ledger. An open row here means this repo owes another repo an execution.

<!-- MANAGED BY ~/.claude/tools/xrepo-relay.py — do not hand-edit rows in this table.
     Column order is fixed because the tool reads it back; a hand-edit that shifts a column
     silently changes what `inbox`/`answer`/`--check` believe. Add context in the linked
     markdown file instead, which is unbounded and is what the executor actually reads. -->

| ID | From | Ask | Status | Instruction | Answer | Raised | Answered |
|----|------|-----|--------|-------------|--------|--------|----------|
| XR-IN-1000014 | estatehub | 3 conformance finding(s) in your tree — INV-LEDGER-005; INV-PAGE-001; INV-SPEC-001 | `DONE` | `XREPO/requests/REQUEST-estatehub-XR-IN-1000014-3-conformance-finding-s-in-your-tree-inv-ledger.md` | `XREPO/answers/ANSWER-amzn-api-amazon-sp-api-XR-IN-1000014-3-conformance-finding-s-in-your-tree-inv-ledger.md` (in estatehub) | 2026-08-22 | 2026-08-22 |

## Build order — IN PROGRESS

**Approved:** 2026-08-21T00:00:00Z
**Note:** Opened by `xrepo-queue.py` because this repo carried authorized incoming cross-repo work and no order to run it from. An `XR-IN` row is already-authorized work — another repo is blocked until it is done — so it is queued, not asked about (RULE-L24). Build each, then `xrepo-relay.py answer --id <XR-IN-nnn>` files the ANSWER back onto their ledger.

| Seq | Item | Status | Note |
|---|---|---|---|
| 1 | `XR-IN-1000014` | DONE | all 3 findings cleared (`0cab878`), answer delivered to estatehub as `XR-OUT-416` (`7ddbf32`) |
