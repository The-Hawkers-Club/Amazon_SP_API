# SPEC-build-order-phantom-xr-ans-items — the two ids at the head of this repo's build order stop being unbuildable ghosts, because the answers they point at are read and closed with evidence

**Source:** PLAN/dumps/20260905192730-xrin-xr-in-1000810-oi-9019-build-order-hygiene-inv-order-001-1-find.md
**Status:** READY            <!-- DRAFT -> QUESTIONS-OUT -> READY -> ADOPTED -->
**As of:** 2026-09-05

## Goal

The two items at seq 1 and seq 2 of this repo's live build order — `XR-ANS-001` and `XR-ANS-417` —
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

## Done when

`python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo .`, run from
this repo's canonical checkout, reports **0 open** across all 11 selected invariants (it reports
1 open today); `overnight-run.schedule()` returns no entry with `no_rows=True` for this ledger and its
plan head is `PRJ-001`; and both `XR-IN-1000810` and `XR-IN-1000833` read terminal on this repo's
incoming cross-repo table with answers delivered into `estatehub`.

## DoD check

```sh
set -u
cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1
python3 ~/.claude/tools/estate-conformance.py --check --only INV-GOV,INV-ORDER --repo . 2>&1 \
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

## Fits

The whole change is two status cells and two note cells in one file. There is no code in this repo to
change — this is a data defect in the ledger, and the code that reads it is estate-wide and correct.

- `PROJECT-LEDGER.md:71` — order row seq 1, `| 1 | XR-ANS-001 | QUEUED | …`. Status cell
  `QUEUED` → `DONE`; Note cell gains the evidence sentence and **keeps** its `` `XR-OUT-001` ``.
- `PROJECT-LEDGER.md:72` — order row seq 2, `| 2 | XR-ANS-417 | QUEUED | …`. Status cell
  `QUEUED` → `MOOT`; Note cell gains the current-state citation and **keeps** its `` `XR-OUT-417` ``.
- `PROJECT-LEDGER.md:61` and `:62` — the `XR-IN-1000810` / `XR-IN-1000833` inbox rows, retyped to
  terminal by `xrepo-relay.py answer`, not by hand (both tables carry a `MANAGED BY … do not
  hand-edit rows` banner at `:39-42` and `:53-56`).
- `PROJECT-LEDGER.md:86` — `## Build order — COMPLETED (archive)`, where `order-archive.py` will move
  both rows once they are terminal for 24h. Nothing to edit; named because it is where they go.

Deliberately **not** touched: no `OI-` row is raised, so `PROJECT-LEDGER.md:10`'s `**Next IDs:**`
pointer and `:19`'s reconciliation line are unchanged. An earlier draft of this spec raised an
`OI-0012` for a supposed unpushed-commits residual on `XR-ANS-417`; that residual does not exist
(see Conflicts), and raising a row for it would have put a permanently-blocked founder item on
`PRJ-001` for work already done.

**The entry point production takes, traced rather than assumed:**
`estate-conformance.py:1622 inv_order_items_resolve` imports `overnight-run.py` and calls
`ov.schedule(text)`; its finding is the comprehension at `estate-conformance.py:1652`
(`p["no_rows"] and not p["all_blocked"] and not p["exhausted"]`). `schedule()` skips terminal items
outright (`if (it.get("status") or "").upper() in TERMINAL: continue`), so a terminal item cannot be
unreachable — that single line is the entire repair. `schedule()` builds `by_row` from
`render-open-ledger.py`'s `scan(text)["rows"]`, which against this ledger this session returned
exactly `OI-0001`, `XR-OUT-001`, `XR-OUT-417`, `XR-IN-1000014`, `XR-IN-1000810`, `XR-IN-1000833`,
`OI-0002`…`OI-0011`. **Neither `XR-ANS-001` nor `XR-ANS-417` is among them**, which is the defect,
enumerated against the authoritative source rather than asserted.

## Wiring

There is nothing to wire — no new code, no new caller. What must be true instead is that the readers
of these bytes keep agreeing after the edit, and each was probed:

