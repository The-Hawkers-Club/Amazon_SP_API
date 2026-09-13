# Project Ledger — AMZN API/Amazon_SP_API

> Every project running in this repo, every open item under it, and every cross-referral ask it is
> waiting on. **Canonical open-items store.**

**Protocol:** OIL v5.5.0
**Page:** https://oil-web-production.up.railway.app/r/Amazon_SP_API
**Installed:** 2026-08-21 (oil-install.py)
**Last reconciled:** never — the first /wrap performs the first reconcile
**Next IDs:** PRJ-001 · OI-0100 · XA-001
**Next XR-OUT ID:** 0419

## Portfolio

| ID | Project | Status | WS | 👤 | 🤖 | 🔗 | ⚪ | Open total | Oldest open | Last touched |
|----|---------|--------|----|----|----|----|----|-----------|-------------|--------------|
| PRJ-000 | Unfiled | STANDING | W0 | 0 | 3 | 0 | 1 | 4 | 2026-08-21 | 2026-09-07 |
| PRJ-001 | SPEC-spapi-archive-readable-and-guarded — the 422-PDF archiv | ACTIVE |  | 0 | 10 | 0 | 0 | 10 | 2026-09-05 | 2026-09-05 |
| PRJ-002 | SPEC-spapi-xr-ans-order-ids-resolve — the two queued cross-r | ACTIVE |  | 0 | 10 | 0 | 0 | 10 | 2026-09-06 | 2026-09-06 |
| PRJ-003 | SPEC-build-order-phantom-xr-ans-items — the two ids at the h | ACTIVE |  | 0 | 6 | 0 | 0 | 6 | 2026-09-12 | 2026-09-12 |
| PRJ-004 | SPEC-xrepo-queue-mints-unreachable-order-ids — a queued answ | ACTIVE |  | 0 | 10 | 0 | 0 | 10 | 2026-09-12 | 2026-09-12 |

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
| OI-0012 | W0 | 🤖 **Read the answer to `XR-OUT-418`** from .claude — `XREPO/answers/ANSWER-claude-XR-IN-1000843-xrepo-queue-py-mints-xr-ans-nnn-order-ids-that-n.md` — and act on it. Raised by `xrepo-queue.py` because the answer arrived with no build-order item naming a real row (XR-IN-1000843). | 🤖 | `OPEN` | 2026-09-05 | 2026-09-05 |
| OI-0015 | W0 | 🤖 **Read the answer to `XR-OUT-001`** from AMZN API/Amazon_Ads_API — `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` — and act on it. Raised by `xrepo-queue.py` because the answer arrived with no build-order item naming a real row (XR-IN-1000843). | 🤖 | `OPEN` | 2026-09-06 | 2026-09-06 |
| OI-0018 | W0 | 🤖 **Read the answer to `XR-OUT-417`** from AMZN API/amzn-api-integration — `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` — and act on it. Raised by `xrepo-queue.py` because the answer arrived with no build-order item naming a real row (XR-IN-1000843). | 🤖 | `OPEN` | 2026-09-06 | 2026-09-06 |
| OI-0051 | W0 | ⚪ **6 open build task(s) are written down in `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` and tracked by no row.** Verdict `ITEMS-ONLY` (0/6 ticked — a ticked box is a claim, not evidence). Backfilled by `INV-SPEC-001` so the work is VISIBLE; it is not scheduled and not adopted. Next action: `python3 ~/.claude/tools/spec-inventory.py --repo "AMZN API/Amazon_SP_API"` to read the open tasks, then file it into a project or adopt the spec on the open-ledger page. | ⚪ | `OPEN` | 2026-09-07 | 2026-09-07 |

## Requests this repo has sent — XREPO OUTBOX

Work this repo has filed into ANOTHER repo's ledger. `SENT` means the instruction and their row exist; it does not mean they have executed it. It closes when their answer lands back here as a row.

<!-- MANAGED BY ~/.claude/tools/xrepo-relay.py — do not hand-edit rows in this table.
     Column order is fixed because the tool reads it back; a hand-edit that shifts a column
     silently changes what `inbox`/`answer`/`--check` believe. Add context in the linked
     markdown file instead, which is unbounded and is what the executor actually reads. -->

| ID | To | Ask | Status | Instruction | Answer | Sent | Answered |
|----|----|-----|--------|-------------|--------|------|----------|
| XR-OUT-001 | AMZN API/Amazon_Ads_API | Amazon_Ads_API is PRIVATE, not public — README:16 / START-HERE:26 are wrong, and this closes the UNVERIFIED visibility BLOCKER in your SPEC-doc-archive-truth | `DONE` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` (in AMZN API/Amazon_Ads_API) | `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` | 2026-08-21 | 2026-08-21 |
| XR-OUT-417 | AMZN API/amzn-api-integration | Push Amazon_SP_API doc surface to origin | `DONE` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` (in AMZN API/amzn-api-integration) | `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` | 2026-08-22 | 2026-08-22 |
| XR-OUT-418 | .claude | xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos | `DONE` | `XREPO/requests/REQUEST-amzn-api-amazon-sp-api-XR-IN-1000843-xrepo-queue-py-mints-xr-ans-nnn-order-ids-that-n.md` (in .claude) | `XREPO/answers/ANSWER-claude-XR-IN-1000843-xrepo-queue-py-mints-xr-ans-nnn-order-ids-that-n.md` | 2026-09-06 | 2026-09-06 |

