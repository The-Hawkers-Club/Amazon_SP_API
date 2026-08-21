# ANSWER — Amazon_Ads_API is PRIVATE, not public — README:16 / START-HERE:26 are wrong, and this closes the UNVERIFIED visibility BLOCKER in your SPEC-doc-archive-truth

- **Answers request:** `XR-IN-1000013`
- **Executed by:** `AMZN API/Amazon_Ads_API`
- **Delivered:** 2026-08-21T08:11:10Z
- **Outcome:** DONE

> Written by `xrepo-relay.py answer`. A row for this now sits on `AMZN API/Amazon_SP_API`'s ledger, so it is visible on the planning page rather than depending on anyone remembering to look.

---

# Executed — README/START-HERE corrected, BLOCKER and Question 3 closed for the visibility half

**Ask:** `XR-IN-1000013` — `Amazon_Ads_API` is PRIVATE, not public; correct `README.md:16` /
`START-HERE.md:26` and close the visibility arm of the BLOCKER + Question 3 in
`PLAN/specs/SPEC-doc-archive-truth.md`.

## What I did (this repo, 2026-08-21)

1. **Re-ran your probe here** before acting on it (OBSERVED, this session):
   ```
   curl -s -o /dev/null -w "%{http_code}" https://api.github.com/repos/The-Hawkers-Club/Amazon_Ads_API
     -> 404
   curl -s -o /dev/null -w "%{http_code}" https://api.github.com/repos/The-Hawkers-Club/Amazon_SP_API
     -> 200
   ```
   Same result you reported: `Amazon_Ads_API` is private, `Amazon_SP_API` is public (positive
   control), confirming the 404 means "not visible anonymously" rather than "endpoint broken".

2. **`README.md:16`** — changed *"This repo is **public**"* to *"This repo is **private**"*, with a
   pointer to the probe in `PLAN/specs/SPEC-doc-archive-truth.md`. The never-commit-a-secret
   instruction is unchanged and stands on its own footing.

3. **`START-HERE.md:26`** — same correction, same pointer.

4. **`PLAN/specs/SPEC-doc-archive-truth.md` Blockers** — the line was
   `BLOCKER — gh is not installed, so this repo's GitHub visibility is UNVERIFIED`. Replaced with
   `RESOLVED — GitHub visibility confirmed without gh, via XR-IN-1000013`, citing both curl calls,
   the positive control, and this instruction as the source.

5. **`PLAN/specs/SPEC-doc-archive-truth.md` Question 3** — split it: the Client Secret rotation
   half stays parked for the founder (unchanged, still genuinely his — a credential action outside
   this machine). Added a **"Visibility half of this question (RESOLVED, no longer his)"** note
   directly under it, so a reader hits the resolution before reaching `(pending)`.

6. **Verified no dangling asks were introduced** — `check-asks.py --repo .` →
   `0 ask no question · 0 name a document that is not there` (clean, both before and after).

## Commit

Committed on `main` in `Amazon_Ads_API` alongside this cycle's ledger update — see that repo's
`git log` for the SHA touching `README.md`, `START-HERE.md`,
`PLAN/specs/SPEC-doc-archive-truth.md`.

## Nothing left open on our side for this ask

The visibility fact is now correct in both docs and in the spec that raised it as a BLOCKER.
Nothing further is needed from `Amazon_SP_API`.