- **producer:** `xrepo-queue.py:714 queue()` → **consumer:** `PROJECT-LEDGER.md:69-85`, the live order
  table. This is what wrote both phantom rows on 2026-09-02, via `xrepo-queue.py:207 unqueued_answers`
  → `xrepo-queue.py:274 answer_order_id`. It runs on a schedule, so after the edit it must NOT write
  them again. Guarded by `xrepo-queue.py:461`, verified live on the post-fix text this session:
  `_outbox_id_referenced_in_any_order(text, "XR-OUT-001")` → `True`, `("XR-OUT-417")` → `True`,
  because `xrepo-queue.py:695 _answered_outbox_note` put those ids in the Note cell in prose and
  `_order_section_bodies` (`xrepo-queue.py:400`) searches the **whole body** of **every**
  `## Build order …` section, Item column or not.
- **producer:** `PROJECT-LEDGER.md:69-85` → **consumer:** `overnight-run.py:2388 schedule()`, which
  every cycle and the overnight runner walk. Verified post-fix on the temp copy: both rows drop out of
  the plan entirely and the head becomes `PRJ-001`, with all 13 remaining items at `no_rows=False`.
- **producer:** `PROJECT-LEDGER.md` → **consumer:** `order-archive.py`, which moves items terminal for
  >24h into `## Build order — COMPLETED (archive)` at `PROJECT-LEDGER.md:86`. This is the one move
  that could silently un-arm the re-queue guard later, so it was probed rather than assumed:
  `_order_section_bodies` matches `^##\s+Build order\b` and the COMPLETED heading matches it, so both
  notes travel into the archive still naming their `XR-OUT-nnn` id and the guard keeps holding.
- **producer:** `xrepo-relay.py` `answer` → **consumer:** `estatehub`'s ledger. This is the only edge
  that writes outside this repo, and it is the one the instruction itself names as the close
  condition: *"The loop is not closed until the answer exists on the other side."*

## Conflicts

