# Project Ledger — AMZN API/Amazon_SP_API

> Every project running in this repo, every open item under it, and every cross-referral ask it is
> waiting on. **Canonical open-items store.**

**Protocol:** OIL v5.5.0
**Page:** https://oil-web-production.up.railway.app/r/Amazon_SP_API
**Installed:** 2026-08-21 (oil-install.py)
**Last reconciled:** never — the first /wrap performs the first reconcile
**Next IDs:** PRJ-001 · OI-0049 · XA-001
**Next XR-OUT ID:** 0419

## Portfolio

| ID | Project | Status | WS | 👤 | 🤖 | 🔗 | ⚪ | Open total | Oldest open | Last touched |
|----|---------|--------|----|----|----|----|----|-----------|-------------|--------------|
| PRJ-000 | Unfiled | STANDING | W0 | 0 | 3 | 0 | 0 | 3 | 2026-08-21 | 2026-09-06 |
| PRJ-001 | SPEC-spapi-archive-readable-and-guarded — the 422-PDF archiv | ACTIVE |  | 0 | 10 | 0 | 0 | 10 | 2026-09-05 | 2026-09-05 |
| PRJ-002 | SPEC-spapi-xr-ans-order-ids-resolve — the two queued cross-r | ACTIVE |  | 0 | 10 | 0 | 0 | 10 | 2026-09-06 | 2026-09-06 |

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
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-06T22:28:40Z · `sh set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1 G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py" python3 "$G" --selftest`

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
**DoD status:** DoD UNVERIFIABLE · not checked · EXIT=n/a · 2026-09-06T22:28:40Z · `sh set -u cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1 python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . > /tmp/spapi-inv.txt 2>&1 grep -q -- '-> 0 repaired, 0 open' /tmp/spapi-inv.txt || exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000810[[:space:]]+\[DONE\]' || exit 1 python3 ~/.claude/tools/ledger-read.py --repo . --xrin 2>&1 | grep -qE 'XR-IN-1000833[[:space:]]+\[DONE\]' || exit 1 python3 - <<'PY' || exit 1 import importlib.util, os, sys T=os.path.expanduser("~/.claude/tools"); sys.path.insert(0,T) sp=importlib.util.spec_from_file_location("_xq", os.path.join(T,"xrepo-queue.py")) xq=importlib.util.module_from_spec(sp); sp.loader.exec_module(xq) sys.exit(0 if not xq.unqueued_answers(".") else 1) PY`

BOTH DIRECTIONS PROVEN THIS SESSION, not asserted:

- **Negative control** — run verbatim against the live tree as it stands today: `EXIT=1`. It fails at
  the conformance arm, which currently prints `-> 0 repaired, 1 open`.
- **Positive control** — run against a temp fixture holding this repo's real `PROJECT-LEDGER.md` and
  real `XREPO/` with only the four status cells flipped to the target end state: `EXIT=0`, and the
  conformance line read
  `estate-conformance: 1 repos x 11 invariants -> 0 repaired, 0 open`.

The fourth arm (`unqueued_answers() == []`) is the one that matters most and it is not decorative: it
is the arm that fails if the tempting-but-wrong fix is taken. See Conflicts.
