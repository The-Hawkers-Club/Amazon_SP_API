# SPEC-spapi-xr-ans-order-ids-resolve — the two queued cross-repo ANSWERS get read and closed, so the build order stops naming ids that resolve to nothing

**Source:** PLAN/dumps/20260905192730-xrin-xr-in-1000833-oi-9019-fix-1-inv-gov-inv-order-conformance-find.md
**Status:** READY
**As of:** 2026-09-05

## Goal

Two ids sit at the head of this repo's approved build order — `XR-ANS-001` and `XR-ANS-417` — that
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

## Done when

`estate-conformance.py --check --only INV-GOV,INV-ORDER --repo .` reports `0 open` for this repo,
both `XR-ANS-001` and `XR-ANS-417` read a terminal status in the live order with evidence in their
Note cells, `xrepo-queue.py`'s `unqueued_answers()` returns `[]` for this repo (so neither id is
re-minted on the next `com.thc.xrepo-queue` tick), and both `XR-IN-1000810` and `XR-IN-1000833` read
`DONE` on this repo's cross-repo table with answers delivered into `estatehub`.

## DoD check

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

BOTH DIRECTIONS PROVEN THIS SESSION, not asserted:

- **Negative control** — run verbatim against the live tree as it stands today: `EXIT=1`. It fails at
  the conformance arm, which currently prints `-> 0 repaired, 1 open`.
- **Positive control** — run against a temp fixture holding this repo's real `PROJECT-LEDGER.md` and
  real `XREPO/` with only the four status cells flipped to the target end state: `EXIT=0`, and the
  conformance line read
  `estate-conformance: 1 repos x 11 invariants -> 0 repaired, 0 open`.

The fourth arm (`unqueued_answers() == []`) is the one that matters most and it is not decorative: it
is the arm that fails if the tempting-but-wrong fix is taken. See Conflicts.

## Fits

The whole change lands in one file plus two relay calls. No source code in this repo is touched.

- `PROJECT-LEDGER.md:71` — the live order's Seq 1 row for `XR-ANS-001`, whose Note cell already reads
  "answer to `XR-OUT-001` arrived from AMZN API/Amazon_Ads_API; read … and act on it". The **Status
  cell only** moves `QUEUED` -> `DONE`, and the Note cell gains the evidence. The Item cell string
  `` `XR-ANS-001` `` MUST NOT be retyped — see Conflicts.
- `PROJECT-LEDGER.md:72` — the live order's Seq 2 row, the same shape for `XR-ANS-417` /
  `XR-OUT-417` / `AMZN API/amzn-api-integration`. Same rule: Status cell and Note cell, never the
  Item cell.
- `PROJECT-LEDGER.md:64` — the `IN PROGRESS` order heading that `overnight-run.py`'s `_order_start()`
  anchors on. Unchanged; named because every edit above is scoped to that section and not to the
  `COMPLETED (archive)` heading at `PROJECT-LEDGER.md:86`.
- `PROJECT-LEDGER.md` cross-repo table (rows `XR-IN-1000810`, `XR-IN-1000833`) — both currently
  `` `OPEN` ``, both move to `` `DONE` ``. This edit is made BY `xrepo-relay.py answer`, not by hand.
- `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md`
  — read-only input for step 1. Exists (`ls` OBSERVED, 2982 bytes).
- `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md`
  — read-only input for step 3. Exists (`ls` OBSERVED, 11200 bytes).
- Two new files under `XREPO/` written by the relay, one per instruction, naming the commit.

Entry point production takes — this order table is READ, every cycle, by:

- `~/.claude/tools/overnight-run.py:2388` `schedule()` — via `order_items()` at
  `~/.claude/tools/overnight-run.py:1504`, which reads the status from the **Status cell by header**
  and the id from the **Item cell**. An item whose id maps to no row sets `no_rows`, and
  `plan_text()` (`~/.claude/tools/overnight-run.py:2764`) then emits the degenerate plan line. This is
  the consumer the finding is actually about.
- `~/.claude/tools/estate-conformance.py:1622` `inv_order_items_resolve()` — imports
  `overnight-run.py` and calls the same `schedule()`, so it is measuring exactly what the runner sees.
