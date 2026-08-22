# 3 conformance finding(s) in your tree — INV-LEDGER-005; INV-PAGE-001; INV-SPEC-001

- **Request id:** `XR-IN-1000014`
- **From repo:** `estatehub`
- **To repo:** `AMZN API/Amazon_SP_API`
- **Filed:** 2026-08-22T03:52:49Z
- **Instruction key:** `a1ee25cc3d9d`
- **Originating rows:** —

> Filed by `xrepo-relay.py` under RULE-L24: cross-repo work is filed as an instruction, never handed back as a question.
> **When you have executed this, run:** `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000014 --body-file <what-you-did.md>`
> That writes the answer into `estatehub` and lands a row on ITS ledger. The loop is not closed until the answer exists on the other side.

---

# 3 conformance finding(s) in `AMZN API/Amazon_SP_API` — measured from this machine, filed so they are yours to clear rather than ours to watch

**From:** estatehub · **Filed:** 2026-08-22T03:52:49Z · **Fingerprint:** `bbd67ae44800`

## 1. What we need

Clear the findings below in `AMZN API/Amazon_SP_API`, or refute any you disagree with. A refutation closes the loop just as well as a repair — what does not close it is silence, because the estate-wide check stays red and nobody can tell a disputed finding from an unread one.

## 2. Why it must come from your side

Every one of these is a defect in YOUR tree — your ledger's own columns, your specs, your dumps. We can measure them from here and we cannot fix them from here: editing another repo's working tree is the one thing this estate's rules do not authorise. So the measurement travels and the repair stays with the owner.

## 3. The measured findings

### `INV-SPEC-001` — 1 spec(s) with 10 open task(s) referenced in no ledger row

```
PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md
```

### `INV-LEDGER-005` — `PROJECT-LEDGER.md` resolves `merge=union` HERE ONLY — `.gitattributes` exists and is UNTRACKED, so it is on no branch, so every clone, every stream worktree and every other machine still merges the register with the default driver

```
A green `git check-attr` is fully consistent with this: it reports the attribute as resolved on THIS disk and cannot see whether the file that resolved it is on a branch. MEASURED in `~/.claude` 2026-08-19, where `.gitignore` line 3 is a bare `*` and swallowed the `.gitattributes` the repair had just written. Repair appends `!.gitattributes` to `.gitignore` where an ignore rule is the cause; committing the file is the repo's own cycle to do, which is why this leg REPORTS and does not gate
```

### `INV-PAGE-001` — the `**Page:**` header names no url at all

```
**Page:** (set on first publish)
```

## 4. Reproduce it yourself, exactly

```bash
python3 ~/.claude/tools/estate-conformance.py --check --repo "AMZN API/Amazon_SP_API" --json
```

**Two properties of that tool you need, both of which have cost this estate a debug cycle each:** it has **no argparse at all**, so an unrecognised flag (`--only …`) is accepted and **silently ignored** rather than rejected; and `--repo` is a **SUBSTRING** match, so the quotes above are load-bearing — unquoted, `--repo AMZN Analytics` selects **5** repos and prints other people's findings as if they were yours.

## 5. You are not alone in this, and that is a fact about the estate

- `INV-LEDGER-005` is open in **41** repos (78% of those failing): AMZN API, AMZN API/Amazon_Ads_API, AMZN API/Amazon_SP_API, AMZN API/selling-partner-api-models, AMZN Analytics, AMZN-Competitor, AMZN-shared, Amazon, Anthropic-Watch, Backup, Bellwether, CIO-PO Analytics, Forecasting Gap Analytics, Freight Forwarders, GCS-THC, GroundIQ, Home Depot, Invoicing, KeepIQ, Legal, Marketing System, Marketing System/leadgen, NAL PROJECT, PresenterIQ, RITE-Chewy, Recovery-Site, Sales Report, Slate, THC, THC/backend, THC/bots, THC/browser-extension, THC/trigger, Telemetry Hub, TimeOffIQ, TimeOffIQ-repo, TimeOffIQ-repo-backup, Walmart, autoblog-v3, clientmindIQ, flightclaimiq. It is being filed per-repo because each ledger is repaired by its owner, but if you find a shared root cause it is worth telling us — one answer would close several rows.

## 6. What we do the moment you deliver

Nothing is asked of us. This loop re-measures every cycle from your tree, so a repair closes it here automatically — you do not need to tell us. If you answer and the findings are still present, this loop deliberately **will not re-file**; it escalates instead, because re-sending an identical instruction is a re-run, not a remedy.

## 7. If you cannot or will not do this

Answer with that and say why. A refusal is a valid answer and closes both sides. What we ask you not to do is leave it silent — the estate-wide conformance gate is red until every repo's findings are either cleared or disputed, and three projects in estatehub are held PARTIAL by exactly that gate.

<!-- conformance-fanout fingerprint: bbd67ae44800 -->
