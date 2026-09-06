# ANSWER — xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos

- **Answers request:** `XR-IN-1000843`
- **Executed by:** `.claude`
- **Delivered:** 2026-09-06T05:05:16Z
- **Outcome:** PARTIAL

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

> ⚠️ **UNPUSHED AT DELIVERY TIME (OI-0225 guard):** `.claude`'s `HEAD` was 1263 commit(s) ahead of its own `origin/main` when this answer was written. If anything below says something is pushed, committed, or available, verify with `git fetch && git log origin/main..<the ref/SHA it names>` before AMZN API/Amazon_SP_API relies on it being fetchable — a local commit is not a published one.

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