- `~/.claude/tools/ledger-doctor.py` C3 — a third reader of the same table, report-only
  (`grep -c "_fix_c3" ~/.claude/tools/ledger-doctor.py` -> `0`).

## Wiring

There is no new code to wire; the question this section exists to answer is whether the EDIT will be
observed by anything, and whether anything will UNDO it. Both were probed by executing the real
functions, not by reading them.

- **producer:** `~/.claude/tools/xrepo-queue.py:714` `queue()` (with the note builder at
  `~/.claude/tools/xrepo-queue.py:695` `_answered_outbox_note`) is what wrote rows 71–72 on
  2026-09-02. The Item-cell id is minted by `~/.claude/tools/xrepo-queue.py:274` `answer_order_id()`,
  which deliberately derives `XR-ANS-nnn` from `XR-OUT-nnn` so the two never collide.
  **-> consumer:** `~/.claude/tools/overnight-run.py:2388` `schedule()`, and through it
  `~/.claude/tools/estate-conformance.py:1622`. Confirmed live: running
  `inv_order_items_resolve("BASELINE", <this repo>)` returns exactly one finding with detail
  `XR-ANS-001, XR-ANS-417`, and running it against the same ledger with both status cells flipped to
  `DONE` returns `0 finding(s)`. Same function, same file, both directions.
- **the producer is on a timer and will re-run:** `~/Library/LaunchAgents/com.thc.xrepo-queue.plist`
  exists (OBSERVED), so `xrepo-queue.py` re-evaluates this repo unattended. The re-mint decision is
  made by `~/.claude/tools/xrepo-queue.py:207` `unqueued_answers()`, which was executed directly this
  session against three ledger states:

  | ledger state | `unqueued_answers()` returns |
  |---|---|
  | live tree, as it stands today | `[]` |
  | both order rows flipped to `DONE` | `[]` |
  | both order rows **deleted** | `[('XR-ANS-001', 'XR-OUT-001'), ('XR-ANS-417', 'XR-OUT-417')]` |

  So the fix in this spec is stable under the timer and the wrong one is not. That third row is the
  reason the DoD check carries a fourth arm.
- **answer-back path:** `~/.claude/tools/xrepo-relay.py:2484` `cmd_answer()` -> writes into
  `/Users/peterbeke/Developer/VS Code/estatehub` (directory OBSERVED to exist) and flips this repo's
  own `XR-IN` row to `DONE`. Confirmed as a working path on this exact repo by the precedent already
  in the tree: `XR-IN-1000014` reads `[DONE]` with
  `XREPO/answers/ANSWER-amzn-api-amazon-sp-api-XR-IN-1000014-…md (in estatehub)`.

## Conflicts

- **rules:** `command grep -c "XR-ANS" ~/.claude/commands/CLAUDE.md` -> `0`. No standing command rule
  mentions this id class, so nothing here contradicts one.
- **decisions:** `ls DECISIONS.md` -> `No such file or directory`. This repo has no decisions file
  (the one `XR-ANS-417`'s answer cites, with DEC-0146 / DEC-0242, lives in `amzn-api-integration`, not
  here). Nothing local to contradict.
- **live rows:** the ids this touches are `XR-ANS-001`, `XR-ANS-417` (live order Seq 1 and 2) and
  `XR-IN-1000810`, `XR-IN-1000833` (cross-repo table, both `[OPEN]` per
  `ledger-read.py --repo . --xrin`). Nothing else on the 15-item order is touched.
- **🔴 THE TWO INSTRUCTIONS ARE THE SAME FINDING.** `XR-IN-1000810` (filed 2026-09-05T20:31:39Z) and
  `XR-IN-1000833` (filed 2026-09-06T00:07:46Z) are both estatehub OI-9019, both INV-ORDER-001, and
  both name the identical affected ids `XR-ANS-001, XR-ANS-417` — read side by side from
  `XREPO/requests/`. They are a duplicate, not two units of work. One fix closes both, but **two
  separate `xrepo-relay.py answer` calls are still required**, because each has its own row here and
  its own row on estatehub's ledger.
