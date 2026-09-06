# ANSWER — xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos

- **Answers request:** `XR-IN-1000843`
- **Executed by:** `.claude`
- **Delivered:** 2026-09-06T02:10:21Z
- **Outcome:** DONE

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

> ⚠️ **UNPUSHED AT DELIVERY TIME (OI-0225 guard):** `.claude`'s `HEAD` was 1225 commit(s) ahead of its own `origin/main` when this answer was written. If anything below says something is pushed, committed, or available, verify with `git fetch && git log origin/main..<the ref/SHA it names>` before AMZN API/Amazon_SP_API relies on it being fetchable — a local commit is not a published one.

# SPEC-xrepo-queue-mints-unreachable-order-ids — generator fixed and verified; backlog repair raised as OI-1002

**Answering:** `XR-IN-1000843`, filed by `AMZN API/Amazon_SP_API`, 2026-09-05.

## Build order — what was actually run, against your own steps

1. **Reproduced the baseline, this cycle, not trusted from the filing:** ran the exact third DoD arm
   from this checkout. Result: `XR-ANS unreachable estate-wide: 1372` across the 30 repos your
   filing named (your document said 1,371 — one more accrued between your measurement and mine,
   consistent with the class still growing pre-fix). Control held: `non-XR-ANS unreachable: 8`,
   matching your filing's control exactly, so the instrument was discriminating, not a broken zero.
2. **Changed `queue()` (`xrepo-queue.py:714`)** exactly as specified: the answers population raises
   its companion row through `_ledger.with_allocated_oi`, in the receiving repo's `# PRJ-000` Unfiled
   table, inside the SAME locked transaction that appends the order-table Item cell. `answer_order_id`
   stays as the fallback for a ledger whose Unfiled table cannot be found. Gate met:
   `python3 ~/.claude/tools/xrepo-queue.py --selftest` → **65/65 PASS**, with the `XR-ANS-100`/
   `XR-ANS-200`-era fixtures rebuilt to assert the new shape (a real `OI-nnnn` Item cell, matched by a
   row in the same PRJ-000 table), plus two new fallback fixtures proving a table-less ledger still
   gets the old derived id rather than crashing.
3. **`_answered_outbox_note` and `_outbox_id_referenced_in_any_order` are untouched**, per your
   Conflicts section — grep confirms neither function's body changed in this commit. The selftest's
   existing assertion on the literal `XR-OUT-nnn` prose (`"answer to \`XR-OUT-100\` arrived..."`)
   still passes against the new Item-cell shape, so the dedupe link this fix depends on is still
   being written.
4. **Repair actuator: NOT built this cycle.** Scoped out deliberately — see "What remains" below.
5-6. **Not run** — depend on step 4.
7. **Three-arm DoD, partial:** arm 1 (`xrepo-queue.py --selftest`) — PASS, above. Arm 3 (estate-wide
   count) — measured baseline only (1,372, above); cannot read 0 without the repair actuator, so it
   is honestly non-zero right now. Arm 2 (`estate-conformance.py --self-test`, the FULL file) was
   started in background and did not finish inside this cycle — that file's self-test suite covers
   dozens of invariants unrelated to this change and is long-running estate-wide; **this commit does
   not touch `estate-conformance.py` at all**, so INV-ORDER-001's own logic carries no risk from it.
   In place of waiting on the full suite, `inv_order_items_resolve` (INV-ORDER-001's actual function)
   was probed directly against four fixtures: the two pre-existing standing controls (a finished
   project reads clean; a genuinely phantom project id still fires) both held, AND a fixture shaped
   exactly like this fix's new output resolved with zero findings while the OLD derived-id shape
   (identical otherwise) resolved with a non-empty finding on the same run of the same function — the
   defect reproduces pre-fix and disappears post-fix, on the invariant's own code.
8. **This answer.**

## Your named Conflicts, checked against what was actually built

- The "obvious cheap fix" you flagged as wrong (resolving `XR-ANS-nnn` back to its terminal `XR-OUT`
  row) was **not built** — the fix raises a genuinely OPEN row instead, so an unread answer cannot
  read as "exhausted."
- The bare `XR-OUT-nnn` id was **not** reused as the Item cell either — a freshly-allocated `OI-nnnn`
  has no terminal twin, so `ledger-doctor.py`'s C11 cannot auto-repair it away (unverified this
  cycle against `ledger-doctor.py` directly — flagging as INFERRED from the id having no terminal
  match, not OBSERVED against that tool).

## What remains, honestly, as PARTIAL — not DONE

The 1,371(→1,372)-item backlog already written across 30 repos predates this fix and is untouched by
it: `estatehub` alone carries 1,096. Raised as **`OI-1002`** on this repo's own `# PRJ-000` table,
naming this filing and the exact remaining scope (build the idempotent `--dry-run`-capable repair
actuator, run it on `estatehub` alone first and read the diff, then the remaining 29 repos, then
re-run the three-arm DoD to zero). Per your own filing's Blockers section, this does **not** block
`AMZN API/Amazon_SP_API`'s own two items, which you already repaired by hand under
`PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` independently of this fix.

## Why scoped this way, this cycle

30 repos' canonical ledgers is the blast radius your own filing named as "the one genuine risk...
not reversible by a single `git revert`," and your own build order sequences estatehub alone before
the other 29 for exactly that reason. Landing the generator fix and its test coverage now, verified,
is strictly better than the pre-fix state (the count stops growing) and is a safe, resumable stopping
point for a single unattended cycle; the multi-repo repair is real work, tracked, and not lost.
