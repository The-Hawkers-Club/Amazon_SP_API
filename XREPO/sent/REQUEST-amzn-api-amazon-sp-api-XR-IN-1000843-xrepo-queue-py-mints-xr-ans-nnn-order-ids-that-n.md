# xrepo-queue.py mints XR-ANS-nnn order ids that name no row — 1,371 unreachable build-order items in 30 repos

- **Request id:** `XR-IN-1000843`
- **From repo:** `AMZN API/Amazon_SP_API`
- **To repo:** `.claude`
- **Filed:** 2026-09-06T01:41:39Z
- **Instruction key:** `5a8a67985fca`
- **Originating rows:** —

> Filed by `xrepo-relay.py` under RULE-L24: cross-repo work is filed as an instruction, never handed back as a question.
> **When you have executed this, run:** `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000843 --body-file <what-you-did.md>`
> That writes the answer into `AMZN API/Amazon_SP_API` and lands a row on ITS ledger. The loop is not closed until the answer exists on the other side.

---

# SPEC-xrepo-queue-mints-unreachable-order-ids — a queued answer becomes a real ledger row instead of a synthetic id that names nothing, and the 1,371 already written estate-wide are repaired

**Source:** PLAN/dumps/20260905192730-xrin-xr-in-1000810-oi-9019-build-order-hygiene-inv-order-001-1-find.md
**Status:** READY            <!-- DRAFT -> QUESTIONS-OUT -> READY -> ADOPTED -->
**As of:** 2026-09-05
**Owner repo:** `.claude` (registry row 1 of `~/.claude/state/repo-registry.tsv` → `/Users/peterbeke/.claude`), which owns `tools/xrepo-queue.py`. Filed there via `xrepo-relay.py request`; this file is the body.

## Goal

When an answer comes back to an ask this estate sent, `xrepo-queue.py` puts a follow-up item on the
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

## Done when

`python3 ~/.claude/tools/estate-conformance.py --check --only INV-ORDER` across the registered estate
reports **zero** `INV-ORDER-001` findings whose detail names an `XR-ANS-*` id (it names 1,371 today,
across 30 repos), and a fresh `xrepo-queue.py` run against a fixture with an answered outbox row
appends an item whose Item cell names a row that exists in the same ledger.

## DoD check

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

## Fits

Every locus is a shared estate tool under `~/.claude/tools/`, so each is cited below by the only name
it has — there is no repo-relative path for these files by construction.

- `xrepo-queue.py:274` — `answer_order_id(r)`, which returns `f"XR-ANS-{digits}"`. This is the mint.
  It must stop being the *only* thing that happens: the id it returns has to correspond to a row that
  exists.
- `xrepo-queue.py:714` — `queue(repo, rows, dry, note_fn)`, the shared append for both populations.
  It already holds the ledger open and already writes the Note cell; raising the companion row belongs
  **inside this transaction**, not in a second pass that can fail separately.