- **🔴 A SIBLING PASS SPECC'D THE DUPLICATE INSTRUCTION WHILE THIS ONE RAN, AND ITS OUTPUT IS NOW ON
  DISK.** `ls PLAN/specs/` (OBSERVED after writing this spec) shows two files written 20:31–20:33
  from the `XR-IN-1000810` dump:
  - `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md` — **the same work as this spec.** Only one
    of the two should be adopted; the other should be marked superseded rather than built, because
    adopting both would raise two sets of OI rows for one set of status-cell edits. As of this
    writing that file's Status line reads `READY` but `spec-gate.py` returns 🔴 NOT READY on it
    (`8 of 8 step(s) carry no gate:`), whereas this spec returns ✅ READY TO ADOPT on all eleven
    dimensions — stated as an observation, not a claim on the outcome; which one he adopts is his.
    That file was NOT edited from here: it belongs to a concurrent pass and two writers on one file
    is the race this note exists to avoid.
  - `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` — the RECURRENCE, correctly scoped
    to the `.claude` repo (its header names `.claude` as owner repo and says the file is the body of
    an `xrepo-relay.py request`). That is the same cross-repo filing this spec's step 9 was going to
    make, so step 9 is now a CHECK-THEN-FILE rather than a file: `xrepo-relay.py request` refuses a
    duplicate an open recipient still holds, and forcing past that refusal with
    `--force-duplicate` is exactly what produced the two estatehub instructions this spec is closing.
- **🔴 THE OBVIOUS FIX IS THE WRONG ONE, AND IT IS WRONG TWICE OVER.** The instruction offers
  "removing the id if the work no longer exists" and "updating the order table to the row's current
  id". Both are traps, and the estate's own tooling records why:
  - *Deleting the rows* re-opens the finding on the next timer tick. Measured above: with the rows
    deleted, `unqueued_answers()` returns both ids and `queue()` re-appends them.
  - *Retyping the Item cell to the real id* is worse. `~/.claude/tools/xrepo-queue.py:274`
    `answer_order_id()`'s docstring records that `ledger-doctor.py`'s C11 check auto-repairs — with
    no env var required, unattended, every 1800s via `com.thc.ledger-doctor` — any order row whose id
    also names a terminal row elsewhere in the same ledger. `XR-OUT-001` and `XR-OUT-417` are
    answered, therefore terminal (`grep -c` -> 2 occurrences each in this ledger). Retyping hands C11
    exactly the shape it exists to delete, and the answer is silently dropped with nobody prompted to
    read it. Separately, `~/.claude/tools/xrepo-queue.py:461`
    `_outbox_id_referenced_in_any_order()`'s docstring records this retype being done live in
    `AMZN-Consulting` on 2026-09-03 (`48c93aa7`): Seq 49's Item cell was retyped `XR-ANS-043` ->
    `OI-0426` and the next run re-appended the same work at Seq 132.
  - The surviving option is the one this spec takes: leave both Item cells byte-identical, do the
    work, move the Status cells.
- **`ledger-doctor.py` C1, adjacent and deliberately out of scope:** running it on this repo also
  reports `the build reports 1 item(s) finished; the ledger's order says 0 of 15`. That is a separate
  contradiction between the overnight-run record under `## Overnight runs` and the live order, it is
  not INV-GOV/INV-ORDER, and neither instruction asks for it. Named here so a later reader knows it
  was seen and left alone, not missed.

## Blast radius

What can break is whatever READS these four status cells. The consumers were enumerated by running
them, not by reasoning about them.

- **`overnight-run.py` `schedule()` / `plan_text()`** — this is the intended effect, and it is a
  widening, not a narrowing: today `free_rows` is starved for these two items and the head of the
  order cannot advance; after the fix the head advances to `PRJ-001`, which is already `QUEUED` and
  already approved. Nothing that was buildable stops being buildable.
- **`estate-conformance.py` INV-ORDER-001** — goes from 1 open finding to 0. Executed both ways this
  session (`BASELINE: 1 finding(s) ['XR-ANS-001, XR-ANS-417']` / `OPT-C-done: 0 finding(s) []`).
  INV-ORDER-002/003 are explicitly a different question (`estate-conformance.py:1665` comment) and
  the 11-invariant run in the positive control came back clean across all of them, so this does not
  trade one finding for another.
