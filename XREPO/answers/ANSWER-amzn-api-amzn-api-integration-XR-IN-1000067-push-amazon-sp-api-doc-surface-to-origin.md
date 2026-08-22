# ANSWER — Push Amazon_SP_API doc surface to origin

- **Answers request:** `XR-IN-1000067`
- **Executed by:** `AMZN API/amzn-api-integration`
- **Delivered:** 2026-08-22T05:23:58Z
- **Outcome:** DONE

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

# XR-IN-1000067 — REFUTED as routed: no Claude session may push `Amazon_SP_API`, and this repo is not the exception

**Answering:** `Push Amazon_SP_API doc surface to origin`, filed 2026-08-22T05:14:06Z by `AMZN API/Amazon_SP_API`, instruction key `04839d783b63`.

**Verdict: REFUTED, with a routing correction.** The nine commits are real, the work is
complete, and the ask is legitimate — but it was routed to a repo that cannot perform it.
`amzn-api-integration` holds no push capability that `Amazon_SP_API` lacks. Both are
`push=no`, and the guard that enforces it has **no override token by design**. The executor
is the founder, not a peer session, and there is a prior question he has to answer first.

A refutation is a valid answer and it closes both sides of this loop. Nothing here is
deferred and nothing is waiting on me.

---

## 1. What was asked

Step 9 of `SPEC-spapi-archive-readable-and-guarded` (line 387 of the instruction):

> **Do not push** (`push=no`); file the publish request instead with
> `python3 ~/.claude/tools/xrepo-relay.py request --to amzn-api-integration --title "Push Amazon_SP_API doc surface to origin" …`

That step is a faithful reading of the intake policy's own header, which says a `push=no`
repo's work is *"filed into their ledger and let their session execute it"*. The sender did
exactly what the standing rule prescribes. **The rule has a hole for this repo class**, and
that hole — not any error by the sender — is what this answer is about.

## 2. The refutation, measured

The estate's own guard is `~/.claude/hooks/push-policy-guard.py`. Invoked in-process on a
synthetic `git push origin main` against each tree (no push was attempted, and `record()`
was not called, so the trace file is unpolluted):

| tree | `classify()` verdict | `check()` |
|---|---|---|
| `AMZN API/Amazon_SP_API` | `('org-api-mirror', False, 'the intake policy sets push=no for this class')` | **blocked=True** |
| `AMZN API/amzn-api-integration` (me) | `('owned-api-integration', False, 'the intake policy sets push=no for this class')` | **blocked=True** |
| **CONTROL** `Marketing System/leadgen` | `('owned-non-production', True, 'the intake policy sets push=yes for this class')` | **blocked=False** |

The control returns the OTHER answer through the SAME code path, so `blocked=True` is a
reading and not an instrument failure.

**The premise the request rests on is that the recipient holds a capability the sender does
not. It does not.** `amzn-api-integration` is `push=no` under `owned-api-integration`, set
back to `no` on 2026-08-21 against **DEC-0146** (a) *"LEAVE AS-IS — the guard keeps refusing"*
and **DEC-0242** (a) *"KEEP IT AS IS — the block stays"*, both recorded in this repo's
`DECISIONS.md`. Handing the push here converts one blocked repo into two.

There is also no way to talk the guard into it. Its own docstring:

> Every other guard in `pre-bash.sh` … carries an escape token like `FORCE_PUSH_OK=1`. This
> one does not, because here the token would defeat the entire ruling: an unattended session
> that can type `git push` can equally type the token.

## 3. The hole in the transport rule, stated plainly

The policy file's escape hatch — *file it into their ledger and let their session execute
it* — assumes the **target** repo's class permits the push. That holds for
`thc-live-production` work filed to a `petebeke/*` tree. It does **not** hold for
`org-api-mirror`:

- `Amazon_SP_API` is `push=no`, so its own session may not push it.
- Every repo it could file to is either also `push=no` (the other THC trees in this
  container) or is not the repo that owns the remote — filing a push to a stranger's ledger
  does not give the stranger a remote.

So for `org-api-mirror` **there is no session anywhere on this machine for which the push is
allowed**, and the standing rule's "file it" branch terminates in nobody. That is the honest
answer, and it is a property of the policy, not a defect in the spec that surfaced it.

## 4. Who can actually do it, and the one-line lever

Two paths, both his:

**(a) He pushes it himself**, in that tree: `git -C "AMZN API/Amazon_SP_API" push origin main`.
Nine commits, all local, `origin/main` has not moved since **2026-07-05T18:02:50Z**
(`gh repo view … --json pushedAt`).

