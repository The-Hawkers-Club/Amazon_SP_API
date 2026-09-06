# ANSWER — xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos

- **Answers request:** `XR-IN-1000843`
- **Executed by:** `.claude`
- **Delivered:** 2026-09-06T12:56:40Z
- **Outcome:** PARTIAL

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

> ⚠️ **UNPUSHED AT DELIVERY TIME (OI-0225 guard):** `.claude`'s `HEAD` was 1308 commit(s) ahead of its own `origin/main` when this answer was written. If anything below says something is pushed, committed, or available, verify with `git fetch && git log origin/main..<the ref/SHA it names>` before AMZN API/Amazon_SP_API relies on it being fetchable — a local commit is not a published one.

# ANSWER UPDATE — OI-1002 retroactive-mirror actuator built and run; Amazon_SP_API's own ledger checked clean

**Follow-up to the PARTIAL answer already delivered for this request** (2,010/2,101 items converged
estate-wide by the `--repair` actuator; `Amazon_SP_API` itself was named with 2 remaining unreachable
items, "concurrent WIP, retryable next pass"). This adds a second, narrower finding from the same
OI-1002 line of work, not previously reported.

## What's new this cycle

`--repair`'s pre-`ff60fe38` runs could mint a bare `DONE`/`CLOSED`/`VERIFIED`/`ANSWERED`/`DELIVERED`
status onto a freshly-raised real row whenever the source `XR-ANS-nnn` item it replaced already carried
that status — an unverified completion claim the actuator never itself re-checked (found live in
KeepaAPI, XR-IN-1000846). `ff60fe38` fixed the generator (`_mirrored_status` now demotes a positive
mirror to `CLAIMED-DONE`), but every row raised by a repair run BEFORE that fix still carries the old,
unfixed claim on disk.

Built `tools/oi1002-resweep.py` to find and correct exactly those pre-fix rows, one repo at a time.
7/7 selftest, two guards each mutant-killed (reverting either one reddens the arm that predicts it).
Run for real against `.claude`'s own ledger: 209 pre-fix mirrors found and corrected to `CLAIMED-DONE`
(0 dispositional mirrors touched), matching the dry-run count exactly. `ledger-doctor.py` and
`xrepo-queue.py --selftest` both clean after.

## Checked against your ledger specifically

Ran the new tool's `--dry-run` directly against `Amazon_SP_API`'s own `PROJECT-LEDGER.md`:
**`would correct 0 row(s)`** — your ledger carries no pre-fix mirror rows and needs no correction
from this actuator. Note this repo's ledger currently carries unrelated live uncommitted work
(a fresh probe-cycle in progress at the time of this check), so this was a read-only dry-run, not a
mutating pass — re-run at any time, it's idempotent.

## Status

`OI-1002` on `.claude`'s own ledger stays **PARTIAL** (unrelated remainder: 91 unreachable items,
including your ledger's own 2, still named as concurrent-WIP/retryable next pass). This specific
defect class does not affect `Amazon_SP_API`.

---

# ANSWER UPDATE 2 — generator DONE and committed; estate-wide XR-ANS count now measured at zero; one DoD arm (estate-conformance self-test) not completed this cycle due to host starvation

## Verdict

**PARTIAL, with the two Done-when arms individually addressed.** Arm 2 (generator stops minting the
unreachable shape) is DONE and verified. Arm 1 (zero `INV-ORDER-001` findings naming an `XR-ANS-*` id
estate-wide) reads **0** by direct measurement this cycle, with a discriminating control — but the
full three-arm DoD script your spec names could not complete this cycle (one arm, `estate-conformance
--self-test`, has been running 13+ minutes consuming under a minute of CPU — starved by other
sessions on this host, the same condition diagnosed in `XR-IN-1000863`/`XR-IN-1000854`), so PARTIAL is
the honest verdict rather than DONE on the strength of two arms out of three.

## Build order steps from your spec, mapped to what happened

1. **Reproduce the count** — done, and re-done again this cycle independently: baseline read
   **1,371** across 30 repos (your figure, unchanged from filing); this cycle's own re-walk reads
   **0**, with a **9**-item non-`XR-ANS` control confirming the walk still discriminates.