- **`xrepo-queue.py` re-mint** — probed as unchanged (`[]` before, `[]` after); see the Wiring table.
- **`order-archive.py`** (`~/.claude/tools/order-archive.py` exists, and
  `~/Library/LaunchAgents/com.thc.build-order-archive.plist` runs it) will move both rows into the
  `COMPLETED (archive)` section once they are >24h terminal. That is safe and evidenced:
  `XR-IN-1000014` already sits in that archive `DONE` and has never been re-queued, which is the
  positive control that archived rows still count as "referenced in an order" for `xrepo-queue.py`.
- **`ledger-doctor.py`** — C3 stops naming these two ids (its own report is the observable). C11 is
  the one that could delete a row, and it cannot fire here:
  `grep -c "XR-ANS-001" PROJECT-LEDGER.md` -> `1`, i.e. the id occurs ONLY as the Item cell and names
  no row elsewhere, so C11's `item_status.get("XR-ANS-001")` finds nothing. This holds only while the
  Item cell is left alone, which is why Fits states that constraint twice. *This one arm is INFERRED
  from the code plus the occurrence count rather than executed, because `ledger-doctor.py` refuses a
  temp-dir fixture — it returned `no repo matched … NOTHING WAS CHECKED (2 = could not look, never a
  pass)`. Step 6 of the build order re-runs it against the real tree, where it does work, and that is
  where the arm becomes OBSERVED.*
- **Outside this repo:** `xrepo-relay.py answer` writes into `estatehub` — two new answer files and
  two ledger rows there. That is the intended, and the only, cross-repo write.
- **Not touched:** no `.py`, no `docs/`, no PDF, no `README.md`, no `START-HERE.md`. `PRJ-001`'s DoD
  check is unaffected except that its blocked publish request is retired as moot (step 4).

## Blockers

Swept before writing this, each with the command that looked and a control where an absence is
claimed. **No BLOCKER survived the sweep.**

- **A missing tool or credential?** No. `ls ~/.claude/tools/{estate-conformance,xrepo-relay,xrepo-queue,ledger-read,ledger-doctor,order-archive}.py`
  -> all six present; all were EXECUTED this session (conformance, ledger-read and ledger-doctor ran
  and produced output; xrepo-queue was imported and its functions called). No API key, token or
  network call is involved anywhere in this spec.
- **A counterparty who must ship first?** No. `ls -d "/Users/peterbeke/Developer/VS Code/estatehub"`
  -> exists. **Resolved:** estatehub is the recipient of the answers, not a dependency of the fix —
  steps 1–6 complete without it, and `XR-IN-1000014`'s delivered answer is the positive control that
  the relay reaches that tree from here.
- **A founder ruling this contradicts?** No. `grep -c "XR-ANS" ~/.claude/commands/CLAUDE.md` -> `0`;
  `ls DECISIONS.md` -> absent. Control: the same file does carry the Parallel-by-default and
  build-order rules under other search terms, so the file is readable and the `0` is a real absence
  rather than a bad path.
- **A capability that does not exist?** No. Every step is a ledger edit or a relay call, both of which
  this repo has performed before (`XR-IN-1000014`, closed with commit `0cab878` and answer `7ddbf32`
  per its archive row).
- **A gate that would refuse it — the push=no guard.** `git push` from this tree IS blocked:
  `~/.claude/hooks/push-policy-guard.py` classifies this repo `org-api-mirror`, `push=no`, and the
  guard carries no override token by design — that is precisely the finding `XR-ANS-417`'s answer
  file documents, measured, with a `Marketing System/leadgen` control returning `blocked=False`
  through the same code path. **Resolved, and it does not block this spec:** this spec requires a
  COMMIT, not a push, and the estate has since demonstrated another path anyway —
  `git rev-parse HEAD` and `git rev-parse origin/main` both return
  `2d54cad788bf6b2bce0a4919e334ee98428e0aa5` and `git rev-list --count origin/main..main` -> `0`,
  i.e. the work landed on origin via the merge of PR #1
  (`Merge pull request #1 from The-Hawkers-Club/fix/20260905-193901-fast-lane-bulk-land-amzn-api-amazon-sp-a`).
