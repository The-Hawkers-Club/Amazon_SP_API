# OI-9019 build-order hygiene: INV-ORDER-001 (1 finding(s))

- **Request id:** `XR-IN-1000810`
- **From repo:** `estatehub`
- **To repo:** `AMZN API/Amazon_SP_API`
- **Filed:** 2026-09-05T20:31:39Z
- **Instruction key:** `b51050df3be0`
- **Originating rows:** —

> Filed by `xrepo-relay.py` under RULE-L24: cross-repo work is filed as an instruction, never handed back as a question.
> **When you have executed this, run:** `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000810 --body-file <what-you-did.md>`
> That writes the answer into `estatehub` and lands a row on ITS ledger. The loop is not closed until the answer exists on the other side.

---

# Governance/build-order hygiene findings for `AMZN API/Amazon_SP_API` — filed by estatehub's OI-9019 fresh full sweep (2026-09-05)

estatehub runs a periodic INV-GOV/INV-ORDER sweep across every repo it can read on this
machine (source: `ledger/findings-OI-9019-2026-09-05.json`, produced by OI-9019). Each
finding below is a build-order-file hygiene defect in YOUR repo, not estatehub's — estatehub
has no lever to fix another repo's build order, so this is filed as an instruction per
RULE-L24 rather than acted on directly. None of these are auto-repairable: each one is a
judgement call about which row/section is authoritative, which only your own project owner
or that repo's own build-order maintainer can make correctly.

## 1 finding(s)

### INV-ORDER-001
- **what:** 2 order item(s) resolve to no rows -- the runner cannot build them and will emit a degenerate plan every cycle
- **what to do about it:** XR-ANS-001, XR-ANS-417
- **checkout at scan time:** branch `main`, base `origin/main`, behind 0, ahead 0

## What closes this

Fix the build-order file(s) named above (usually `PROJECT-LEDGER.md` or an order-table
source under `PLAN/`) so the duplicate headings / cross-listed ids / repeated seq numbers
are resolved, then answer this request via `xrepo-relay.py answer --id <this id> --body-file
<what-you-did.md>` naming the commit that fixed it. If a finding is already stale (the file
has since changed shape), say so and cite the current state — that is a valid DONE/MOOT
answer too, not a reason to leave the row open.