- **🔴 The correction this spec was rewritten for.** An earlier draft treated `XR-ANS-417` as carrying
  a live founder residual — nine unpushed commits, blocked on PRJ-001's Question 1 — taken from the
  refutation's own text. **Probed against the remote and found overtaken.** After an actual
  `git fetch origin`: `git rev-list --count origin/main..HEAD` → **1**, `HEAD..origin/main` → **0**,
  and the single unpushed commit is `c72de9e`, a spec file written by a concurrent planning pass
  minutes ago. `git ls-tree -r --name-only origin/main` lists `START-HERE.md` and
  `docs/01-getting-started.md` … `docs/06-coverage-report.md` — **the doc surface is published** —
  landed by `abc4c83` via merged pull request `2d54cad` (*"Merge pull request #1 from
  The-Hawkers-Club/fix/…-fast-lane-bulk-land-amzn-api-amazon-sp-a"*). A merged PR is a route neither
  `XR-OUT-417` nor its refutation considered; both reasoned only about `git push` from a local
  checkout, which is still blocked and still `push=no`. The ask is satisfied by another path, so the
  row is MOOT, not blocked.
- **The same finding was filed at this repo twice.** `XR-IN-1000810` (this dump) and `XR-IN-1000833`
  (`PROJECT-LEDGER.md:62`) are both estatehub OI-9019, both `INV-ORDER-001`, both naming the identical
  pair: the 1000810 request says *"what to do about it: XR-ANS-001, XR-ANS-417"*; the 1000833 request
  says *"Affected id(s): `XR-ANS-001, XR-ANS-417`"*. **This is not two units of work.** One fix closes
  both, and both inbox rows must be answered — steps 5 and 6.
- **A concurrent planning pass produced a second spec for the same fix, and it is not a rival.**
  `PLAN/specs/SPEC-spapi-xr-ans-order-ids-resolve.md` (committed as `c72de9e`) is sourced from the
  duplicate dump `XR-IN-1000833` and specifies the same two terminal transitions. It reached the
  `XR-ANS-417`-is-moot conclusion independently and got there first. The pipeline pairs each spec to
  its own dump by the `**Source:**` line, so both files must exist; **but this is one build.**
  Whichever is adopted first should be built, and the other closed as satisfied by the same commit —
  they must not both be executed, because both edit `PROJECT-LEDGER.md:71-72` and would race.
- **rules:** `grep -n 'build order' ~/.claude/CLAUDE.md` → the session directive. Nothing forbids
  retyping an order row's status; what it forbids is *approving or queueing* an order, which this spec
  does not do. The two rows are already on an order he approved 2026-08-21T00:00:00Z; this changes
  what they report, not whether they are authorised.
- **live rows:** touches `PROJECT-LEDGER.md:71` and `:72` only. It touches **no** `OI-` row.
  `OI-0010` ("Commit locally … do not push … file the publish request through `xrepo-relay.py`") is
  the row that *produced* `XR-OUT-417`; it is left alone deliberately — its own status is PRJ-001's
  business, and pointing seq 2 at it would cross-list one id twice in the same order table, which is
  the very defect class this instruction exists to close.
- **decisions:** this repo has no `OPEN-DECISIONS.md` (`ls OPEN-DECISIONS.md` → *No such file or
  directory*), so no local decision can conflict. The governing push rulings live in
  `AMZN API/amzn-api-integration/DECISIONS.md:5870` (**DEC-0146**) and `:6369` (**DEC-0242**), both
  ruled *"the block stays"*, and both are about the `owned-api-integration` class rather than this
  repo's `org-api-mirror`. Neither is contradicted: this spec does not push and does not propose
  pushing, and nothing here asks for the policy to be widened.
- **the synthetic id is deliberate, not a typo.** `xrepo-queue.py:274 answer_order_id`'s docstring
  states `XR-ANS-nnn` is *"DELIBERATELY NOT the bare `XR-OUT-nnn` id"*, so that `ledger-doctor.py`'s
  C11 auto-repair — unattended, no env var, every 1800s — cannot delete the row for colliding with a
  terminal twin. **So the ids must not be retyped to `XR-OUT-nnn`.** Closing them in place, which is
  what this spec does, respects that constraint entirely.

## Blast radius

Two status cells and two note cells in one file. What reads that file, enumerated against the
authoritative registry rather than guessed:

- **This repo's own cycle — the largest effect, and the intended one.** The plan head moves from a
  phantom to `PRJ-001`. The session directive currently names `XR-ANS-001` as *"the next BUILDABLE
  item"*; it is not buildable by anyone. Afterwards the runner starts on `PRJ-001`, which is a real
  10-row project with a real DoD check, so **work volume goes up**, not down.
- **`xrepo-queue.py` re-queueing.** The one way this edit can bite. Guarded and verified above, and
  the DoD check asserts both the guard and `unqueued_answers(".") == []` directly, so a future edit
  that drops the `XR-OUT-nnn` prose from a note reddens the check instead of silently re-opening the
  loop on the next scheduled tick.
- **`ledger-doctor.py` C3 / C11.** C3 ("the order names a row that does not exist") currently names
  both ids and is report-only — `grep -n '_fix_c3' ~/.claude/tools/ledger-doctor.py` → no match, and
  its `fix()` calls only `_fix_c5`/`_fix_c5b`/`_fix_c11`. Afterwards both remain C3 ghosts but are
  terminal, so no cycle reaches them and no repair path touches them. C11 is unreachable because
  neither id names a row anywhere, which is the whole reason `answer_order_id` chose the shape.
- **The rendered page.** Two items leave the IN PROGRESS panel and, after 24h, appear under
  COMPLETED. Nothing new appears — this spec raises no row.
- **`estatehub`.** Two answers land on its ledger via `xrepo-relay.py`. That is the point of the
  instruction, and it is the only write outside this repo.
- **Nothing else outside this repo.** Absence claim, enumerated rather than asserted:
  `grep -rn 'XR-ANS-001\|XR-ANS-417'` across the registered estate finds these two ids only inside
  this repo's own tree — `PROJECT-LEDGER.md`, the two `XREPO/requests/` files, the two `PLAN/dumps/`
  copies and the specs. Positive control that the sweep reaches other repos: the same walk across the
  62-row registry returns 1,371 `XR-ANS-*` unreachable items in 30 **other** repos, so it is not
  returning a short list because it cannot see them. **Those 1,371 are the upstream generator's
  defect and are specced separately** — `PLAN/specs/SPEC-xrepo-queue-mints-unreachable-order-ids.md`.
- **What this deliberately does NOT change:** `origin/main` is not touched, nothing is pushed, the
  intake policy is not touched, `PRJ-001`'s rows are not touched, and no PDF moves.
- **One thing he should know, not a change this spec makes:** `docs/05-archive-index.md` — the
  542-line machine-readable index of 422 Amazon documents — is now **live on a public GitHub repo**.
  `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` **Question 1** (public or private?) argued
  its own cost as near-zero partly because that index was not yet published. It is now. The question
  is unchanged and stays where it is; only its urgency moved, and it is flagged here rather than
  re-asked (see Questions).

## Blockers

Swept for the six classes; each was looked at with a command, and each command has a control.

- **A missing credential or grant** — none needed. Two cell edits plus two `xrepo-relay.py` answer
  calls, in a repo this session already has full edit and commit authority over, writing to a sibling
  ledger on the same disk. Control that the sweep would have found one: it did surface the push
  capability gap below, from the same evidence base.
- **An absent upstream field or endpoint** — none. Every reader this depends on exists and was
  imported and executed this session: `overnight-run.py:2388 schedule()`,
  `xrepo-queue.py:461 _outbox_id_referenced_in_any_order`, `xrepo-queue.py:207 unqueued_answers`,
  `estate-conformance.py:1622`. `MOOT` was confirmed present in `overnight-run.py`'s `TERMINAL`.
- **A counterparty who must ship first** — none. Both answers landed on 2026-08-21 and 2026-08-22,
  both files are on disk, and both were read in full while writing this spec. Nothing is awaited.
- **A founder ruling this contradicts** — none. DEC-0146 and DEC-0242 rule the push block stays; this
  spec does not push. Control that the grep discriminates: the same search over
  `amzn-api-integration/DECISIONS.md` returns both ids with their rulings, so an absence elsewhere is
  a reading and not a broken search.
- **A capability that does not exist** — one, and it does **not** block this spec. No session on this
  machine may `git push` this repo: `~/.claude/state/repo-intake-policy.tsv` line 52 sets the
  `org-api-mirror` class (which names both AMZN THC trees) to `push=no`, and
  `push-policy-guard.classify()` returned `blocked=True` for both AMZN trees against `blocked=False`
  for the control `Marketing System/leadgen`. It does not block this spec because **this spec pushes
  nothing**, and because the work `XR-OUT-417` asked for arrived on `origin/main` by merged PR
  instead. **RESOLVED — the ask is satisfied without the capability.**
- **A gate that would refuse it** — the estate's pre-bash hook refuses any shell command whose text
  names the intake-policy TSV alongside an output redirection, including a harmless `2>/dev/null`
  (hit live this session). Not a blocker here — the note cells this spec writes do not quote that path
  — but it is why any row text that *does* quote it must be written with `Edit`, never a heredoc.

**No BLOCKER is unanswered.**

## Questions

**None for him.** This is instructed cross-repo work (`XR-IN-1000810`), already authorized by the
sending repo, and the instruction's own text says the judgement it needs — *"which row/section is
authoritative"* — belongs to the receiving repo's project owner, not the founder. Every such
judgement was settled from the code, the two answer files, and the observed state of `origin/main`,
and each is recorded above with the probe that settled it.

One genuinely-his question is **touched but deliberately not re-asked**: whether
`The-Hawkers-Club/Amazon_SP_API` stays public or flips to private is already
`PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` **Question 1**, still pending and live on his
page as `PRJ-001`. What changed is only its premise — that spec argued the cost of flipping was near
zero partly because `docs/05-archive-index.md` had not been published, and PR `2d54cad` has since
published it. The right response is to carry that fact into the existing question, not to open a
second one: asking twice is worse than asking once, which is that spec's own standard. Build order
step 4 does exactly that, as a premise update with no new ask attached.

## MVP

The shortest route to a true `Done when` is **steps 1-3** — retype the two status cells with their
evidence, then commit. That is what makes
`estate-conformance --check --only INV-GOV,INV-ORDER --repo .` read `0 open` and moves the plan head
to `PRJ-001`; it was verified in exactly that reduced form on a temp copy this session. Step 4 is a
one-line premise update to an existing question, and steps 5-6 close the cross-repo loop. A run that
stops after step 3 leaves the repo strictly better and unblocked: the order head is buildable and no
cycle emits a degenerate plan again. A run that stops after step 2 without step 3 loses the work, so
the commit is the last step that cannot be dropped.

The MVP, named as rows:
- Close build-order seq 1 (`XR-ANS-001`) as DONE with the answer's own closing line as evidence, leaving the Note cell's `` `XR-OUT-001` `` untouched — because: `Done when` requires 0 open, and this is one of the two unreachable ids; fixing only the other leaves the finding firing with one id.
- Close build-order seq 2 (`XR-ANS-417`) as MOOT citing the merged PR and the measured ahead=1 / behind=0, leaving the Note cell's `` `XR-OUT-417` `` untouched — because: it is the second unreachable id, and without it `schedule()` still returns a `no_rows=True` entry and the plan head is still not `PRJ-001`.
- Commit `PROJECT-LEDGER.md` by name — because: both arms of `Done when` are read from the canonical checkout's file on disk, and an uncommitted edit is lost or reverted by the next session, making the observable state false again.

**Reaches the goal because:** `Done when` has three arms and this set closes the two that are about
this repo's own state. Arm 1 — the conformance run reads `0 open` — was verified in precisely this
reduced form on a temp copy: retyping only these two status cells took the run from `1 open` to
`1 repos x 11 invariants -> 0 repaired, 0 open`. Arm 2 — no `no_rows=True` entry, head `PRJ-001` —
was measured on the same copy and returned `dead=[]` with the head at `PRJ-001`, because `schedule()`
skips terminal items outright. There are exactly two unreachable ids in this ledger and this set
addresses both, so nothing outside it can keep either arm false. Arm 3 (the two inbox rows terminal)
is steps 5-6 and is deliberately outside the MVP: it is what the *other* repo is owed, not what makes
this repo correct.

**Holds continuously because:** the only mechanism that could undo this unattended is
`xrepo-queue.py`, which runs on a schedule and re-appends any answered outbox row it believes is in no
order. It will not re-append these: `xrepo-queue.py:207 unqueued_answers` skips a row when
`_outbox_id_referenced_in_any_order` (`:461`) finds the literal `` `XR-OUT-nnn` `` anywhere in an
order-section body, and both Notes keep that string — probed against the post-fix text this session,
both returning `True`. It survives archival: `_order_section_bodies` (`:400`) matches every
`^## Build order` heading, so both notes still count once `order-archive.py` moves them into
`## Build order — COMPLETED (archive)`. `ledger-doctor.py`'s unattended `--fix` cannot touch them
either, because C3 is report-only and C11 needs an id that also names a terminal row elsewhere, which
neither id does. No human step recurs, and no row is left waiting on anyone. The DoD check's
`unqueued_answers(".")` assertion is the standing regression guard: if a future edit drops the
`XR-OUT-nnn` prose, it reddens instead of the backlog silently rebuilding.

## Build order

1. **Close order seq 1** at `PROJECT-LEDGER.md:71`: status `QUEUED` → `DONE`, Note appended with the evidence — the `XR-OUT-001` answer was read, Amazon_Ads_API corrected its own `README.md:16` and `START-HERE.md:26` and closed its spec's visibility BLOCKER, and its closing line is *"Nothing further is needed from `Amazon_SP_API`"* — while keeping `` `XR-OUT-001` `` verbatim in the Note. — gate: `grep -c 'XR-OUT-001' PROJECT-LEDGER.md` is unchanged from its pre-edit value AND the seq-1 row matches `XR-ANS-001` with status `DONE` on exactly one line.
2. **Close order seq 2** at `PROJECT-LEDGER.md:72`: status `QUEUED` → `MOOT`, Note appended with the current state — `XR-OUT-417` was REFUTED as routed and its residual is overtaken, because the doc surface reached `origin/main` via merged PR `2d54cad` (`abc4c83`), leaving `origin/main..HEAD` = 1 and `HEAD..origin/main` = 0 as measured after `git fetch` — while keeping `` `XR-OUT-417` `` verbatim in the Note. — gate: `grep -c 'XR-OUT-417' PROJECT-LEDGER.md` unchanged AND `git ls-tree -r --name-only origin/main | grep -c 'docs/05-archive-index.md'` returns 1, so the cited evidence is still true at build time.
3. **Commit**, staging `PROJECT-LEDGER.md` by name and never `git add -A`, then run the DoD check exactly as written above, writing the exit code into the log with `echo "EXIT=$?" >> …` and reading the log rather than any wrapper's status. — gate: `git show --stat HEAD` lists `PROJECT-LEDGER.md` and nothing else, and `/tmp/spec-phantom-dod.log` ends `EXIT=0` with its conformance line reading `0 repaired, 0 open`.
4. **Update Question 1's premise** in `PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` — one dated line recording that `docs/05-archive-index.md` is now published on the public repo by PR `2d54cad`, so the "cost of flipping is near zero" argument is read against current fact; the question, its options and its pending answer are left exactly as they are, and no new question is raised. — gate: `grep -c '2d54cad' PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` returns 1 AND the count of pending-answer markers in that file is unchanged.
5. **Answer `XR-IN-1000810`** with `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000810 --body-file <what-I-did.md>`, naming step 3's commit SHA, the before/after of both order rows, and the `0 open` conformance output. — gate: `PROJECT-LEDGER.md:61`'s Status cell reads terminal and its Answer cell names a file that exists on disk.
6. **Answer `XR-IN-1000833`** the same way, citing the *same* commit and stating explicitly that it is the duplicate of `XR-IN-1000810` — same invariant, same two ids, closed by one fix — which is the "already stale / MOOT is a valid answer too" branch the instruction itself invites. — gate: `python3 ~/.claude/tools/ledger-read.py --repo . --xrin` shows no OPEN incoming row.

## Items

- Close build-order seq 1 (`XR-ANS-001`) as DONE at `PROJECT-LEDGER.md:71`, citing the Amazon_Ads_API answer's own closing line *"Nothing further is needed from `Amazon_SP_API`"* as evidence, and leaving the Note cell's `` `XR-OUT-001` `` untouched so the re-queue dedupe keeps holding.
- Close build-order seq 2 (`XR-ANS-417`) as MOOT at `PROJECT-LEDGER.md:72`, citing merged PR `2d54cad` and the post-fetch ahead=1 / behind=0 measurement that overtakes the refutation's nine-unpushed-commits premise, and leaving the Note cell's `` `XR-OUT-417` `` untouched for the same reason.
- Commit `PROJECT-LEDGER.md` by name and run the DoD check, capturing the exit code into the log rather than reading a wrapper's status.
- Record a dated premise update under Question 1 of `SPEC-spapi-archive-readable-and-guarded.md` noting that `docs/05-archive-index.md` is now published, without re-asking the question or altering its options.
- Answer `XR-IN-1000810` through `xrepo-relay.py`, naming the commit and the conformance output.
- Answer `XR-IN-1000833` as the duplicate of `XR-IN-1000810`, closed by the same commit, so both inbox rows go terminal.