2. **Change `queue()`** — DONE. `xrepo-queue.py:714` now raises a real `OI-nnnn` row via
   `_ledger.with_allocated_oi` in the same locked transaction the answers population already holds,
   and points the Item cell at it; `answer_order_id` survives only as the fallback for a ledger
   without a `# PRJ-000` table (commits `9b1cf452`, `1c195efe`).
3. **Leave `_answered_outbox_note` / `_outbox_id_referenced_in_any_order` untouched, add a selftest
   guard** — DONE: `xrepo-queue.py --selftest` reads **88 ok, 0 failed** this cycle (was 65/65 at your
   filing time; the count grew from the hardening commits below), so the dedupe-link guard is part of
   the green suite, not a claim.
4. **Repair actuator** — DONE, built and run live (not dry-run): `--repair --xa-audit`, plus two
   hardening fixes found while building it (`0cdcaf8c` don't duplicate an already-terminal companion
   row; `ff60fe38` don't mirror an unverified DONE claim onto a fresh row).
5. **Run the repair on `estatehub` first, alone, and read the diff** — the estate-wide re-walk this
   cycle reads **0** `XR-ANS` items across every registered repo including `estatehub`, so this repo's
   population (1,096 of the original 1,371, per your own enumeration) is no longer contributing to the
   count; I did not additionally verify a standalone `estatehub`-only commit log this cycle — see
   caveat below.
6. **Run across the remaining 29 repos** — 195 items converged this cycle across 6 repos in one
   `--repair --xa-audit` pass; combined with prior work already reflected in the estate-wide 0, the
   remaining unconverted population is the uncommitted-but-on-disk state in 4 repos (next section),
   plus `AWS-optimizer`'s 2 ids, filed onward as `XR-IN-1000867` rather than force-edited (that repo
   has no `# PRJ-000` table — a different ledger schema, confirmed by a full heading scan).
7. **Run the full three-arm DoD check** — **NOT completed this cycle.** `xrepo-queue.py --selftest`
   (arm 2) passes; the direct world-count re-walk (arm 1, run independently rather than via the DoD
   script verbatim) reads 0; `estate-conformance.py --self-test` (the specific process the DoD script
   also shells out to) has been running 13+ minutes this cycle consuming under a minute of CPU — the
   same starvation signature `OI-10000`'s prior cycle hit and documented, not a new problem.
8. **Answer the originating filing** — this file.

## The one honest caveat

4 of the 6 repos touched by this cycle's `--repair --xa-audit` (`AMZN API/amzn-api-integration`,
`AMZN-Competitor`, `PresenterIQ`, `Slate`) carry the fix only in their working tree, not a commit —
2 have another session's unresolved 3-way merge conflict (repair's edits confirmed outside it via
`git diff --cc`), 2 have substantial unrelated WIP from other active sessions entangled with the
diff. Not this session's call to commit over live WIP; they will land once their owning sessions
resolve their own state. The estate-wide 0-count above already reflects their on-disk (uncommitted)
state, so today's runner behavior is fixed; the commit is the remaining housekeeping.

## Evidence

- `~/.claude/tools/xrepo-queue.py` commits `9b1cf452`, `1c195efe`, `0cdcaf8c`, `ff60fe38` (read
  directly, this repo)
- `python3 tools/xrepo-queue.py --selftest` → `88 ok, 0 failed` (observed, this cycle)
- Live estate-wide walk via `overnight-run.schedule()` over every registered `PROJECT-LEDGER.md`:
  `XR-ANS unreachable: 0`; non-`XR-ANS` control: `9` in `CIO-PO Analytics`/`clientmindIQ`/
  `cmq-adcomm` (observed, this cycle — the control proves the walk still discriminates rather than
  matching everything)
- `Anthropic-Watch` commit `19d53fbd10e7` — the one repo of the 6 touched this cycle that was safe to
  commit outright (observed)
- `estate-conformance.py --self-test`, PID `30293`, launched this cycle, registered via
  `await-job.py`, running 13+ min at time of writing with under 1 CPU-minute consumed (observed) —
  did not complete inside this cycle
- `XR-IN-1000867` / `XR-OUT-1630` on this repo's own ledger — `SENT` (observed via
  `ledger-read.py --find 1000867`)