- **A stale premise inside the work itself?** Yes, one, and it is a finding rather than a blocker.
  `XR-ANS-417`'s refutation rests on *"Nine commits, all local, `origin/main` has not moved since
  2026-07-05T18:02:50Z"* (written 2026-08-22). That premise is now FALSE: `HEAD == origin/main`, as
  above. **Resolved:** the doc surface is published, so neither of the two founder paths that answer
  named — (a) he pushes it himself, (b) he flips `org-api-mirror` to `push=yes` via
  `intake-policy-set.py` — is needed for this work. Step 4 records that as the act-on-it, and it is
  why this spec parks no question for him.
- **Would fixing this need the archive / PDFs / `PRJ-001` first?** No. `PRJ-001` sits at Seq 3, behind
  both of these; the dependency runs the other way, and this spec is what unblocks the head of the
  order.

## Questions

**None are his.** Every ambiguity in the two instructions was settleable from the code and was
settled, which is the standard for not spending his attention:

- *Which of the instruction's two remedies applies — (a) the row was renamed, or (b) the row is
  genuinely missing?* Settled by `~/.claude/tools/xrepo-queue.py:274` `answer_order_id()`, whose
  docstring states the ids are DELIBERATELY synthetic and defined by no row anywhere. Neither (a) nor
  (b): the third answer is that the ids are correct as written and the work behind them is simply
  unfinished. Not his — it is a fact about a tool on this machine.
- *Should the rows be deleted instead?* Settled by executing `unqueued_answers()` against a
  rows-deleted fixture: they come straight back. Not a judgement call, a measurement.
- *Does the push in `XR-ANS-417` still need him?* Settled by `git rev-parse` — it already happened via
  PR #1. Asking him to push an already-pushed branch would be the exact waste the standing rule
  against re-asking exists to prevent.

The one thing in this material that IS genuinely his — whether `org-api-mirror` should move to
`push=yes`, a widening of a push rule he has already ruled on twice (DEC-0146, DEC-0242, both in
`amzn-api-integration`) — is deliberately NOT raised here, because nothing in this spec needs it and
the merge of PR #1 shows the estate already has a working publish path. Raising it would manufacture
a blocker out of a resolved one. If a later spec genuinely needs `git push` from this tree, that is
the spec that should ask him.

## MVP

The shortest route to a TRUE `Done when` is nearly the whole of it, with one arm split out. `Done
when` has four conjuncts (0 open findings · both order rows terminal with evidence ·
`unqueued_answers()` empty · both `XR-IN` rows `DONE` on both sides), and the only Item that no
conjunct requires is the cross-repo filing to `.claude`. Everything else is load-bearing:

- Read `XREPO/answers/ANSWER-…-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` and confirm against this tree that nothing is owed here — because: without it, taking `XR-ANS-001` to `DONE` is an unevidenced status flip, which is the RULE-L08 violation this whole finding class exists to catch.
- Take `XR-ANS-001`'s live-order row (`PROJECT-LEDGER.md:71`) to `DONE` with that evidence, Item cell untouched — because: `Done when`'s first conjunct is literally `0 open`, and the measurement showed the finding clears only when BOTH rows go terminal.
- Read `XREPO/answers/ANSWER-…-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` and establish `HEAD` vs `origin/main` — because: the answer's premise is stale, and closing 417 on a premise nobody re-checked would repeat the exact error the estate's own verify-at-the-boundary rule names.
- Take `XR-ANS-417`'s live-order row (`PROJECT-LEDGER.md:72`) to `DONE` with the moot-remedy note, Item cell untouched — because: with one of the two ids still `QUEUED`, INV-ORDER-001 still fires and `Done when` is FALSE.
- Commit `PROJECT-LEDGER.md` and this spec by name — because: an uncommitted ledger is at the mercy of the next unattended `--fix` pass, so the conjuncts would not still hold an hour later.
- Re-run `ledger-doctor.py --repo .` and confirm C3 no longer names the two ids — because: it is the only executable check of the one Blast-radius arm that is INFERRED rather than OBSERVED, and it runs unattended every 1800s with a delete-capable fixer.
- Write the `ANSWER-*.md` and deliver it for `XR-IN-1000833` — because: `Done when`'s fourth conjunct names this row explicitly, and the instruction's own closing line says the loop is not closed until the answer exists on the other side.
- Deliver the same answer for the duplicate `XR-IN-1000810` — because: it is a separate row on both ledgers, so the fourth conjunct is FALSE while it stays `OPEN`, however completely the underlying defect is fixed.
- Run the DoD check and record its real output — because: the conjuncts are only true when something observed them, and this is the thing that observes them.