## Incoming requests from other repos — XREPO INBOX

Another repo has filed work here. These are **buildable rows, not questions** — each is already authorized (RULE-L24). Execute it, then close the loop with `xrepo-relay.py answer --id <ID>`, which writes the answer back into the originating repo's ledger. An open row here means this repo owes another repo an execution.

<!-- MANAGED BY ~/.claude/tools/xrepo-relay.py — do not hand-edit rows in this table.
     Column order is fixed because the tool reads it back; a hand-edit that shifts a column
     silently changes what `inbox`/`answer`/`--check` believe. Add context in the linked
     markdown file instead, which is unbounded and is what the executor actually reads. -->

| ID | From | Ask | Status | Instruction | Answer | Raised | Answered |
|----|------|-----|--------|-------------|--------|--------|----------|
| XR-IN-1000014 | estatehub | 3 conformance finding(s) in your tree — INV-LEDGER-005; INV-PAGE-001; INV-SPEC-001 | `DONE` | `XREPO/requests/REQUEST-estatehub-XR-IN-1000014-3-conformance-finding-s-in-your-tree-inv-ledger.md` | `XREPO/answers/ANSWER-amzn-api-amazon-sp-api-XR-IN-1000014-3-conformance-finding-s-in-your-tree-inv-ledger.md` (in estatehub) | 2026-08-22 | 2026-08-22 |
| XR-IN-1000810 | estatehub | OI-9019 build-order hygiene: INV-ORDER-001 (1 finding(s)) | `OPEN` | `XREPO/requests/REQUEST-estatehub-XR-IN-1000810-oi-9019-build-order-hygiene-inv-order-001-1-find.md` | — | 2026-09-05 | — |
| XR-IN-1000833 | estatehub | OI-9019: fix 1 INV-GOV/INV-ORDER conformance finding(s) (INV-ORDER-001) | `OPEN` | `XREPO/requests/REQUEST-estatehub-XR-IN-1000833-oi-9019-fix-1-inv-gov-inv-order-conformance-find.md` | — | 2026-09-06 | — |

## Build order — IN PROGRESS

**Approved:** 2026-08-21T00:00:00Z
**Note:** Opened by `xrepo-queue.py` because this repo carried authorized incoming cross-repo work and no order to run it from. An `XR-IN` row is already-authorized work — another repo is blocked until it is done — so it is queued, not asked about (RULE-L24). Build each, then `xrepo-relay.py answer --id <XR-IN-nnn>` files the ANSWER back onto their ledger.

| Seq | Item | Status | Note |
|---|---|---|---|
| 1 | `OI-0015` | QUEUED | queued by `xrepo-queue.py` 2026-09-02 — answer to `XR-OUT-001` arrived from AMZN API/Amazon_Ads_API; read `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` and act on it |
| 2 | `OI-0018` | QUEUED | queued by `xrepo-queue.py` 2026-09-02 — answer to `XR-OUT-417` arrived from AMZN API/amzn-api-integration; read `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` and act on it |
| 3 | `PRJ-001` | QUEUED | adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05 — he ticked Adopt on the page, which is the approval for this item; queued by `adopt-specs.py` directly into the live order (PRJ-040 T-03) |
| 4 | `OI-0002` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 5 | `OI-0003` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 6 | `OI-0004` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 7 | `OI-0005` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 8 | `OI-0006` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 9 | `OI-0007` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 10 | `OI-0008` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 11 | `OI-0009` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 12 | `OI-0010` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 13 | `OI-0011` | QUEUED | queued by `order-triage.py` 2026-09-05 — 🤖, buildable, was in no build order |
| 14 | `XR-IN-1000810` | QUEUED | queued by `xrepo-queue.py` 2026-09-05 — incoming from estatehub; the instruction file is the spec |
| 15 | `XR-IN-1000833` | QUEUED | queued by `xrepo-queue.py` 2026-09-05 — incoming from estatehub; the instruction file is the spec |
| 16 | `OI-0012` | QUEUED | queued by `xrepo-queue.py` 2026-09-05 — answer to `XR-OUT-418` arrived from .claude; read `XREPO/answers/ANSWER-claude-XR-IN-1000843-xrepo-queue-py-mints-xr-ans-nnn-order-ids-that-n.md` and act on it |
| 17 | `PRJ-002` | QUEUED | adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06 — he ticked Adopt on the page, which is the approval for this item; queued by `adopt-specs.py` directly into the live order (PRJ-040 T-03) |
| 18 | `OI-0021` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 19 | `OI-0024` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 20 | `OI-0027` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 21 | `OI-0030` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 22 | `OI-0033` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 23 | `OI-0036` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 24 | `OI-0039` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 25 | `OI-0042` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 26 | `OI-0045` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 27 | `OI-0048` | QUEUED | queued by `order-triage.py` 2026-09-06 — 🤖, buildable, was in no build order |
| 28 | `PRJ-003` | QUEUED | adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12 — he ticked Adopt on the page, which is the approval for this item; queued by `adopt-specs.py` directly into the live order (PRJ-040 T-03) |
| 29 | `PRJ-004` | QUEUED | adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12 — he ticked Adopt on the page, which is the approval for this item; queued by `adopt-specs.py` directly into the live order (PRJ-040 T-03) |
## Build order — COMPLETED (archive)