- `xrepo-queue.py:695` — `_answered_outbox_note`, which writes the real `XR-OUT-nnn` id into the Note
  in prose. **This must not change.** It is the only surviving link between the order item and the
  outbox row, and `xrepo-queue.py:461` `_outbox_id_referenced_in_any_order` is the dedupe that reads
  it (`XR-IN-1000719`'s fix). Any redesign that stops writing that prose re-opens a closed defect.
- `_ledger.py:1302` — `with_allocated_oi(ledger_path, n, mutate)`, **the writer's door**. It reserves
  ids and writes the caller's rows in one locked transaction, which is exactly the shape this needs
  and is why the fix does not require new locking. There is already a working caller to copy:
  `estate-conformance.py:1605` uses it to raise rows into the Unfiled table via a `mutate(text, ids)`
  closure, and bumps the Portfolio with `_bump_unfiled_portfolio`.
- `overnight-run.py:2388` — `schedule()`, the consumer. **Do not change it.** See Conflicts for the
  cheap fix here that is wrong.
- `estate-conformance.py:1622` — `inv_order_items_resolve`, the grader whose finding count is the
  Done-when. Also unchanged.
- `render-open-ledger.py` — `scan(text)["rows"]`, which is what `schedule()` reads to build `by_row`
  and is therefore what decides whether the newly raised row is visible. Unchanged, but it is the
  reason the new row must land in a table `scan()` parses (the Unfiled table qualifies — verified
  against `AMZN API/Amazon_SP_API` this session, where `scan()` returned `OI-0001` from exactly it).

**The entry point production takes, traced rather than grepped for a plausible name:**
`xrepo-queue.py:207` `unqueued_answers(repo)` reads the OUTBOX table, filters to terminal rows, calls
`answer_order_id` at `:256`, skips anything already booked via `_inorder_ids` (`:156`) or
`_outbox_id_referenced_in_any_order` (`:265`), and hands what survives to `queue()`. That is the only
path that writes an `XR-ANS-*` Item cell, confirmed by enumerating producers rather than assuming:
`grep -rln 'XR-ANS-' ~/.claude/tools/` returns `xrepo-queue.py` as the sole producer, with the other
hits being `.bak` copies and read-only consumers.

## Wiring

- **producer:** `~/.claude/tools/xrepo-queue.py:714 queue()` → **consumer:** each repo's
  `PROJECT-LEDGER.md` `## Build order — IN PROGRESS` table. Live, scheduled, and already running: it
  is what wrote all 1,371 items now on disk, so there is no question whether this code path executes.
- **producer:** `PROJECT-LEDGER.md` order table → **consumer:**
  `~/.claude/tools/overnight-run.py:2388 schedule()` → **consumer:**
  `~/.claude/tools/estate-conformance.py:1622`. The whole defect lives in this chain and every link
  was executed this session against real ledgers.
- **the new link this spec adds:** `queue()` → `_ledger.with_allocated_oi` →
  the receiving repo's `PRJ-000` Unfiled table. This is a **new** producer→consumer edge, so it is
  the one that can be built correct and inert. It is not inert here, because `schedule()` reads
  `render-open-ledger.scan(text)["rows"]`, which reads the Unfiled table — verified against
  `AMZN API/Amazon_SP_API` this session, where `scan()` returned `OI-0001` from exactly that table.
- **repair pass:** a new `xrepo-queue.py repair` (or a sibling actuator) → the same
  `with_allocated_oi` door → the same tables. Same edge, run once over the backlog.

## Conflicts

- **The obvious cheap fix is WRONG and must be named so nobody takes it.** `schedule()` could be made
  to resolve `XR-ANS-nnn` back to its `XR-OUT-nnn` row — the mapping already exists in the Note cell
  and `_outbox_id_referenced_in_any_order` already reads it. That would clear all 1,371 findings in
  one small diff. **Do not.** An answered `XR-OUT` row is terminal by construction, so the item would
  resolve to a terminal row and report `exhausted` (`~/.claude/tools/overnight-run.py:2534`), which
  `INV-ORDER-001` deliberately excludes — i.e. it would read as *finished*. That re-creates precisely
  the bug `unqueued_answers` exists to close, in its own words: *"'closed' and 'actioned' are
  different states … 2,528 XR-OUT rows read a terminal outcome with the id appearing NOWHERE else in
  the file"*. It would silence the invariant while making 1,371 unread answers invisible again.
- **`XR-ANS-nnn` must not be replaced by the bare `XR-OUT-nnn` id either.** `answer_order_id`'s
  docstring records this being caught before shipping: `ledger-doctor.py`'s C11 auto-repairs, with no
  env var and unattended every 1800s, any order row whose id also names a terminal row elsewhere —
  *"154 rows on `.claude`'s own ledger, silently gone the next time the evidence gate passed, with
  nobody ever prompted to read a single answer."* A freshly-allocated **OPEN** `OI-nnnn` row has no
  terminal twin, so it is invisible to C11. That is why the fix allocates rather than reuses.
- **rules:** `grep -n 'process-loop\|alarm is not very useful' ~/.claude/CLAUDE.md` → the standing
  rule that *"a scheduled thing without a loop is a timer"* and *"an alarm is not very useful because
  it's not done"*. This spec is on the right side of it: the repair is an actuator that converges the
  backlog, not a report that names it. Nothing in `~/.claude/commands/CLAUDE.md` forbids
  `xrepo-queue.py` writing a row — it already writes order rows.
- **live rows:** in **this** repo, the only rows touched by the sibling spec are
  `PROJECT-LEDGER.md:71-72` plus a new `OI-0012`; this spec touches none of them. In `.claude`, the
  rows are that repo's to raise on adoption.
- **decisions:** `grep -rn 'XR-ANS' ~/.claude/PROJECT-LEDGER.md | wc -l` → **575** occurrences, and
  `schedule()` against that same ledger returns **0** `XR-ANS` items in the live plan and **0**
  unreachable — every one of them is in a terminal or archived section. So the owning repo is the one
  repo the defect does not currently bite, which is itself the reason it has gone unfixed: there is no
  local pressure to notice it. Stated because it changes how this filing should be read, not as an
  accusation.
- **an existing filing on the adjacent surface:**
  `~/.claude/XREPO/requests/REQUEST-amzn-consulting-XR-IN-1000719-retyping-an-xr-ans-order-row-un-arms-xrepo-queue.md`
  already fixed the *retype* hazard on this exact mechanism. This spec is the **next** defect on the
  same surface, not a re-file of that one: 1000719 asked "a retype un-arms the dedupe", this asks
  "the id should never have needed retyping".

## Blast radius

- **30 repos' build orders are rewritten by the repair pass** — 1,371 Item cells retyped and 1,371
  rows raised. Enumerated against the authoritative registry (62 rows, 60 with a build order), not
  estimated: `estatehub` **1,096**, `Forecasting Gap Analytics` 66, `AMZN API` 41, `AMZN-Competitor`
  32, `TradeIQ` 26, `Anthropic-Watch` 24, `cmq-adcomm` 15, `AMZN-shared` 10, `THC` 9,
  `AMZN API/amzn-api-integration` 8, and 20 more with 1–5 each. This is the largest single
  consequence and it is why the repair must be idempotent and must run per-repo, one locked
  transaction at a time.
- **`estatehub` absorbs 80% of it.** The repo that filed this class of finding at other repos is
  itself carrying 1,096 of them. A repair pass that runs there is a 1,096-row ledger write; it should
  be run first, alone, and read before the other 29 follow.
- **Every repo's OI id space advances.** Raising 1,371 rows consumes 1,371 `OI-` ids. Safe only
  through `_ledger.with_allocated_oi`, whose whole existence is the recorded "two rows, one name"
  clobber (`OI-0006` in both PRJ-002 and PRJ-004). A repair that allocates outside that door will
  reproduce that incident 1,371 times.
- **Each repo's next buildable item changes.** Today those 1,371 items are skipped as unbuildable;
  afterwards each resolves to a live OPEN row, so runners will start picking them up. That is the
  intended effect and it is a real increase in work volume — 1,371 answers that have been sitting
  unread become buildable. It argues for the repair being ordered (estatehub first) rather than
  fanned out.
- **What does NOT change:** `_answered_outbox_note`'s prose, so `_outbox_id_referenced_in_any_order`
  keeps de-duping; `schedule()`; `INV-ORDER-001`; and the `XR-OUT` outbox tables, which are not
  touched at all.
- **Absence claim, enumerated:** nothing outside `~/.claude/tools/` produces an `XR-ANS-` id.
  `grep -rln 'XR-ANS-' ~/.claude/tools/` returns `xrepo-queue.py` as the only producer (other hits
  are `.bak` copies and consumers that read the string). Positive control that the grep reaches
  producers: the same search over `~/.claude/tools/` returns `xrepo-relay.py` for `XR-OUT-`, so it is
  not returning a short list because it cannot see the directory.

## Blockers

- **A missing credential or grant** — none. Everything is local file work in `~/.claude`, a
  registered working directory. Control: the same sweep did surface the write-guard below, so it
  discriminates.
- **An absent upstream field or endpoint** — none. `_ledger.with_allocated_oi` exists at
  `~/.claude/tools/_ledger.py:1302` and has a working caller at
  `~/.claude/tools/estate-conformance.py:1605`; both were read this session.
- **A counterparty who must ship first** — none. This repo (`AMZN API/Amazon_SP_API`) does **not**
  depend on it: its own two items are repaired by hand under
  `PLAN/specs/SPEC-build-order-phantom-xr-ans-items.md`, and that repair is durable without this one
  because `_outbox_id_referenced_in_any_order` prevents re-queueing (verified live: both probes
  returned `True` against the post-fix text). The two specs are genuinely independent in both
  directions.
- **A founder ruling this contradicts** — none found. `grep -rn 'XR-ANS' ~/.claude/DECISIONS.md`
  → no match; control, the same file returns hits for `DEC-` ids, so the absence is a reading.
  The relevant standing rule (*process-loop*: converge, do not merely alarm) is **satisfied** by this
  spec, not contradicted.
- **A capability that does not exist** — none. The generator, the allocator, the dedupe guard and the
  grader all exist and were executed this session.
- **A gate that would refuse it** — `~/.claude/hooks/pre-bash.sh` refuses shell commands whose text
  names `state/repo-intake-policy.tsv` next to a redirection (hit live this session on a
  `2>/dev/null`). Irrelevant to these files, but it means the repair actuator must be written with
  `Write`/`Edit`, not a heredoc, if its body quotes that path. Not a blocker.
- **The one genuine risk, stated rather than hidden:** the repair pass is a bulk write across 30
  repos' canonical ledgers. It is not reversible by a single `git revert` because each repo commits
  separately. Mitigation is in the build order: `--dry-run` first, estatehub alone second, the rest
  only after its diff is read.

**No BLOCKER is unanswered.**

## Questions

**None for him.** Everything here is a technical judgement inside the estate's own tooling, and the
receiving repo (`.claude`) owns every locus. The design choice that looks like it might be his —
whether to repair the 1,371 existing items or only stop minting new ones — is settled by the
standing rule he already locked (*"an alarm is not very useful because it's not done. I want it to be
done"*), which makes converging the backlog the required half rather than an option. The one
genuinely-his decision anywhere near this work, whether `The-Hawkers-Club/Amazon_SP_API` stays public,
belongs to the sibling spec and is already parked there as PRJ-001's Question 1; it is not re-asked
here.

## MVP

The shortest route to a true `Done when` is **steps 2 + 4 + 5 + 6** — stop the generator minting the
shape, then converge the backlog, estatehub first. Everything else is measurement and loop-closing.
A run that stops after step 2 leaves the estate strictly better (no new unreachable items are ever
written) but still 1,371 short of `Done when`, because the Done-when counts the world, not the
generator. A run that stops after step 5 has fixed 80% of the population in one repo and is safely
resumable, because the repair is idempotent by construction.

The MVP, named as rows:
- Change `xrepo-queue.py:714 queue()` so the answers population raises a real `OI-nnnn` row through `_ledger.with_allocated_oi` in the same locked transaction, and puts that id in the Item cell — because: while the generator still mints `XR-ANS-nnn`, the estate-wide count rises again after any repair, so `Done when` cannot hold even for one scheduled run.
- Build the idempotent repair actuator that retypes existing `XR-ANS-*` items and raises their companion rows, one locked transaction per repo — because: `Done when` counts the 1,371 items already on disk, and fixing the generator changes none of them.
- Run the repair on `estatehub` first and alone, commit, and read the diff — because: 1,096 of the 1,371 are there, so `Done when` is arithmetically unreachable without it, and it is the one write large enough to need reading before the rest follow.
- Run the repair across the remaining 29 affected repos, committing each by name — because: `Done when` is zero estate-wide, not zero in the worst repo; the remaining 275 items keep the count non-zero.

**Reaches the goal because:** `Done when` has two arms and this set closes both. Arm 2 — a fresh
`xrepo-queue.py` run appends an item whose Item cell names a row that exists — is exactly what step 2
changes, and `--selftest` measures it at the generator. Arm 1 — zero `INV-ORDER-001` findings naming
an `XR-ANS-*` id estate-wide — is a count over the 1,371 items now on disk, and steps 4-6 are the only
thing that moves that count; the measured population is fully partitioned by "estatehub" (1,096) and
"the other 29 repos" (275), so the two repair steps cover it with nothing left over. Steps 1, 3, 7 and
8 measure, guard and report; none of them changes either arm's value.

**Holds continuously because:** the count converges rather than being reset by hand. After step 2 the
generator can only write ids that name real rows, so the population cannot regrow — which is the
difference between this and a sweep that has to be re-run. Step 4's actuator is idempotent (a second
`--dry-run` after a real run reports 0), so a partial or interrupted repair is resumable without
double-raising rows, and `_ledger.with_allocated_oi` makes double-allocation unreachable by
construction rather than by care. Step 3's mutant test is the standing guard on the one thing that
must not drift: if a future edit stops `_answered_outbox_note` writing the literal `XR-OUT-nnn`,
`_outbox_id_referenced_in_any_order` goes blind and the whole population re-queues — that reddens a
test instead of silently rebuilding the backlog. Nothing here needs a human on a recurring basis; per
the standing rule, the repair is an actuator that finishes, not an alarm that reports.

## Build order

1. **Reproduce the count from the owning repo's own checkout** — run the third DoD arm from `~/.claude` and confirm 1,371 across 30 repos rather than trusting this document's figure. — gate: the script prints a non-zero `XR-ANS` count and the 8-item non-`XR-ANS` control is also non-zero, so the instrument is discriminating.
2. **Change `queue()` (`~/.claude/tools/xrepo-queue.py:714`) so the answers population raises its companion row inside the same locked transaction** — via `_ledger.with_allocated_oi`, into the receiving repo's `PRJ-000` Unfiled table, with the row text naming the answer file and the Item cell holding that new `OI-nnnn`; `answer_order_id` stays as the fallback for a repo whose Unfiled table cannot be found, so an unusual ledger degrades to today's behaviour rather than crashing. — gate: `python3 ~/.claude/tools/xrepo-queue.py --selftest` exits 0 with its `XR-ANS-100`/`XR-ANS-200` fixtures updated to assert the new shape.
3. **Leave `_answered_outbox_note` and `_outbox_id_referenced_in_any_order` untouched**, and add a selftest case that fails if the `XR-OUT-nnn` prose stops being written. — gate: a mutant that deletes the `XR-OUT` id from the note reddens at least one selftest assertion, and the unmutated control stays green.
4. **Write the repair actuator** — walks the registry and, for each `XR-ANS-nnn` item whose `XR-OUT-nnn` row it can locate in the same ledger, raises the companion row and retypes the Item cell, one `with_allocated_oi` transaction per repo; idempotent, and a ledger it cannot parse escalates rather than retrying. — gate: `--dry-run` on a temp copy of `estatehub`'s ledger reports 1,096 planned changes and writes nothing, and a second `--dry-run` after a real run reports 0.
5. **Run the repair on `estatehub` alone**, commit, and read the diff before touching anything else. — gate: `estate-conformance --check --only INV-ORDER --repo <estatehub>` drops from 1,096 `XR-ANS` findings to 0 while its build order still lists the same number of items.
6. **Run it across the remaining 29 repos**, committing each by name and never with `git add -A`. — gate: the DoD script's estate-wide count reads `0`.
7. **Run the full three-arm DoD check**, writing the exit code into the log with `echo "EXIT=$?" >> …` and reading the log rather than the notification. — gate: `/tmp/xrans-dod.log` ends `EXIT=0`.
8. **Answer the originating filing** through `xrepo-relay.py answer`, naming the commits and the before/after counts. — gate: the answer row lands terminal on the sending repo's ledger and its Answer cell names a file that exists.

## Items

- Measure the baseline from `.claude`'s own checkout — `XR-ANS` unreachable items estate-wide, plus the non-`XR-ANS` control — and record both numbers before changing anything.
- Change `xrepo-queue.py:714 queue()` so the answers population raises a real `OI-nnnn` row through `_ledger.with_allocated_oi` in the same locked transaction, and puts that id in the Item cell.
- Keep `answer_order_id` as the degradation path for a ledger whose Unfiled table cannot be located, so an unusual ledger falls back to today's behaviour instead of failing the queue.
- Add a selftest that reddens if `_answered_outbox_note` stops writing the literal `XR-OUT-nnn` id, since `_outbox_id_referenced_in_any_order` is the only remaining dedupe link.
- Update the existing `XR-ANS-100` / `XR-ANS-200` selftest fixtures at `xrepo-queue.py:1226-1318` to assert the new Item-cell shape, in the same commit as the behaviour change.
- Build the idempotent repair actuator that retypes existing `XR-ANS-*` items and raises their companion rows, one locked transaction per repo, escalating on any ledger it cannot parse rather than retrying it.
- Run the repair on `estatehub` first and alone (1,096 items), commit, and read the diff before proceeding.
- Run the repair across the remaining 29 affected repos, committing each by name.
- Run the three-arm DoD check, capturing the exit code into the log rather than reading a wrapper's status.
- Answer the originating cross-repo filing with the commits and the before/after counts.