DEFERRED, not in the MVP: the cross-repo filing to `.claude` about the recurrence. It prevents the
NEXT instance; it changes no conjunct of this `Done when`, this repo cannot build it anyway, and the
sibling pass has already written its body as `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md`.

Reaches the goal because: the four conjuncts of `Done when` map one-to-one onto this set — the two
status flips plus their evidence satisfy conjuncts one and two, the Item cells being left
byte-identical is what satisfies conjunct three (measured: deletion re-mints, `DONE` does not), and
the two relay deliveries satisfy conjunct four. The final step runs the DoD check itself, whose
positive control already returned `0` against exactly this end state.

Holds continuously because: the end state is a set of terminal rows in a committed file, and the
three unattended processes that touch it were each checked to leave it alone rather than merely hoped
to. `com.thc.xrepo-queue` re-mints only what `unqueued_answers()` returns, measured `[]` for the
`DONE` state. `com.thc.ledger-doctor --fix` can delete an order row only via C11, which cannot fire
while `grep -c "XR-ANS-001" PROJECT-LEDGER.md` stays at `1`, and it has no C3 fixer at all
(`grep -c "_fix_c3"` -> `0`). `com.thc.build-order-archive` moves the rows into the archive section
after 24h, which is fine and is evidenced by `XR-IN-1000014` already sitting there `DONE` and never
having been re-queued. Nothing needs doing again on any schedule, which is what makes this a fix
rather than an alarm.

## Build order