Items that finished more than 24h ago, moved out of the live order by `order-archive.py` so it shows only what is still to do. Nothing is deleted.

| Seq | Item | Status | Note |
|---|---|---|---|
| 1 | `XR-IN-1000014` | DONE | all 3 findings cleared (`0cab878`), answer delivered to estatehub as `XR-OUT-416` (`7ddbf32`) |
## Overnight runs

### Run of 2026-08-21 23:01 — ORDER-COMPLETE

- **Cycles:** 2 · **verdict:** `ORDER-COMPLETE`
- **Order now:** `XR-IN-1000014`=DONE
- **Still buildable:** none — order exhausted
- **Awaited job(s):** none

| # | moved | commits | note |
|---|-------|---------|------|
| 1 | HEAD 1758ba31ec1b->6ef1e268da89, XR-IN-1000014 QUEUED->DONE | 3 |  |
| 2 | HEAD 6ef1e268da89->9a87b082621c | 2 |  |

> Written by `overnight-run.py`. Progress is measured against OBSERVABLES between cycles — the git HEAD, the order's item statuses, the ledger — never against a cycle's own account of itself, because activity is not progress.

# PRJ-001 — SPEC-spapi-archive-readable-and-guarded — the 422-PDF archive becomes machine-readable, coverage-mapped and citation-guarded, and the repo stops describing itself falsely
**Goal:** This repo is the offline documentation base a **live** SP-API integration cites by filename, and today
neither half of that sentence is visible from inside it. The outcome: the 422 PDFs become searchable
text on this machine rather than 170 MB of opaque binaries no tool here can open; the archive's
coverage of the API versions production actually calls is a file you read instead of a grep that
silently returns zero; the 41 exact filename citations a sibling repo hangs its adopted decisions on
are guarded by a loop that converges when they drift; and a teammate opening the repo learns the real
role posture (which surfaces return 200, which return 403 and why) instead of a fifteen-line README
that says the archive is "internal" while GitHub serves it to the world.

