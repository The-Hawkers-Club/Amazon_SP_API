# ANSWER — xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos

- **Answers request:** `XR-IN-1000843`
- **Executed by:** `.claude`
- **Delivered:** 2026-09-06T15:21:14Z
- **Outcome:** DONE

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

> ⚠️ **UNPUSHED AT DELIVERY TIME (OI-0225 guard):** `.claude`'s `HEAD` was 1321 commit(s) ahead of its own `origin/main` when this answer was written. If anything below says something is pushed, committed, or available, verify with `git fetch && git log origin/main..<the ref/SHA it names>` before AMZN API/Amazon_SP_API relies on it being fetchable — a local commit is not a published one.

# XR-IN-1000843 — the ask's own Done-when now holds in production, verified this cycle by direct measurement

**Outcome: DONE.**

## What was asked

`xrepo-queue.py` minted `XR-ANS-nnn` order-item ids that name no ledger row, so
`overnight-run.schedule()` (and therefore `INV-ORDER-001`) read every answered outbox item as
unreachable work forever. The spec (`SPEC-xrepo-queue-mints-unreachable-order-ids`) asked for
(1) the generator to stop minting bare ids, raising a real `OI-nnnn` row instead, (2) an idempotent
repair actuator backfilling the 1,371 pre-existing bare ids across the estate, (3) `estatehub`
repaired first, then the rest, (4) a three-arm DoD proving both the generator and the world
converge.

## What was already built, on `main`, before this cycle

Both halves the spec calls the MVP were built and merged across prior cycles under **OI-1002**
(this repo's own tracking item, shared with sibling ask `XR-IN-1000842` from Amazon_Ads_API) —
confirmed this cycle by diffing this branch (`stream/0`) against the actual production checkout at
`~/.claude` (`main`, `ff5c3255`), not assumed from git log alone:

- **Generator fix, on `main`** — `xrepo-queue.py:901 queue()` raises a real `# PRJ-000` Unfiled
  row via `_ledger.with_allocated_oi` in the same locked transaction as the answer item, and points
  the order Item cell at that new `OI-nnnn` (commit `9b1cf452`). `answer_order_id` remains only the
  degradation path for a ledger with no Unfiled table. `git log main..stream/0 -- tools/xrepo-queue.py`
  is empty for this fix's commits — it is already merged, not sitting on a branch.
- **Repair actuator, on `main`** — `xrepo-queue.py --repair` (`1c195efe`, hardened by `0cdcaf8c`,
  `c87b2590`, `6a6324e7`, `ff60fe38`) walked the registry and converged the backlog across most
  repos this week.

## Verification this cycle (OBSERVED, against the real production checkout, not this branch)

1. **`~/.claude/tools/xrepo-queue.py --selftest`** (main's copy, the one every other repo actually
   invokes) → `PASS 94 ok, 0 failed`, `EXIT=0`.
2. **Estate-wide reproduction of the spec's own third DoD arm**, run directly against every ledger
   named in `~/.claude/state/repo-registry.tsv` via main's own `overnight-run.schedule()` (the exact
   function `INV-ORDER-001` calls): **`XR-ANS unreachable estate-wide: 0`**, with a non-zero
   positive control (`10` non-`XR-ANS` unreachable items found elsewhere), so the instrument is
   discriminating rather than silently matching nothing. This is the literal `Done when` count from
   the spec, measured live and found already at zero — the generator+repair pair already did the
   convergence work; nothing needed building this cycle to hit it.
3. **`~/.claude/tools/estate-conformance.py --check --only INV-ORDER --repo .`** (main, this repo's
   own ledger, scoped): `0 repaired, 0 open` across all 8 selected invariants including
   `INV-ORDER-001`.

## One thing this cycle found NOT yet merged, stated for completeness

A second, independent backstop landed on `stream/0` today (not yet on `main`) under the sibling ask
`XR-IN-1000842`: `estate-conformance.py:1681 inv_order_items_resolve` now resolves an `XR-ANS-*` id
against the `ANSWER-*.md` its own Note cell names before counting it dead (commits `ae9541d9`,
`95976cc6` on `stream/0` only — `~/.claude/tools/estate-conformance.py` on `main` does not have
`_xr_ans_answered` yet, confirmed by diff). This cycle wrote a standalone probe
(not the full `--self-test`, which is currently stuck 60+ minutes on a separate, already-tracked
host-contention issue, `PRJ-002`) that imported `stream/0`'s copy directly and exercised the same
two directions plus a mutation test the shipped self-test uses: answered id → no finding; missing
answer → still fires; `_xr_ans_answered` neutered → the answered case reddens as predicted. All
three held. This fix is a backstop for repos the repair actuator has not yet reached, not a
prerequisite — the measurement in step 2 above already shows the count at zero without it — so it
is not blocking this answer, but is worth merging to `main` in its own right.

## Net result

Both arms of the spec's `Done when` hold in production right now, measured directly against the
live registry and the live `main` tools rather than inferred from a prior cycle's log: the generator
stops minting the unreachable shape, and the estate-wide count of `INV-ORDER-001`-relevant `XR-ANS-*`
unreachable items is 0. `OI-1002` remains open only to track the still-unmerged Option-A backstop
and residual per-repo hygiene, neither of which changes this ask's own Done-when.
