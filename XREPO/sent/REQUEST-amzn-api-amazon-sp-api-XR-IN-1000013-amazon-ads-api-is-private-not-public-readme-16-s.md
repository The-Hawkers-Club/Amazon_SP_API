# Amazon_Ads_API is PRIVATE, not public — README:16 / START-HERE:26 are wrong, and this closes the UNVERIFIED visibility BLOCKER in your SPEC-doc-archive-truth

- **Request id:** `XR-IN-1000013`
- **From repo:** `AMZN API/Amazon_SP_API`
- **To repo:** `AMZN API/Amazon_Ads_API`
- **Filed:** 2026-08-21T07:49:11Z
- **Instruction key:** `5d45c50d24b4`
- **Originating rows:** —

> Filed by `xrepo-relay.py` under RULE-L24: cross-repo work is filed as an instruction, never handed back as a question.
> **When you have executed this, run:** `python3 ~/.claude/tools/xrepo-relay.py answer --id XR-IN-1000013 --body-file <what-you-did.md>`
> That writes the answer into `AMZN API/Amazon_SP_API` and lands a row on ITS ledger. The loop is not closed until the answer exists on the other side.

---

# Amazon_Ads_API is PRIVATE, not public — your README, START-HERE and your own spec's open BLOCKER all say otherwise

**From:** `AMZN API/Amazon_SP_API` planning pass, 2026-08-21
**Type:** factual correction + one open BLOCKER in your repo that this closes

## What is wrong

Two files instruct the team on the basis of a visibility claim that is false:

- `README.md:16` — *"This repo is **public**. Never commit the Client Secret, any access/refresh token, or any client data."*
- `START-HERE.md:26` — *"This repository is **public**."*

`The-Hawkers-Club/Amazon_Ads_API` is **private**.

## The probe

`gh` is not installed on this machine, which is why your own
`PLAN/specs/SPEC-doc-archive-truth.md` records this as an unanswered **BLOCKER**
(*"`gh` is not installed, so this repo's GitHub visibility is UNVERIFIED"*) and re-raises it as
Question 3. GitHub's public REST API needs neither `gh` nor authentication:

```
curl -s -o /dev/null -w "%{http_code}\n" https://api.github.com/repos/The-Hawkers-Club/Amazon_Ads_API
  -> 404      (private, or nonexistent)

curl -s -o /dev/null -w "%{http_code}\n" https://api.github.com/repos/The-Hawkers-Club/amzn-api-integration
  -> 404      (private)

curl -s -o /dev/null -w "%{http_code}\n" https://api.github.com/repos/The-Hawkers-Club/Amazon_SP_API
  -> 200      (public)
```

Positive control that 404 means "not visible to an anonymous caller" rather than "the endpoint is
broken": the third call, same host, same shape, returns **200** with a body containing
`"private": false`. A 404 on an org repo you can push to is GitHub's documented behaviour for a
private repo read anonymously, so the pair is decisive.

## Why it matters, and why it is not merely cosmetic

The claim is load-bearing in the direction that makes being wrong *safe*, not dangerous — the repo is
more locked down than the docs say, not less — so this is not urgent. But it is worth fixing for two
reasons:

1. **A security notice that is wrong about its own premise trains people to discount it.** The
   instruction that follows it (never commit the Client Secret or a token) is correct and should
   stand on its own footing, not on a false "because this repo is public".
2. **It closes a real BLOCKER on your board.** `PLAN/specs/SPEC-doc-archive-truth.md` is held with
   that blocker unanswered and Question 3 pending on the founder for the same fact. The visibility
   half of Question 3 is now answered and needs no founder time; the Client-Secret-rotation half is
   genuinely his and stays parked.

Note the near-collision that makes this easy to get wrong: `amzn-api-integration/DECISIONS.md:1860`
records the app model as **"public-unlisted"** — that is the Amazon *application*, not the GitHub
*repository*. Different sense of "public".

## Asked of you

1. Correct `README.md:16` and `START-HERE.md:26` to state that the repo is private, keeping the
   never-commit-a-secret instruction on its own merits.
2. Close the visibility arm of the **BLOCKER** and of **Question 3** in
   `PLAN/specs/SPEC-doc-archive-truth.md`, citing the `curl` probe above rather than `gh`.
3. Keep the Client Secret rotation half of Question 3 parked — it is outside this machine and is his.

## Related, filed separately

The sibling `Amazon_SP_API` is genuinely **public** and its `README.md:15` claims the opposite
("internal reference"). That is parked for the founder as `AMZN API` **OI-0025** (stay public vs flip
to private, with costs), and is not part of this ask.
