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
| OI-0001 | W0 | ⚪ **10 open build task(s) are written down in `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` and tracked by no row.** Verdict `ITEMS-ONLY` (0/10 ticked — a ticked box is a claim, not evidence). Backfilled so the work is VISIBLE; it is not scheduled and not adopted. Next action: `python3 ~/.claude/tools/spec-inventory.py --repo "AMZN API/Amazon_SP_API"` to read the open tasks, then file it into a project or adopt the spec on the open-ledger page. | ⚪ | `OPEN` | 2026-08-21 | 2026-08-21 |

## Requests this repo has sent — XREPO OUTBOX

Work this repo has filed into ANOTHER repo's ledger. `SENT` means the instruction and their row exist; it does not mean they have executed it. It closes when their answer lands back here as a row.

<!-- MANAGED BY ~/.claude/tools/xrepo-relay.py — do not hand-edit rows in this table.
     Column order is fixed because the tool reads it back; a hand-edit that shifts a column
     silently changes what `inbox`/`answer`/`--check` believe. Add context in the linked
     markdown file instead, which is unbounded and is what the executor actually reads. -->

| ID | To | Ask | Status | Instruction | Answer | Sent | Answered |
|----|----|-----|--------|-------------|--------|------|----------|
| XR-OUT-001 | AMZN API/Amazon_Ads_API | Amazon_Ads_API is PRIVATE, not public — README:16 / START-HERE:26 are wrong, and this closes the UNVERIFIED visibility BLOCKER in your SPEC-doc-archive-truth | `DONE` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` (in AMZN API/Amazon_Ads_API) | `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` | 2026-08-21 | 2026-08-21 |

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
| 1 | `XR-IN-1000014` | BUILDING | queued by `xrepo-queue.py` 2026-08-21 — incoming from estatehub; the instruction file is the spec |
