# OI-9019: fix 1 INV-GOV/INV-ORDER conformance finding(s) (INV-ORDER-001)

- **Request id:** `XR-IN-1000833`
- **From repo:** `estatehub`
- **To repo:** `AMZN API/Amazon_SP_API`
- **Filed:** 2026-09-06T00:07:46Z
- **Instruction key:** `799c4f6e6d7f`
- **Originating rows:** —

> Filed by `xrepo-relay.py` under RULE-L24: cross-repo work is filed as an instruction, never handed back as a question.
> **When you have executed this, run:** `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000833 --body-file <what-you-did.md>`
> That writes the answer into `estatehub` and lands a row on ITS ledger. The loop is not closed until the answer exists on the other side.

---

# INV-GOV / INV-ORDER conformance findings for `AMZN API/Amazon_SP_API`

**Source:** estatehub OI-9019 — estate-wide `estate-conformance.py --check --only INV-GOV,INV-ORDER` sweep, 2026-09-05, unscoped across all registered repos.

## Why this lands on your repo, not estatehub's
`estate-conformance.py` scores every repo's OWN `PROJECT-LEDGER.md` build-order table against the estate's governance invariants (unique headings, no dangling row ids, no duplicate seq numbers, no idle runner). estatehub cannot edit another repo's ledger from outside — per the founder's standing cross-repo rule (2026-08-10), this is filed as work for your own repo to execute, not a question back to him.

## Findings (1)
### 1. `INV-ORDER-001`
**Dangling build-order id(s)** — these id(s) appear as rows in your live build order table but resolve to NO row in your ledger, so any runner that walks the order emits a degenerate plan for them every cycle. For each id below: find out whether (a) the ledger row was deleted/renamed and the order table still points at the old id — fix by updating the order table to the row's current id, or removing the id if the work no longer exists; or (b) the ledger row is genuinely missing and needs to be restored. This is a judgement only your own repo's history can make; estatehub cannot resolve it from outside.

Affected id(s): `XR-ANS-001, XR-ANS-417`

## Done when
`estate-conformance.py --check --only INV-GOV,INV-ORDER --repo <your-repo-root>` reads 0 open findings for this repo (run from your repo's own canonical checkout, not a worktree — a worktree checkout returns a disjoint finding set for the same repo).

## What to send back
Write your `ANSWER-*.md` back through `xrepo-relay.py answer --id <this-XR-id> --body-file <file>` naming which findings you fixed and how (commit hash / file / before-after). If any finding is already stale (row deleted, heading already unique, etc.) by the time you read this, say so — that closes the loop too.