1. Read `XREPO/answers/ANSWER-amzn-api-amazon-ads-api-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` in full and act on it — verify locally that this tree carries no stale `Amazon_Ads_API` visibility claim and no local copy of the spec that answer edited, rather than taking its closing "nothing further is needed" on trust — gate: `grep -rn "Amazon_Ads_API" README.md START-HERE.md docs/ | grep -icE "public|private"` returns `0` AND `ls PLAN/specs/SPEC-doc-archive-truth.md` reports absent. (Both already OBSERVED this session; this is re-confirmation at build time, not discovery.)
2. Close `XR-ANS-001` — in `PROJECT-LEDGER.md:71` move the Status cell `QUEUED` -> `DONE` and append the step-1 evidence (the two commands and their results) plus the conclusion "answer read, nothing owed by this repo" to the Note cell, leaving the Item cell string byte-identical — gate: `grep -c "XR-ANS-001" PROJECT-LEDGER.md` still returns `1` AND that row's Status cell reads `DONE`.
3. Read `XREPO/answers/ANSWER-amzn-api-amzn-api-integration-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` in full and establish the current state of the publish it refused, because its premise ("nine commits, all local") was written 2026-08-22 — gate: `test "$(git rev-parse HEAD)" = "$(git rev-parse origin/main)"` exits `0` AND `git rev-list --count origin/main..main` prints `0`.
4. Close `XR-ANS-417` — in `PROJECT-LEDGER.md:72` move the Status cell to `DONE` and record in the Note cell that the refutation is ACCEPTED and its remedy MOOT (the doc surface reached `origin/main` at `2d54cad` via PR #1, so neither founder path it named is needed, and the publish step of `SPEC-spapi-archive-readable-and-guarded` / `PRJ-001` is satisfied without one), Item cell untouched — gate: `grep -c "XR-ANS-417" PROJECT-LEDGER.md` still returns `1` AND `python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo .` prints `-> 0 repaired, 0 open`.
5. Commit, staging by name — `git add PROJECT-LEDGER.md PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` and never `git add -A` (this tree carries 422 PDFs and untracked planning artifacts); do not attempt `git push`, which the policy guard blocks and which nothing here needs — gate: `git status --porcelain PROJECT-LEDGER.md` is empty AND `git log --oneline -1` names the ledger change.
6. Re-run the third reader against the REAL checkout, `python3 ~/.claude/tools/ledger-doctor.py --repo .`, which is what converts the single INFERRED arm in Blast radius into an OBSERVED one (it refuses an unregistered temp dir, returning `NOTHING WAS CHECKED (2 = could not look, never a pass)`) — gate: its output no longer contains the C3 line `the live order names 2 item(s) that are not rows in this ledger: XR-ANS-001, XR-ANS-417`.
7. Answer `XR-IN-1000833` — write one `ANSWER-*.md` naming the finding fixed (`INV-ORDER-001`), how (both ids taken terminal, Item cells deliberately NOT retyped), the commit hash from step 5, the before/after conformance lines, and the measurement that rejected deleting or retyping the ids; deliver it with `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000833 --body-file <that file>` — gate: `python3 ~/.claude/tools/ledger-read.py --repo . --xrin` shows `XR-IN-1000833  [DONE]`.
8. Answer `XR-IN-1000810` with the same body plus its duplicate status — same fix, separate row on both ledgers, separate relay call; the body additionally states that `XR-IN-1000810` and `XR-IN-1000833` are the same OI-9019 finding filed twice ~3.5h apart, so estatehub can collapse them at source — gate: `python3 ~/.claude/tools/ledger-read.py --repo . --xrin` shows `XR-IN-1000810  [DONE]`.
9. Make sure the RECURRENCE is filed to the repo that owns it, `.claude`, exactly once — check first whether the sibling pass's `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md` has already been sent (that file names `.claude` as owner repo and itself as the request body), and only if no open instruction exists there, send it with `python3 ~/.claude/tools/xrepo-relay.py request --to .claude --title "answer_order_id() mints XR-ANS-nnn ids that estate-conformance INV-ORDER-001 flags, and OI-9019 escalates them cross-repo" --body-file PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md`; never pass `--force-duplicate` here — gate: exactly one open instruction on `.claude` carries this ask, and this repo's outbox names it once.
10. Run the full DoD check block above verbatim — gate: it exits `0` (its negative control on today's tree returned `1`; its positive control on the end-state fixture returned `0`; both were run during planning).

## Items

- Read `XREPO/answers/ANSWER-…-XR-IN-1000013-amazon-ads-api-is-private-not-public-readme-16-s.md` and confirm against this tree that nothing is owed here (no stale `Amazon_Ads_API` visibility claim in `README.md`/`START-HERE.md`/`docs/`, no local `SPEC-doc-archive-truth.md`).
- Take `XR-ANS-001`'s live-order row (`PROJECT-LEDGER.md:71`) to `DONE` with that evidence in its Note cell, leaving the Item cell string untouched.
- Read `XREPO/answers/ANSWER-…-XR-IN-1000067-push-amazon-sp-api-doc-surface-to-origin.md` and establish the current publish state of this tree (`HEAD` vs `origin/main`).
- Take `XR-ANS-417`'s live-order row (`PROJECT-LEDGER.md:72`) to `DONE`, recording the refutation as accepted and its founder-only remedy as moot because the doc surface reached `origin/main` at `2d54cad` via PR #1 — which also retires the publish step of `SPEC-spapi-archive-readable-and-guarded` for `PRJ-001`.
- Commit `PROJECT-LEDGER.md` and this spec by name (no `git add -A`, no `git push`).
- Re-run `ledger-doctor.py --repo .` against the real checkout and confirm its C3 line no longer names the two ids.
- Write the `ANSWER-*.md` and deliver it to estatehub for `XR-IN-1000833` via `xrepo-relay.py answer`.
- Deliver the same answer for the duplicate instruction `XR-IN-1000810`, stating explicitly that the two are one finding filed twice so estatehub can collapse them at source.
- Ensure the RECURRENCE is filed to `.claude` exactly once — `answer_order_id()` mints an id no row defines, and its docstring reasons only about `ledger-doctor.py` C3 being report-only, not knowing that `estate-conformance.py:1622` INV-ORDER-001 flags the same shape and that OI-9019 escalates it into cross-repo instructions, so every future answered `XR-OUT-nnn` estate-wide manufactures a fresh finding; the sibling pass already wrote the body as `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md`, so check before sending and never `--force-duplicate`.
- Run the DoD check and record its real output in the closing row.