The integration is **not** built here and this spec does not move it. `The-Hawkers-Club/amzn-api-integration`
holds it, `src/spapi/` and `src/spine/` are its loci, and this repo's job is to be the reference that
repo already treats as authoritative.
**Definition of done:** `AMZN API/.claude/spapi-index/` holds one extracted-text sidecar and one manifest row for every one of
the 422 PDFs; `docs/05-archive-index.md` lists every PDF on disk with its capture date; a coverage
report names, for each of the 19 SP-API family/version prefixes production calls, whether this archive
documents it; the citation guard reports every `*.pdf` filename cited by `../amzn-api-integration`
as resolving, or converges it; and `README.md` plus a new `START-HERE.md` and `docs/01–04` describe
what is actually true — including this repo's real GitHub visibility.
**Status:** ACTIVE
**Source:** adopted from `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` on 2026-09-05 by `adopt-specs.py` (RULE-L23) — he ticked adopt on the page; the spec graded 6/6 both when it was offered and again here.
| ID | Ws | Item — Residual Scope Only | Type | Status | Blocked By | Next Action | Where | Verified By | Raised | Last Checked |
|---|---|---|---|---|---|---|---|---|---|---|
| OI-0002 | — | Install `pypdf` (`pip3 install --user pypdf`, no brew/sudo) and prove it decodes this archive's Skia subset fonts — today **no tool on this machine can read one of the 422 PDFs** (pdftotext/mutool/qpdf absent, four Python PDF libraries absent, Read's `pdftoppm` absent, brew absent, stdlib zlib returns glyph codes); ToUnicode CMaps present in 25/25 sampled files make this the one cheap unlock. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0003 | — | Build `AMZN API/.claude/checks/spapi_doc_guard.py index` → 422 text sidecars + `manifest.json` (sha256, bytes, pages, PDF `/CreationDate`, chars) under `AMZN API/.claude/spapi-index/`, deliberately outside the world-readable repo and outside `amzn-api-integration` per `DECISIONS.md:1809`. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0004 | — | Create `docs/05-archive-index.md` — every one of the 422 PDFs by name and surface with its 2026-07-04 capture date; record that renaming is refused because `../amzn-api-integration` cites 41 of these filenames exactly, one of them as the evidence line under an adopted decision (`DECISIONS.md:1862`). (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0005 | — | Produce the coverage report: ~19 SP-API family/version prefixes production calls × 52 models in `../selling-partner-api-models` × what this archive documents — searched over extracted text, not filenames. Settles whether Orders **2026-01-01** (called in `src/`, present in the models tree, absent from every filename here) is documented at all. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0006 | — | Build the citation-integrity converge loop + `mutants_spapi_doc_guard.py` + hourly `com.thc.amzn-api-doc-citations` LaunchAgent, in the container's existing `.claude/checks/` pattern: distinct remedies, escalate on unknown signature, goal predicate reads the archive and never the log. Baseline to hold: **70 cited `.pdf` tokens, 56 exact + 12 suffix + 2 glob, 0 dangling.** (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0007 | — | Write `docs/03-status.md` — the probed role posture (I&OT held, Amazon Fulfillment not, Brand Analytics not and PARKED by OQ5, RDT/PII not), 12/12 endpoints 2xx, `APP_STATE=draft` in production, and the measured rate-limit spread — each line cited to the file that observed it. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0008 | — | Write `START-HERE.md`, `docs/01-getting-started.md`, `docs/02-playbook.md` and `docs/04-incident-response-plan.md` on the sibling archive's shape; `04` reuses the Incident Lead answer parked on `Amazon_Ads_API/PLAN/specs/SPEC-doc-archive-truth.md` rather than re-asking. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0009 | — | Rewrite `README.md:5,15` — repoint the asserted coverage bullet at the enumerated index and delete the "internal reference" sentence that GitHub contradicts. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0010 | — | Commit locally, staging paths by name; **do not push** (`org-api-mirror`, `push=no`), and file the publish request through `xrepo-relay.py`. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |
| OI-0011 | — | 🔗 FILED CROSS-REPO (not an item here): `Amazon_Ads_API/README.md:16` and `START-HERE.md:26` both tell the team *"This repo is **public**"* and base a credential-handling instruction on it — it is **private** (unauthenticated `api.github.com` → 404, vs 200 and `"private": false` for `Amazon_SP_API`). This also closes the open **BLOCKER** in that repo's own `PLAN/specs/SPEC-doc-archive-truth.md`, which recorded the visibility as UNVERIFIED because `gh` is not installed — `curl` against the public API needs no `gh` and no auth. (adopted from `SPEC-spapi-archive-readable-and-guarded` on 2026-09-05, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest \\ && python3 "$G" verify \\ && test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \\ && grep -q 'amzn-api-integration' docs/03-status.md \\ && ! grep -q 'internal reference by The H | `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` | — | 2026-09-05 | 2026-09-05 |

**DoD check:**
```sh
set -u
cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1
G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py"
python3 "$G" --selftest \
&& python3 "$G" verify \
&& test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \
&& grep -q 'amzn-api-integration' docs/03-status.md \
&& ! grep -q 'internal reference by The Hawker' README.md \
&& python3 -c "import os,sys; idx=open('docs/05-archive-index.md').read(); sys.exit(1 if [f for f in os.listdir('.') if f.endswith('.pdf') and f not in idx] else 0)"
```
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-13T17:56:46Z · `sh set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest`

OBSERVED 2026-08-21: this exact block was written to `/tmp/spapi-dod.sh` and run —
`bash /tmp/spapi-dod.sh > /tmp/spapi-dod.log 2>&1; echo "EXIT=$?" >> /tmp/spapi-dod.log` → **`EXIT=2`**
(the exit code is written to the log by the shell, not read from a wrapper's status). Every arm was
also failed individually today: `test -f START-HERE.md` → NO, `test -f docs/03-status.md` → NO,
`test -f docs/05-archive-index.md` → NO, `grep -q 'internal reference by The Hawker' README.md` →
still present. Positive control that the arms are satisfiable rather than impossible: the same two
`test -f` arms run against the sibling `../Amazon_Ads_API` → both PRESENT.

`--selftest` is not redundant with `verify`. `verify` proves the guard agrees with **this** archive;
`--selftest` proves the guard can still *see* a fault, by planting one on a temp copy (a renamed PDF,
a sidecar whose sha256 no longer matches its source, a citation pointed at a file that does not exist)
and requiring a non-zero exit on each — the defect being that a checker which repairs or silently
skips what it is looking for reports green forever (`AMZN API/.claude/checks/page_link_guard.py:30-40`
records that exact failure happening on this estate).

# PRJ-002 — SPEC-spapi-xr-ans-order-ids-resolve — the two queued cross-repo ANSWERS get read and closed, so the build order stops naming ids that resolve to nothing
**Goal:** Two ids sit at the head of this repo's approved build order — `XR-ANS-001` and `XR-ANS-417` — that
resolve to no row anywhere in `PROJECT-LEDGER.md`. Three independent surfaces already say so:
`estate-conformance.py` INV-ORDER-001 (OBSERVED this session: `2 order item(s) resolve to no rows`),
`ledger-doctor.py` C3 (OBSERVED: `the live order names 2 item(s) that are not rows in this ledger:
XR-ANS-001, XR-ANS-417`), and estatehub's OI-9019 sweep, which escalated the same fact into two
cross-repo instructions (`XR-IN-1000810`, `XR-IN-1000833`).

The outcome: both ids stop being phantoms — not by deleting them, but because the real work each one
points at gets done and their order rows go terminal with evidence in the row. `XR-ANS-001` points at
`XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md`;
`XR-ANS-417` points at
`XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md`.
Both were read in full during this planning pass and both turn out to be closable here without
building anything new, because the acting repo already did its half and — for 417 — the world moved
underneath the refutation. Once both order rows are terminal, `overnight-run.py`'s `schedule()` stops
emitting a degenerate "no live rows yet, RAISE the rows this project needs" plan for them every cycle,
the head of the approved order finally advances to `PRJ-001`, and the two estatehub instructions get
their answers.

This is a ledger-and-transport correction. It changes no runtime code in this repo and does not touch
the 422-PDF archive or `PRJ-001`'s own work, beyond retiring one dependency `PRJ-001` was carrying
(the publish request at step 9 of `SPEC-spapi-archive-readable-and-guarded`, which `XR-ANS-417`
refuted and which reality has since made moot).
**Definition of done:** `estate-conformance.py --check --only INV-GOV,INV-ORDER --repo .` reports `0 open` for this repo,
both `XR-ANS-001` and `XR-ANS-417` read a terminal status in the live order with evidence in their
Note cells, `xrepo-queue.py`'s `unqueued_answers()` returns `[]` for this repo (so neither id is
re-minted on the next `com.thc.xrepo-queue` tick), and both `XR-IN-1000810` and `XR-IN-1000833` read
`DONE` on this repo's cross-repo table with answers delivered into `estatehub`.
**Status:** ACTIVE
**Source:** adopted from `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` on 2026-09-06 by `adopt-specs.py` (RULE-L23) — he ticked adopt on the page; the spec graded 6/6 both when it was offered and again here.
| ID | Ws | Item — Residual Scope Only | Type | Status | Blocked By | Next Action | Where | Verified By | Raised | Last Checked |
|---|---|---|---|---|---|---|---|---|---|---|
| OI-0021 | — | Read `XREPO/answers/ANSWER-…-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` and confirm against this tree that nothing is owed here (no stale `Amazon_Ads_API` visibility claim in `README.md`/`START-HERE.md`/`docs/`, no local `SPEC-doc-archive-truth.md`). (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0024 | — | Take `XR-ANS-001`'s live-order row (`PROJECT-LEDGER.md:71`) to `DONE` with that evidence in its Note cell, leaving the Item cell string untouched. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0027 | — | Read `XREPO/answers/ANSWER-…-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` and establish the current publish state of this tree (`HEAD` vs `origin/main`). (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0030 | — | Take `XR-ANS-417`'s live-order row (`PROJECT-LEDGER.md:72`) to `DONE`, recording the refutation as accepted and its founder-only remedy as moot because the doc surface reached `origin/main` at `2d54cad` via PR #1 — which also retires the publish step of `SPEC-spapi-archive-readable-and-guarded` for `PRJ-001`. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0033 | — | Commit `PROJECT-LEDGER.md` and this spec by name (no `git add -A`, no `git push`). (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0036 | — | Re-run `ledger-doctor.py --repo .` against the real checkout and confirm its C3 line no longer names the two ids. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0039 | — | Write the `ANSWER-*.md` and deliver it to estatehub for `XR-IN-1000833` via `xrepo-relay.py answer`. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0042 | — | Deliver the same answer for the duplicate instruction `XR-IN-1000810`, stating explicitly that the two are one finding filed twice so estatehub can collapse them at source. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0045 | — | Ensure the RECURRENCE is filed to `.claude` exactly once — `answer_order_id()` mints an id no row defines, and its docstring reasons only about `ledger-doctor.py` C3 being report-only, not knowing that `estate-conformance.py:1622` INV-ORDER-001 flags the same shape and that OI-9019 escalates it into cross-repo instructions, so every future answered `XR-OUT-nnn` estate-wide manufactures a fresh finding; the sibling pass already wrote the body as `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md`, so check before sending and never `--force-duplicate`. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |
| OI-0048 | — | Run the DoD check and record its real output in the closing row. (adopted from `SPEC-spapi-xr-ans-order-ids-resolve` on 2026-09-06, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt \|\| exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 \| grep -qE 'XR-IN-1000810[[:space:]]+\\[DONE\\]' \|\| exit 1 python3 ~/.claude/tools/l | `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` | — | 2026-09-06 | 2026-09-06 |

**DoD check:**
```sh
set -u
cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1
python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1
grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt || exit 1
python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000810[[:space:]]+\[DONE\]' || exit 1
python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000833[[:space:]]+\[DONE\]' || exit 1
python3 - <<'PY' || exit 1
import importlib.util, os, sys
T=os.path.expanduser("~/.claude/tools"); sys.path.insert(0,T)
sp=importlib.util.spec_from_file_location("_xq", os.path.join(T,"xrepo-queue.py"))
xq=importlib.util.module_from_spec(sp); sp.loader.exec_module(xq)
sys.exit(0 if not xq.unqueued_answers(".") else 1)
PY
```
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-13T17:56:46Z · `sh set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt || exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000810[[:space:]]+\[DONE\]' || exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000833[[:space:]]+\[DONE\]' || exit 1 python3 - <<'PY' || exit 1 import importlib.util, os, sys T=os.path.expanduser("~/.claude/tools"); sys.path.insert(0,T) sp=importlib.util.spec_from_file_location("_xq", os.path.join(T,"xrepo-queue.py")) xq=importlib.util.module_from_spec(sp); sp.loader.exec_module(xq) sys.exit(0 if not xq.unqueued_answers(".") else 1) PY`

BOTH DIRECTIONS PROVEN THIS SESSION, not asserted:

- **Negative control** — run verbatim against the live tree as it stands today: `EXIT=1`. It fails at
  the conformance arm, which currently prints `-> 0 repaired, 1 open`.
- **Positive control** — run against a temp fixture holding this repo's real `PROJECT-LEDGER.md` and
  real `XREPO/` with only the four status cells flipped to the target end state: `EXIT=0`, and the
  conformance line read
  `estate-conformance: 1 repos x 11 invariants -> 0 repaired, 0 open`.

The fourth arm (`unqueued_answers() == []`) is the one that matters most and it is not decorative: it
is the arm that fails if the tempting-but-wrong fix is taken. See Conflicts.

# PRJ-003 — SPEC-build-order-phantom-xr-ans-items — the two ids at the head of this repo's build order stop being unbuildable ghosts, because the answers they point at are read and closed with evidence
**Goal:** The two items at seq 1 and seq 2 of this repo's live build order — `XR-ANS-001` and `XR-ANS-417` —
name nothing. No row anywhere in `PROJECT-LEDGER.md` carries either id, so every cycle that walks the
order resolves them to zero rows and emits *"no live rows yet. RAISE the rows this project needs"*
for them, forever. They are the **head** of the order, which is the worst place for this to sit: the
runner's first two decisions each cycle are decisions about phantoms, and `PRJ-001` — the project he
actually queued — is stuck behind them.

Both ids are follow-up items `xrepo-queue.py` wrote on 2026-09-02 so that two cross-repo **answers**
would be read by someone. Neither ever was. Reading them is the work, and both close here:

- **`XR-ANS-001`** → `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-…md`. Amazon_Ads_API
  re-ran the probe, corrected its own `README.md:16` and `START-HERE.md:26`, and closed the visibility
  BLOCKER in its `SPEC-doc-archive-truth`. Its closing line is *"Nothing further is needed from
  `Amazon_SP_API`."* Nothing to build; the row closes DONE with that as its evidence.
- **`XR-ANS-417`** → `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-…md`. This one
  came back **REFUTED as routed**: `amzn-api-integration` proved it holds no push capability this repo
  lacks, both trees being `push=no`. Its residual was *"nine commits, all local, `origin/main` has not
  moved since 2026-07-05"*. **That premise is now overtaken.** The doc surface reached `origin/main`
  by a route neither the request nor the refutation considered — a merged pull request — so the ask is
  satisfied and the row closes MOOT with the current state cited.

Once this is done the order describes work that exists, its head advances to `PRJ-001`, and the two
estatehub instructions that reported the defect get their answers.
**Definition of done:** `python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo .`, run from
this repo's canonical checkout, reports **0 open** across all 11 selected invariants (it reports
1 open today); `overnight-run.schedule()` returns no entry with `no_rows=True` for this ledger and its
plan head is `PRJ-001`; and both `XR-IN-1000810` and `XR-IN-1000833` read terminal on this repo's
incoming cross-repo table with answers delivered into `estatehub`.
**Status:** ACTIVE
**Source:** adopted from `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` on 2026-09-12 by `adopt-specs.py` (RULE-L23) — he ticked adopt on the page; the spec graded 6/6 both when it was offered and again here.
| ID | Ws | Item — Residual Scope Only | Type | Status | Blocked By | Next Action | Where | Verified By | Raised | Last Checked |
|---|---|---|---|---|---|---|---|---|---|---|
| OI-0054 | — | Close build-order seq 1 (`XR-ANS-001`) as DONE at `PROJECT-LEDGER.md:71`, citing the Amazon_Ads_API answer's own closing line *"Nothing further is needed from `Amazon_SP_API`"* as evidence, and leaving the Note cell's `` `XR-OUT-001` `` untouched so the re-queue dedupe keeps holding. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0057 | — | Close build-order seq 2 (`XR-ANS-417`) as MOOT at `PROJECT-LEDGER.md:72`, citing merged PR `2d54cad` and the post-fetch ahead=1 / behind=0 measurement that overtakes the refutation's nine-unpushed-commits premise, and leaving the Note cell's `` `XR-OUT-417` `` untouched for the same reason. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0060 | — | Commit `PROJECT-LEDGER.md` by name and run the DoD check, capturing the exit code into the log rather than reading a wrapper's status. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0063 | — | Record a dated premise update under Question 1 of `SPEC-spapi-archive-readable-and-guarded.md` noting that `docs/05-archive-index.md` is now published, without re-asking the question or altering its options. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0066 | — | Answer `XR-IN-1000810` through `xrepo-relay.py`, naming the commit and the conformance output. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0069 | — | Answer `XR-IN-1000833` as the duplicate of `XR-IN-1000810`, closed by the same commit, so both inbox rows go terminal. (adopted from `SPEC-build-order-phantom-xr-ans-items` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" \|\| exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \\ \| grep -q '0 repaired, 0 open' \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importl | `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` | — | 2026-09-12 | 2026-09-12 |

**DoD check:**
```sh
set -u
cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1
python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-13T17:56:46Z · ````sh set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" ||`
  | grep -q '0 repaired, 0 open' \
&& python3 - <<'PY'
import importlib.util, os, sys
T = os.path.expanduser("~/.claude/tools")
s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py"))
ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov)
s2 = importlib.util.spec_from_file_location("_xq", os.path.join(T, "xrepo-queue.py"))
xq = importlib.util.module_from_spec(s2); sys.modules["_xq"] = xq; s2.loader.exec_module(xq)
text = open("PROJECT-LEDGER.md", encoding="utf-8").read()
plan = ov.schedule(text)
dead = [p["project"] for p in plan
        if p.get("no_rows") and not p.get("all_blocked") and not p.get("exhausted")]
assert not dead, f"still unreachable: {dead}"
assert plan and plan[0]["project"] == "PRJ-001", f"order head is {plan and plan[0]['project']}"
for oid in ("XR-OUT-001", "XR-OUT-417"):
    assert xq._outbox_id_referenced_in_any_order(text, oid), \
        f"{oid} no longer named in an order section -> xrepo-queue will re-queue it"
assert not xq.unqueued_answers("."), "an answered outbox row is unbooked -> it will be re-minted"
print("OK")
PY
```

Run it as `bash /tmp/spec-phantom-dod.sh > /tmp/spec-phantom-dod.log 2>&1; echo "EXIT=$?" >> /tmp/spec-phantom-dod.log`
and read **the log**, not the wrapper's status.

The arms are not redundant. The conformance run proves the *invariant* is quiet. The Python arm proves
the three facts the invariant is blind to: that `schedule()` itself sees no unreachable item (the
**runner's** predicate, not its grader); that the order head is now `PRJ-001` rather than merely
"not a phantom"; and that the literal `` `XR-OUT-001` `` / `` `XR-OUT-417` `` strings survive in an
order-section body. That last assertion is the regression guard for this spec's own failure mode:
`xrepo-queue.py:461 _outbox_id_referenced_in_any_order` is the only thing stopping
`unqueued_answers()` re-appending these two items under fresh ids on the next scheduled tick, and it
matches on that Note-cell prose, not on the Item cell — this is `XR-IN-1000719`'s recorded defect,
where a retype in AMZN-Consulting un-armed the dedupe and the same work was re-queued at seq 132.

**OBSERVED 2026-09-05, this session — the fix was simulated before being specified.** Both status
cells were changed on a temp copy of this ledger and every arm re-run against it:
`estate-conformance --check --only INV-GOV,INV-ORDER` → `1 repos x 11 invariants -> 0 repaired, 0 open`;
`schedule()` dead items → `[]`; plan head → `PRJ-001`; both `_outbox_id_referenced_in_any_order`
probes → `True`. Baseline control against the unmodified live file in the same session → `1 open`
(INV-ORDER-001, `XR-ANS-001, XR-ANS-417`), so the instrument discriminates and the green is a reading.
`MOOT` was confirmed to be in `overnight-run.TERMINAL` rather than assumed to be.

# PRJ-004 — SPEC-xrepo-queue-mints-unreachable-order-ids — a queued answer becomes a real ledger row instead of a synthetic id that names nothing, and the 1,371 already written estate-wide are repaired
**Goal:** When an answer comes back to an ask this estate sent, `xrepo-queue.py` puts a follow-up item on the
receiving repo's build order so somebody actually **reads** the answer — that mechanism is right and
closed a real 2,528-row hole. But the id it writes into the Item cell, `XR-ANS-nnn`, is **synthetic:
it defines no row anywhere**. So the item is on the order and resolves to nothing, and every cycle
that walks that order emits *"no live rows yet. RAISE the rows this project needs"* for it — which
is not a wasted cycle, it is a cycle **instructed to invent rows for work that already has an answer
file on disk**.

`answer_order_id`'s own docstring anticipates a cost and accepts it, and the accepted cost is
understated. It reasons about `ledger-doctor.py`'s C3 check only, concludes *"this costs a cosmetic
diagnostic line, never a repair — the acceptable side of the tradeoff"*, and does not consider
`estate-conformance.py`'s `INV-ORDER-001`, which reads the same defect through
`overnight-run.schedule()` — the **runner's own predicate**, not a diagnostic. The tradeoff is not
cosmetic. It is the exact degenerate-plan failure `INV-ORDER-001` was written for in the first place.

Once this is done, a queued answer names a real, open ledger row that says what to do with the
answer; the estate's 1,371 existing synthetic items are repaired the same way; and `INV-ORDER-001`
goes back to meaning what it was built to mean, instead of being a 1,371-row background hum that no
repo can act on and that every repo now gets filed at it as hygiene work.
**Definition of done:** `python3 ~/.claude/tools/estate-conformance.py --check --only INV-ORDER` across the registered estate
reports **zero** `INV-ORDER-001` findings whose detail names an `XR-ANS-*` id (it names 1,371 today,
across 30 repos), and a fresh `xrepo-queue.py` run against a fixture with an answered outbox row
appends an item whose Item cell names a row that exists in the same ledger.
**Status:** ACTIVE
**Source:** adopted from `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` on 2026-09-12 by `adopt-specs.py` (RULE-L23) — he ticked adopt on the page; the spec graded 6/6 both when it was offered and again here.
| ID | Ws | Item — Residual Scope Only | Type | Status | Blocked By | Next Action | Where | Verified By | Raised | Last Checked |
|---|---|---|---|---|---|---|---|---|---|---|
| OI-0072 | — | Measure the baseline from `.claude`'s own checkout — `XR-ANS` unreachable items estate-wide, plus the non-`XR-ANS` control — and record both numbers before changing anything. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0075 | — | Change `xrepo-queue.py:714 queue()` so the answers population raises a real `OI-nnnn` row through `_ledger.with_allocated_oi` in the same locked transaction, and puts that id in the Item cell. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0078 | — | Keep `answer_order_id` as the degradation path for a ledger whose Unfiled table cannot be located, so an unusual ledger falls back to today's behaviour instead of failing the queue. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0081 | — | Add a selftest that reddens if `_answered_outbox_note` stops writing the literal `XR-OUT-nnn` id, since `_outbox_id_referenced_in_any_order` is the only remaining dedupe link. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0084 | — | Update the existing `XR-ANS-100` / `XR-ANS-200` selftest fixtures at `xrepo-queue.py:1226-1318` to assert the new Item-cell shape, in the same commit as the behaviour change. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0087 | — | Build the idempotent repair actuator that retypes existing `XR-ANS-*` items and raises their companion rows, one locked transaction per repo, escalating on any ledger it cannot parse rather than retrying it. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0090 | — | Run the repair on `estatehub` first and alone (1,096 items), commit, and read the diff before proceeding. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0093 | — | Run the repair across the remaining 29 affected repos, committing each by name. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0096 | — | Run the three-arm DoD check, capturing the exit code into the log rather than reading a wrapper's status. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |
| OI-0099 | — | Answer the originating cross-repo filing with the commits and the before/after counts. (adopted from `SPEC-xrepo-queue-mints-unreachable-order-ids` on 2026-09-12, RULE-L23) | 🤖 | OPEN | — | build it, then the project DoD check must pass: set -u python3 ~/.claude/tools/xrepo-queue.py --selftest \\ && python3 ~/.claude/tools/estate-conformance.py --selftest \\ && python3 - <<'PY' import importlib.util, os, sys T = os.path.expanduser("~/.claude/tools") s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py")) ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov) reg = {} | `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` | — | 2026-09-12 | 2026-09-12 |

**DoD check:**
```sh
set -u
python3 ~/.claude/tools/xrepo-queue.py --selftest \
&& python3 ~/.claude/tools/estate-conformance.py --selftest \
&& python3 - <<'PY'
import importlib.util, os, sys
T = os.path.expanduser("~/.claude/tools")
s = importlib.util.spec_from_file_location("_ov", os.path.join(T, "overnight-run.py"))
ov = importlib.util.module_from_spec(s); sys.modules["_ov"] = ov; s.loader.exec_module(ov)
reg = {}
for line in open(os.path.expanduser("~/.claude/state/repo-registry.tsv"), encoding="utf-8"):
    if line.startswith("#") or not line.strip():
        continue
    p = line.rstrip("\n").split("\t")
    if len(p) >= 2:
        reg[p[0]] = os.path.expanduser(p[1])
tot = 0
for name, path in sorted(reg.items()):
    led = os.path.join(path, "PROJECT-LEDGER.md")
    if not os.path.exists(led):
        continue
    text = open(led, encoding="utf-8", errors="replace").read()
    if "## Build order" not in text:
        continue
    try:
        plan = ov.schedule(text)
    except Exception:
        continue
    dead = [p["project"] for p in plan
            if p.get("no_rows") and not p.get("all_blocked") and not p.get("exhausted")]
    tot += sum(1 for d in dead if str(d).startswith("XR-ANS-"))
print("XR-ANS unreachable estate-wide:", tot)
assert tot == 0, f"still {tot}"
PY
```
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-13T17:56:46Z · `sh set -u python3 ~/.claude/tools/xrepo-queue.py --selftest`

Run it as `bash /tmp/xrans-dod.sh > /tmp/xrans-dod.log 2>&1; echo "EXIT=$?" >> /tmp/xrans-dod.log`
and read the log, not the notification's status.

The three arms are not redundant. `xrepo-queue.py --selftest` proves the **generator** stops minting
the shape (it already carries fixtures at `~/.claude/tools/xrepo-queue.py:1226-1318` that assert on
`XR-ANS-100`/`XR-ANS-200` literals, so they are the arm that must be updated alongside the fix, not
after it). `estate-conformance.py --selftest` proves `INV-ORDER-001` still **discriminates** — its
existing self-test at `~/.claude/tools/estate-conformance.py:7575-7596` pins both directions,
including a `CONTROL: INV-ORDER-001 went blind to a genuinely phantom order item`, so a fix that
silences the invariant instead of the defect reddens there. The third arm measures the **world**, not
the job table: it re-walks every registered ledger and counts what `schedule()` actually resolves.

**Baseline, OBSERVED 2026-09-05 by running exactly that third arm:** `XR-ANS` unreachable estate-wide
= **1,371**, in 30 of the 60 registered repos that carry a build order. Positive control that the
sweep discriminates rather than matching everything: the same walk counts **8** unreachable items
that are *not* `XR-ANS-*` (`OI-0688`, `OI-0136`, `OI-0196`, `PRJ-1016`, `PRJ-002` in `clientmindIQ`,
`cmq-adcomm`, `CIO-PO Analytics`), and returns **0** for `.claude`'s own ledger — so a zero is a
reading, not a broken instrument.