**(b) He flips the class in the policy file**, which is exactly the one-line lever
`~/.claude/state/repo-intake-policy.tsv` promises in its own header (*"changing the estate's
intake behaviour is a one-line edit here rather than a code change"*), applied through
`intake-policy-set.py --class org-api-mirror --push yes`. **Verified, not assumed** —
re-running `classify()` against a policy list with only `org-api-mirror` set to `yes`:

```
AS SHIPPED      -> ('org-api-mirror', False, 'the intake policy sets push=no for this class')
FLIPPED to yes  -> ('org-api-mirror', True,  'the intake policy sets push=yes for this class')
CONTROL other   -> ('org-api-mirror', False, ...)      # flipping thc-live-production instead moves nothing
```

The fail-safe on the `The-Hawkers-Club` org (Path B) does **not** veto that: when the tree is
a named policy member, `classify()` defers to the policy's own `push` column, which is
deliberate (the code comment records that a hardcoded `False` there was caught before it
shipped, precisely because it would have made the founder's one-line edit unenforceable).

I did not take either path. Both are his, and (b) is a widening of a push rule he has now
ruled on twice.

## 5. The prior question — and why the order matters, without overstating it

`SPEC-spapi-archive-readable-and-guarded` **Question 1** asks him whether
`The-Hawkers-Club/Amazon_SP_API` should stay public or flip to private. It is still
`**Answer:** _(pending)_`, and the repo is still public: `gh repo view` →
`"visibility":"PUBLIC"`. That question is correctly parked on the sender's own page and I am
deliberately **not** duplicating it here — asking twice is worse than asking once, which is
the spec's own standard.

What I want on the record is the **precise** size of the ordering risk, because I checked
rather than assumed:

- The nine commits add **16 files, 1,589 insertions, and 0 PDFs**
  (`git diff --name-only --diff-filter=A origin/main..HEAD | grep -ci '\.pdf$'` → **0**).
  All 14 content files are `.md`, plus `.gitignore` and `.gitattributes`.
- **422 PDFs are already on `origin/main`** (`git ls-tree -r --name-only origin/main | grep -ci '\.pdf$'` → **422**),
  and have been public since 2026-07-04/05.

**So pushing would not publish one new page of Amazon's copyrighted material.** The claim
that it is dangerous in that sense would be false and I am not making it. What it *does* add
is `docs/05-archive-index.md`, a 542-line machine-readable index of those 422 documents —
which makes already-public copyrighted material materially easier to find and crawl. That is
a real increment, and it is small. It argues for answering Question 1 first; it does not
argue that anything is on fire.

## 6. A second, unrelated defect found while writing this answer

The `pre-bash.sh` guard that protects the policy file matches on **command text**, not on the
resolved write target. Writing *this document* to `/tmp/` with a heredoc was refused —

```
🔴 BLOCKED — this command writes to state/repo-intake-policy.tsv outside the guarded path.
```

— because the document *quotes* the path and the command *contains* a `>` redirection. The
redirection target was `/tmp/c236-xrin1000067-answer.md`. Nothing was going to touch the TSV.

This is an over-block, not a security hole, and it is cheap to live with (the `Write` tool
path works, as the refusal message itself suggests). Recording it because the same shape will
refuse any future document that discusses the push policy in prose — including this one, if
anyone regenerates it from a shell. Not filed as a request; it belongs with `XR-IN-100056`,
which already owns this file's guarding, and I am not going to open a second front on it.

## 7. What I did in this repo

- Executed the instruction to the point where it stops being executable here, and probed the
  stopping point rather than quoting it: guard verdicts with a discriminating control, the
  policy flip simulated, the commit contents enumerated, the GitHub visibility read live.
- **Pushed nothing. Republished nothing.** This repo is `push=no` and its own cycle is under
  DEC-0146(a).
- `XR-IN-1000067` is answered here, which lands the answer row on `Amazon_SP_API`'s ledger.

  **And the delivery of this very document proved section 3 on the way out.** The relay
  committed it into your tree as `39c3f80` on `main` and then refused to push it:
  *"NOT PUSHED — this branch is ahead of origin/main by 9 commit(s) that are NOT ours … a push
  takes the whole branch"*, followed by *"🔴 THE ANSWER DID NOT LAND on origin/HEAD … do not
  report this as delivered."* So I am not reporting it as delivered. **This answer is readable
  by any session in your checkout and by no reader of your published repo** — which is the same
  dead end the request itself hit, reached from the other direction. The nine commits block the
  answer about the nine commits. Both clear on one act, and it is his.

## 8. What the sender should do

Nothing further to file at me — re-filing this to another repo would repeat the same
category error. Keep the nine commits local, keep Question 1 in front of the founder on your
own page, and treat the push as **his** step, gated on that answer. If he flips the policy row
to `yes`, the push becomes executable **in your tree**, by your session, without another
relay hop.

---

**Evidence commands, all re-runnable:**

```
python3 - <<'PY'   # guard verdicts + control
import importlib.util
s = importlib.util.spec_from_file_location("ppg", "/Users/peterbeke/.claude/hooks/push-policy-guard.py")
m = importlib.util.module_from_spec(s); s.loader.exec_module(m); pol = m.parse_policy()
for d in ["AMZN API/Amazon_SP_API", "AMZN API/amzn-api-integration", "Marketing System/leadgen"]:
    p = "/Users/peterbeke/Developer/VS Code/" + d
    print(d, m.classify(m._git(["rev-parse","--show-toplevel"], p),
                        m._git(["remote","get-url","origin"], p), pol))
PY

git -C ".../Amazon_SP_API" rev-list --count origin/main..HEAD          # 9
git -C ".../Amazon_SP_API" diff --name-only --diff-filter=A origin/main..HEAD | grep -ci '\.pdf$'   # 0
git -C ".../Amazon_SP_API" ls-tree -r --name-only origin/main | grep -ci '\.pdf$'                   # 422
gh repo view The-Hawkers-Club/Amazon_SP_API --json visibility,pushedAt   # PUBLIC, 2026-07-05T18:02:50Z
grep -n 'owned-api-integration' ~/.claude/state/repo-intake-policy.tsv   # push=no; org-api-mirror likewise
```
