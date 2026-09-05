# SPEC-spapi-archive-readable-and-guarded — the 422-PDF archive becomes machine-readable, coverage-mapped and citation-guarded, and the repo stops describing itself falsely

**Source:** PLAN/dumps/202608210128-estate-intake-onboarding.md
**Status:** ADOPTED — became PRJ-001 on 2026-09-05
**As of:** 2026-08-21

## Goal

This repo is the offline documentation base a **live** SP-API integration cites by filename, and today
neither half of that sentence is visible from inside it. The outcome: the 422 PDFs become searchable
text on this machine rather than 170 MB of opaque binaries no tool here can open; the archive's
coverage of the API versions production actually calls is a file you read instead of a grep that
silently returns zero; the 41 exact filename citations a sibling repo hangs its adopted decisions on
are guarded by a loop that converges when they drift; and a teammate opening the repo learns the real
role posture (which surfaces return 200, which return 403 and why) instead of a fifteen-line README
that says the archive is "internal" while GitHub serves it to the world.

The integration is **not** built here and this spec does not move it. `The-Hawkers-Club/amzn-api-integration`
holds it, `src/spapi/` and `src/spine/` are its loci, and this repo's job is to be the reference that
repo already treats as authoritative.

## Done when

`AMZN API/.claude/spapi-index/` holds one extracted-text sidecar and one manifest row for every one of
the 422 PDFs; `docs/05-archive-index.md` lists every PDF on disk with its capture date; a coverage
report names, for each of the 19 SP-API family/version prefixes production calls, whether this archive
documents it; the citation guard reports every `*.pdf` filename cited by `../amzn-api-integration`
as resolving, or converges it; and `README.md` plus a new `START-HERE.md` and `docs/01–04` describe
what is actually true — including this repo's real GitHub visibility.

## DoD check

```sh
set -u
cd "/Users/peterbeke/Developer/VS Code/AMZN API/Amazon_SP_API" || exit 1
G="/Users/peterbeke/Developer/VS Code/AMZN API/.claude/checks/spapi_doc_guard.py"
python3 "$G" --selftest \
&& python3 "$G" verify \
&& test -f START-HERE.md && test -f docs/03-status.md && test -f docs/05-archive-index.md \
&& grep -q 'amzn-api-integration' docs/03-status.md \
&& ! grep -q 'internal reference by The Hawker' README.md \
&& python3 -c "import os,sys; idx=open('docs/05-archive-index.md').read(); sys.exit(1 if [f for f in os.listdir('.') if f.endswith('.pdf') and f not in idx] else 0)"
```

OBSERVED 2026-08-21: this exact block was written to `/tmp/spapi-dod.sh` and run —
`bash /tmp/spapi-dod.sh > /tmp/spapi-dod.log 2>&1; echo "EXIT=$?" >> /tmp/spapi-dod.log` → **`EXIT=2`**
(the exit code is written to the log by the shell, not read from a wrapper's status). Every arm was
also failed individually today: `test -f START-HERE.md` → NO, `test -f docs/03-status.md` → NO,
`test -f docs/05-archive-index.md` → NO, `grep -q 'internal reference by The Hawker' README.md` →
still present. Positive control that the arms are satisfiable rather than impossible: the same two
`test -f` arms run against the sibling `../Amazon_Ads_API` → both PRESENT.

`--selftest` is not redundant with `verify`. `verify` proves the guard agrees with **this** archive;
`--selftest` proves the guard can still *see* a fault, by planting one on a temp copy (a renamed PDF,
a sidecar whose sha256 no longer matches its source, a citation pointed at a file that does not exist)
and requiring a non-zero exit on each — the defect being that a checker which repairs or silently
skips what it is looking for reports green forever (`AMZN API/.claude/checks/page_link_guard.py:30-40`
records that exact failure happening on this estate).

## Fits

Docs-only repo: 424 tracked files, of which **422 are PDFs and 2 are markdown/config**
(`git ls-files | grep -v '\.pdf$'` → `.gitignore`, `README.md` — nothing else). No source tree, no
package manifest, no test runner, no `.github`. So the in-repo loci are markdown lines, and the
executable loci live in the container's existing check directory rather than in this repo — which is
also what `push=no` requires (see **Conflicts**).

In this repo:
- `README.md:1` — `# Amazon SP-API — Solution Provider Documentation Archive`. Stays; gains a
  START-HERE pointer, matching the sibling's `../Amazon_Ads_API/README.md:6`.
- `README.md:5` — the single asserted coverage bullet ("422 documentation pages … covering the full
  SP-API surface"). Repointed at the enumerated index; "the full SP-API surface" is an absence-shaped
  claim this repo cannot currently substantiate about itself.
- `README.md:15` — "retained here for internal reference by The Hawker's Club team." **This is false as
  written**: `curl -s https://api.github.com/repos/The-Hawkers-Club/Amazon_SP_API` (unauthenticated)
  returns HTTP **200** with `"private": false`. Rewritten to state the actual visibility.
- `.gitignore:4-5` — `_THC-*.md`, "keep OUT of the public docs repo". Extended to exclude the derived
  text sidecars if they are ever produced inside the tree by mistake.
- `PLAN/specs/` — created by this pass; this file is its first occupant.
- `PROJECT-LEDGER.md:1-30` — installed 2026-08-21 by `oil-install.py` at OIL v5.5.0, `Next IDs: PRJ-001 ·
  OI-0001`, only the standing `PRJ-000 — Unfiled`. This spec's **Items** become its first real rows.
- new, and deliberately written here **without** backticked paths because they do not exist yet:
  START-HERE, plus docs/01-getting-started, docs/02-playbook, docs/03-status,
  docs/04-incident-response-plan and docs/05-archive-index (all `.md`). They are named as runnable
  paths in the **DoD check** and created in Build order steps 3, 6 and 7 — a spec that cites a file it
  is about to create as if it already existed is the exact claim this section is probed for.

In the container (`/Users/peterbeke/Developer/VS Code/AMZN API/`), following the pattern already
running there:
- `spapi_doc_guard` — new `.py` under `../.claude/checks/`. The `index` / `verify` / `converge` /
  `--selftest` verbs. Named without a path here because it does not exist yet; it is named as a
  runnable path in the **DoD check**.
- `mutants_spapi_doc_guard` — new `.py` in the same directory, mirroring
  `../.claude/checks/mutants_sync.py` and `../.claude/checks/mutants_plist_readable.py`, which exist
  and establish the convention.
- `.claude/checks/com.thc.amzn-api-doc-citations.plist` — new, staged beside the four plists already
  in that directory (`com.thc.amzn-api-page-links.plist`, `…-row-baseline.plist`, `…-ledger-grade.plist`,
  `…-xr-page-truth.plist`) and symmetric with them: `gtimeout 3600` → `/usr/bin/python3 -u <check> converge`,
  `StartInterval 3600`, `WorkingDirectory` = the container, log under `~/.claude/state/`.
- `../.claude/spapi-index/` — new. A manifest (JSON) plus `text/<name>.txt`, one per PDF. Extracted Amazon
  body text lives **here, outside the world-readable repo**, not in it.

Entry point production takes: `~/Library/LaunchAgents/com.thc.amzn-api-doc-citations.plist`, loaded
alongside the five `com.thc.amzn-api-*` agents already registered there (`ls ~/Library/LaunchAgents |
grep -c 'com.thc.amzn-api'` → **5**; `launchctl list | grep amzn-api-page-links` → registered, last
exit 124).

## Wiring

This repo has no runtime, so "who calls this" has two real answers, both enumerated rather than assumed.

**1 — the guard is called by launchd, not by a human.**
producer: `AMZN API/.claude/checks/spapi_doc_guard.py` (`converge`) → consumer:
`~/Library/LaunchAgents/com.thc.amzn-api-doc-citations.plist`, hourly. This is the arm that stops the
work being a spec-shaped file nobody runs. The precedent is live, not hypothetical:
`launchctl list | grep -i 'thc.*amzn-api'` → `com.thc.amzn-api-page-links` present with a recorded exit
status, and its plist runs `AMZN API/.claude/checks/page_link_guard.py converge` from
`WorkingDirectory = /Users/peterbeke/Developer/VS Code/AMZN API`.

**2 — the PDFs are called by a sibling repo, by exact filename.**
producer: the root PDFs → consumers:
- `../amzn-api-integration/DECISIONS.md:1862` — *"Verified against `Authorization Limits.pdf`"*, the
  evidence line under the **adopted** public-unlisted app-model decision.
- `../amzn-api-integration/specs/full-access/01-spapi-read-surfaces.md:9,64` — cites `../Amazon_SP_API/`
  as a source and `Access Orders PII.pdf` by name.
- `../amzn-api-integration/specs/full-access/02-spapi-restricted-analytics-notifications.md:28,55` —
  *"SP-API PDFs (`../Amazon_SP_API/`): named inline per section"*, then `Tokens API.pdf`,
  `Authorization with the Restricted Data Token.pdf`.
- `../amzn-api-integration/specs/amzn-ingestion/requirements.md:6` and `tasks.md:11` — both name the
  archive as a source spec.
- `../amzn-api-integration/README.md:21` — "422 PDFs, full SP-API surface".
- `../amzn-api-integration/ledger/items/OI-0020.md`, `OI-0042.md` — ledger rows whose evidence column
  is a `.pdf` filename.

Enumerated with
`grep -rl "Amazon_SP_API" --include='*.md' --include='*.py' --include='*.ts' --include='*.json' --include='*.tsv' --include='*.sh' "/Users/peterbeke/Developer/VS Code" | grep -v node_modules | grep -v '/AMZN API/Amazon_SP_API/'`
→ **30 files** across `AMZN API/`, `amzn-api-integration/`, `estatehub/` and `THC-scrapers/`.
Positive control: the identical sweep for `Amazon_Ads_API` → **48 files** (so the pattern finds things),
and for a nonsense token → 0.

The citation set was then resolved, because "they cite it" is worth nothing if the citations are
already broken. Measured today across `amzn-api-integration` (`*.md`/`*.json`, excluding
`node_modules`/`dist`): **70 distinct backticked `*.pdf` tokens — 56 resolve exactly against a file in
this archive or the Ads archive, 12 resolve by suffix (the Ads archive embeds `:` path segments in
filenames), 2 are globs, and 0 dangle.** My first pass reported 16 "missing"; refining the matcher to
allow the suffix form reduced that to 0, so the honest statement is that **the citation set is intact
today** and this loop preserves a good invariant rather than repairing a broken one.

The defect this catches is the docs analogue of inert code: an archive nobody can read, guarding
citations nobody checks, under a README that describes a different repo than the one GitHub serves.

## Conflicts

- **rules:** `grep -n -iE "org-api-mirror|doc archive|documentation archive|Amazon_SP_API" ~/.claude/commands/CLAUDE.md`
  → **no hits** (exit 1); positive control `grep -c -i "parallel" ~/.claude/commands/CLAUDE.md` → **6**,
  so the file was really read. The governing rule is not in the commands file but in
  `~/.claude/state/repo-intake-policy.tsv`, which classes this tree **`org-api-mirror`** with
  `onboard=yes  clone=no  **push=no**`, alongside `Amazon_Ads_API`. Its header records the standing
  founder rule verbatim: *"do not push to the THC live repos — file the request into their ledger and
  let their session execute it"*, and *"A repo with push=no still gets planned, still gets a page, and
  still gets work."* **This spec obeys that literally: it builds, it commits locally, it never runs
  `git push`, and publication to `origin` is a filed request, not a step.**
- **live rows (this repo):** `python3 ~/.claude/tools/ledger-read.py --repo . --open --limit 10` →
  `no matching row`. Nothing to collide with.
- **live rows (container):** `python3 ~/.claude/tools/ledger-read.py --repo "AMZN API" --item OI-0003`
  → **OPEN, 👤 PARKED 2026-08-13** — *"This 'AMZN API' folder is not a git repo — it is a container
  holding four real repos … Do you want it to stay a container …"*. That question is about the
  **container's** identity and page, not about this repo's contents. This spec neither answers nor
  duplicates it, and nothing here changes under any of its three arms: every artifact this spec
  creates lands either inside `Amazon_SP_API/` or inside the container's already-existing
  `.claude/checks/` tree, both of which survive a STAY/PROMOTE/DEMOTE ruling unchanged.
- **sibling spec — the real collision risk, and it is close:**
  `AMZN API/Amazon_Ads_API/PLAN/specs/SPEC-doc-archive-truth.md` (167 lines, DRAFT, same dump
  timestamp `202608210128`) was written for the twin archive in a parallel pass. Read in full. Overlap
  is deliberate and bounded: it also creates a `docs/05-archive-index.md` and also corrects a stale
  status page, so **step 3 and step 6 here follow its shape on purpose** — two sibling archives that
  index themselves differently would be worse than a little repetition. It does **not** overlap on:
  text extraction (it indexes filenames only), the endpoint-coverage report, the citation-integrity
  loop, or the LaunchAgent. It also leaves as an unanswered **BLOCKER** the very thing this pass
  settled — *"`gh` is not installed, so this repo's GitHub visibility is UNVERIFIED"* — which is filed
  back to it rather than re-asked here (see **Items**, last row).
- **decisions:** `ls DECISIONS.md` → `No such file or directory`. This repo holds no decision log. The
  decisions bearing on it live next door and this spec contradicts none of them; it propagates two:
  `../amzn-api-integration/DECISIONS.md:1809` (*"archives are referenced by relative path
  (`../Amazon_SP_API`), never committed into the code repo"*) — which is precisely why the text
  sidecars land in the container and not in either repo — and `:1862`/`:1870` (public-unlisted app
  model; **OQ5 Brand Analytics PARKED by founder, "do not apply for the role now"**), which
  `docs/03-status.md` must state rather than quietly re-open.

## Blast radius

Everything here is: new markdown in this repo, one README rewrite, new Python under the container's
`.claude/checks/`, one new LaunchAgent, and a new derived-text directory. No PDF is renamed, moved,
deleted or re-captured. No code in `amzn-api-integration` changes. No Amazon call, no credential, no
deploy.

What can break, enumerated rather than asserted:

- **The 41 exact filename citations.** They are the reason **this spec renames nothing.** A tidier
  naming scheme (the archive has `+`, `(v1)` and spaces in filenames) would break
  `DECISIONS.md:1862`'s evidence line under an adopted decision. Documented in the index as a
  constraint; not fixed.
- **The archive's own byte integrity.** `shasum -a 256 *.pdf | awk '{print $1}' | sort -u | wc -l` →
  **422**, i.e. 422 files, 422 distinct hashes, **0 duplicate-content groups**, and
  `git ls-files '*.pdf' | wc -l` → **422** matches the 422 on disk. The manifest records those hashes,
  so a future silent re-capture is detectable rather than invisible. Nothing in this spec writes to a
  `.pdf`.
- **Disk.** The PDFs are 170 MB (`du -ch *.pdf | tail -1`). Extracted text will add on the order of a
  few tens of MB under `AMZN API/.claude/spapi-index/`, outside git in both repos.
- **launchd.** One more hourly agent joins five existing `com.thc.amzn-api-*` agents. It is
  `Nice 10 / LowPriorityIO / ProcessType Background` under `gtimeout 3600`, matching its siblings, so
  it cannot wedge a slot. Failure mode if it misbehaves: `launchctl bootout` it; nothing else depends
  on it.
- **Anything reading this repo programmatically:**
  `grep -rl "github.com/The-Hawkers-Club/Amazon_SP_API" --include='*.md' --include='*.py' --include='*.ts' --include='*.json' "/Users/peterbeke/Developer/VS Code" | grep -v node_modules | wc -l`
  → **0**. Positive control, the same sweep for the relative path `../Amazon_SP_API` → **7 files**.
  **So every consumer on this machine reaches the archive by local relative path and none by its
  GitHub URL** — which is why Question 1's "make it private" arm has zero local blast radius, and it is
  worth him knowing that before he answers.
- **Asymmetry worth naming:** the *current* state has a blast radius too. A teammate opening this repo
  today reads a 15-line README, cannot open a single PDF with any tool installed on this machine, and
  would reasonably conclude there is no SP-API integration — when there is one, live, with 12 of 12
  probed endpoints returning 2xx against a real seller connection
  (`../amzn-api-integration/docs/SPAPI-SURFACE-INVENTORY.md:24`).

## Blockers

Exhaustive pre-build sweep. Each arm carries the command that looked and a positive control, because
"no blockers" is an absence claim.

- **BLOCKER — nothing on this machine can read a single one of the 422 PDFs, and step 2 is impossible
  until that is fixed.** `which pdftotext mutool qpdf` → all `not found`; `python3 -c "import pypdf"`,
  `import PyPDF2`, `import fitz`, `import pdfplumber` → all `ModuleNotFoundError`; the Read tool's own
  PDF path → `pdftoppm is not installed`; `which brew` → `command not found`, so poppler cannot be
  installed the usual way. I then tested whether extraction is possible with the standard library
  alone: on `Orders API.pdf`, a pure-`zlib` pass inflated **114 of 125** streams but returned
  subset-font glyph codes, not text (`fi fi fl … Adobe UCS`) — Chrome's `Skia/PDF m149` writer embeds
  subset fonts, so naive extraction is useless.
  **Resolved without him, and cheaply:** every sampled file carries a `ToUnicode` CMap —
  `strings "Orders API.pdf" | grep -c ToUnicode` → **18**, and a 25-file sweep → **ToUnicode present in
  25/25** — which is exactly what a real PDF library needs to map those glyphs back to characters.
  `pip3 --version` → pip 21.2.4 on system Python 3.9.6, so `pip3 install --user pypdf` is the enabling
  step, needs no `brew`, no `sudo`, and is reversible. It is Build order step 1 and carries its own
  gate, so if the install fails the build stops there instead of producing empty sidecars.
- **NOT A BLOCKER — no credential or Amazon grant is required.** This spec reads local PDFs and writes
  local markdown; nothing in it authenticates to Amazon. Role posture is *documented* from an
  already-run live probe (`SPAPI-SURFACE-INVENTORY.md`), never re-probed here. Control: the Build order
  cites no Amazon host and no env var.
- **NOT A BLOCKER — no counterparty must ship first.** The only cross-repo output is one filed
  correction to `Amazon_Ads_API` (its README/START-HERE assert a visibility that is false), and no
  step here waits on it. Control: every path in the Build order is under `AMZN API/`.
- **NOT A BLOCKER — no gate would refuse this.** `ls .github` → absent (no CI); `ls .git/hooks/` →
  samples only, none active; the repo has no linter and no test runner to satisfy.
- **NOT A BLOCKER — this contradicts no founder ruling.** The two live ones it touches are honoured,
  not reopened: **OQ5 (2026-07-04) Brand Analytics PARKED, "do not apply for the role now"** — so
  `docs/03-status.md` records the 403s as a standing decision, and does not propose requesting the
  role; and **DEC-0127/DEC-0128 (2026-08-11)** — onboard everything, clone nothing — which is what put
  this repo on the board in the first place.
- **CONSTRAINT, not a blocker — `push=no` (`org-api-mirror`).** Recorded in **Conflicts**. The build
  and its commit stay local. `git push` is never run; publishing is Item 9, filed.
- **UNVERIFIED, flagged rather than assumed — whether the archive documents the API versions
  production now calls.** Production calls `/orders/2026-01-01` (`grep -rhoE "'/[a-z]+/(v[0-9]|20[0-9]{2}-[0-9]{2}-[0-9]{2})" src/ scripts/ | sort -u` → **21** family/version prefixes, ~19 of them SP-API),
  `../selling-partner-api-models/models/orders-api-model/` contains **`orders_2026-01-01.json`** and that
  tree's last commit is **2026-08-18**, while every PDF here was captured **2026-07-04**
  (`ls -l *.pdf` → all 422 share one mtime; PDF `/CreationDate (D:20260704…)` confirms it independently
  of the filesystem). No filename in the archive carries `2026-01-01`. Whether `Orders API.pdf`
  nonetheless documents that version **cannot be determined until step 2 lands** — I state it as
  UNVERIFIED rather than asserting a gap I could not read. Step 4 exists to answer it.

## Questions

1. **Q:** `The-Hawkers-Club/Amazon_SP_API` is **world-readable on GitHub** and holds 422 PDFs of
   Amazon's copyrighted documentation. Its own `README.md:15` says they are "retained here for internal
   reference by The Hawker's Club team", and `.gitignore:4` says `_THC-*.md` is kept "OUT of the public
   docs repo" — so the repo was made public deliberately, but nothing records why. Should it stay
   public, or flip to private?
   **Why it is his:** the fact is settled and I settled it — unauthenticated
   `curl -s -o /dev/null -w "%{http_code}" https://api.github.com/repos/The-Hawkers-Club/Amazon_SP_API`
   → **200**, body `"private": false`, while the same call for `Amazon_Ads_API` and
   `amzn-api-integration` → **404**, i.e. private. So of the three THC repos in this container, the one
   that is public is the one republishing another company's copyrighted material. What I cannot settle
   is whether that is intended: it is a redistribution and reputational call for an approved Amazon
   solution provider, not a technical one, and no decision log on this machine records it
   (`grep -rn "public" ../amzn-api-integration/DECISIONS.md | grep -i "repo"` → only the
   *app*-model "public-unlisted" decision at `:1860`, which is about the SP-API application, a
   different sense of the word entirely — that near-collision is itself a reason to get the answer on
   the record).
   **Recommendation:** **flip it to private**, and say so in the README. The cost of doing that is
   measurably near zero: **0 files anywhere on this machine reference the GitHub URL, and 7 reference
   the local relative path `../Amazon_SP_API`** (commands and positive control in **Blast radius**), so
   nothing breaks and no workflow changes — a teammate still needs the local clone either way. The cost
   of being wrong in the other direction is not symmetric: an approved solution provider serving a
   competitor-visible, complete mirror of Amazon's docs is a takedown or a partner-relationship
   conversation, and it is not recoverable by deleting the repo afterwards, because the tree is already
   in GitHub history and in whatever has crawled it since **2026-07-04**. If you would rather keep it
   public — a plausible reason is that a public repo is easier to hand to a contractor — say so and the
   README will state that intent plainly instead of contradicting it, and step 7 will keep a
   never-commit-a-secret notice matching the sibling's `Amazon_Ads_API/START-HERE.md:26`.
   **Answer:** _(pending)_

Deliberately **not** asked here, because asking twice is worse than asking once:
- **Who is named Incident Lead** on the data incident-response plan. `docs/04-incident-response-plan.md`
  does not exist in this repo yet (enumerated: `grep -rli "incident response" --include='*.md' "AMZN API/"`
  → 2 hits, both under `Amazon_Ads_API/`), and the same person question is already parked as
  **Question 1 of `Amazon_Ads_API/PLAN/specs/SPEC-doc-archive-truth.md`**. Step 7 here reuses whatever
  he answers there; if that answer has not landed when step 7 runs, step 7 ships with visible brackets
  rather than inventing a name.
- **Whether to request the `Amazon Fulfillment` / `Brand Analytics` roles.** That is `amzn-api-integration`'s
  decision, is already recorded there (`DECISIONS.md:2651`, 2026-07-27), and is bounded by his OQ5
  ruling. This repo documents the posture; it does not reopen it.

## MVP

The shortest route to a true `Done when` is **steps 1, 2, 5 and 6**: make the archive readable, index
it, put the loop around it, and put the real role posture on a status page. That set removes the
failure that costs something today — a teammate opening this repo, unable to open a single PDF and
reading nothing about the integration, concluding there is none and rebuilding an SP-API client that
already exists with 12 of 12 endpoints returning 2xx.

The MVP is exactly these four Items:

- Install `pypdf` and prove it decodes this archive's Skia subset fonts — because: without it no
  sidecar can be produced at all, so `Done when`'s first clause ("one extracted-text sidecar … for
  every one of the 422 PDFs") is not merely unmet but unreachable; every other item that reads PDF
  *content* (steps 2 and 4) is blocked behind it.
- Build the guard's `index` verb → 422 sidecars + manifest — because: it *is* `Done when`'s first
  clause verbatim, and it is the only step that produces the manifest the in-repo index (step 3) and
  the coverage report (step 4) both read.
- Build the converge loop and load the hourly agent — because: `Done when`'s citation clause is a
  *standing* property ("the citation guard reports every `*.pdf` filename … as resolving, **or
  converges it**"), which a one-shot run cannot satisfy by construction; and because the same agent
  re-runs `verify --index`, which is what makes the manifest clause survive a re-capture.
- Write the status page carrying the probed role posture, cited line by line — because: `Done when`
  requires `docs/01–04` to "describe what is actually true", and the status page is the one of those
  four that carries the facts a teammate would otherwise get wrong at cost — that an SP-API
  integration already exists, and which roles it does and does not hold.

**Reaches the goal because:** these four satisfy `Done when`'s first clause outright (sidecar +
manifest row for all 422 PDFs), its citation clause (guarded and converged, not merely reported), and
its last (a page that "describes what is actually true"). The two clauses left unmet by the MVP are
both *derived* from the manifest this set produces rather than independent of it: the in-repo index
(step 3) is a rendering of it and the coverage report (step 4) is a query over it. Nothing in the set
is optional, and everything omitted is downstream of it.

**Holds continuously because:** step 5 is in the MVP precisely so the answer is not "a human re-runs
it". The hourly `com.thc.amzn-api-doc-citations` agent re-derives the whole property from the world
each cycle — it re-reads the 422 PDFs' sha256 against the manifest, re-resolves every `*.pdf` citation
in `../amzn-api-integration` against the files that actually exist, and never consults its own log or a
job table to decide whether it is green (mock the log and the verdict must not move; that is what
`--selftest` pins). It **converges** rather than alarms: distinct remedies, re-read the world after
each, and an unhandled failure signature escalates instead of retrying — so a re-captured or renamed
PDF is repaired or raised within the hour without anyone opening this repo. The one part that
genuinely cannot self-heal is the *prose* of the status page, and that is bounded and named: it
asserts a role posture sourced from a dated live probe, so it carries that date and the file it came
from on its face, and goes stale visibly rather than silently.

Steps 3, 4, 7 and 8 deepen it (in-repo index, coverage report, the guides, the README truth-fix) and
step 8's wording depends on Question 1. A run that stops after step 6 leaves the machine strictly
better off — searchable text, a guarded archive and an honest status page — rather than half-edited
markdown, which is the property this section exists to guarantee.

## Build order

1. **Install a PDF text extractor and prove it decodes this archive's subset fonts** (`pip3 install --user pypdf`; no `brew`, no `sudo`) — gate: `python3 -c "import pypdf"` exits 0 **and** `python3 -c "import pypdf,sys; t=pypdf.PdfReader('Orders API.pdf').pages[0].extract_text() or ''; sys.exit(0 if 'order' in t.lower() and len(t)>500 else 1)"` exits 0 — i.e. real words, not glyph codes.
2. **Write the guard's `index` verb** — for each of the 422 PDFs emit a text sidecar under `../.claude/spapi-index/text/` and one manifest row carrying `name`, `sha256`, `bytes`, `pages`, the PDF's own `/CreationDate`, and extracted `chars` — gate: `python3 "$G" verify --index` exits 0: 422 sidecars present, each source sha256 matching the manifest, and none under a minimum character floor (a zero-byte sidecar is the silent failure this arm exists to catch).
3. **Generate the in-repo archive index** from `ls *.pdf` plus the manifest — one row per PDF, grouped by SP-API surface, each with its 2026-07-04 capture date; filenames only and no Amazon body text, so the in-repo artifact stays a table of contents rather than a second copy — gate: the DoD block's final `python3 -c` arm exits 0, i.e. every PDF on disk appears in the index.
4. **Generate the coverage report** — for each of the ~19 SP-API family/version prefixes production calls (from `grep -rhoE "'/[a-z]+/(v[0-9]|20[0-9]{2}-[0-9]{2}-[0-9]{2})" ../amzn-api-integration/src ../amzn-api-integration/scripts | sort -u`, minus the Ads-side `/sb/v4` and `/dsp/v1`) and each of the 52 model directories in `../selling-partner-api-models/models/`, record whether this archive documents it and at which version — searched over the step-2 sidecars, not filenames. This settles the UNVERIFIED item in **Blockers**: does anything here document Orders **2026-01-01**? — gate: `python3 "$G" verify --coverage` exits 0, every prefix carries an explicit COVERED/UNCOVERED verdict, and `grep -c` of the verdict lines equals the prefix count, so no prefix can be silently absent.
5. **Write the citation guard and its mutants, and load the hourly agent** — `converge` re-reads the world after spending each **distinct** remedy (re-resolve by suffix → search the manifest for a renamed twin → escalate); an unknown failure signature **escalates, never retries**; the budget counts distinct remedies, not re-runs; and the goal predicate reads the archive and the citing files, never the agent's own log (`~/.claude/commands/references/process-loop.md`). Stage `com.thc.amzn-api-doc-citations.plist` beside its four siblings in the container's `.claude/checks/` and install it into `~/Library/LaunchAgents/` the way the existing five are — gate: the mutants script exits 0 (a planted rename of a cited PDF makes `verify --citations` exit non-zero and `converge` either repairs it or escalates; with the plant reverted both go green) **and** `launchctl list | grep -q com.thc.amzn-api-doc-citations`.
6. **Write the status page** — integration lives in `The-Hawkers-Club/amzn-api-integration` (`src/spapi/`, `src/spine/`); 12 of 12 probed endpoints 2xx against a live seller (`SPAPI-SURFACE-INVENTORY.md:24`); **Inventory & Order Tracking held, Amazon Fulfillment not held** (deduced from a 200/403 split reproduced 3×, `DECISIONS.md:2651`); Brand Analytics not held and **PARKED by founder ruling OQ5**; RDT/PII not held; app model public-unlisted with `APP_STATE=draft` in production; and the measured rate-limit spread (`getOrders` at ~1 req/min) — gate: `grep -q 'amzn-api-integration' docs/03-status.md && grep -q 'Inventory and Order Tracking' docs/03-status.md && grep -q 'OQ5' docs/03-status.md`.
7. **Write START-HERE and the 01/02/04 guides** on the sibling archive's shape (`../Amazon_Ads_API/START-HERE.md` and its `docs/`), so the two archives read alike; `04` reuses the Incident Lead answer parked on the Ads spec, or ships with visible brackets if that has not landed — gate: `test -f START-HERE.md && test -f docs/01-getting-started.md && test -f docs/02-playbook.md && test -f docs/04-incident-response-plan.md && grep -q '05-archive-index' START-HERE.md`.
8. **Rewrite `README.md:5` and `README.md:15`** — repoint the asserted coverage bullet at the enumerated index, and replace the false "internal reference" sentence with this repo's actual visibility per Question 1's answer (or, unanswered, with the observed fact plus a dated `UNRULED` marker; the DoD only requires that the false sentence is gone) — gate: `! grep -q 'internal reference by The Hawker' README.md && grep -q '05-archive-index' README.md`.
9. **Run the DoD block, then commit — staging by name, never `git add -A`** (`README.md`, `.gitignore`, `START-HERE.md`, `docs/`, `PLAN/specs/`, `PROJECT-LEDGER.md`). **Do not push** (`push=no`); file the publish request instead with `python3 ~/.claude/tools/xrepo-relay.py request --to amzn-api-integration --title "Push Amazon_SP_API doc surface to origin" --body-file PLAN/specs/SPEC-spapi-archive-readable-and-guarded.md` — gate: the DoD block exits **0**, having exited **2** before step 1.

## Items

- Install `pypdf` (`pip3 install --user pypdf`, no brew/sudo) and prove it decodes this archive's
  Skia subset fonts — today **no tool on this machine can read one of the 422 PDFs** (pdftotext/mutool/qpdf
  absent, four Python PDF libraries absent, Read's `pdftoppm` absent, brew absent, stdlib zlib returns
  glyph codes); ToUnicode CMaps present in 25/25 sampled files make this the one cheap unlock.
- Build `AMZN API/.claude/checks/spapi_doc_guard.py index` → 422 text sidecars + `manifest.json`
  (sha256, bytes, pages, PDF `/CreationDate`, chars) under `AMZN API/.claude/spapi-index/`, deliberately
  outside the world-readable repo and outside `amzn-api-integration` per `DECISIONS.md:1809`.
- Create `docs/05-archive-index.md` — every one of the 422 PDFs by name and surface with its 2026-07-04
  capture date; record that renaming is refused because `../amzn-api-integration` cites 41 of these
  filenames exactly, one of them as the evidence line under an adopted decision (`DECISIONS.md:1862`).
- Produce the coverage report: ~19 SP-API family/version prefixes production calls × 52 models in
  `../selling-partner-api-models` × what this archive documents — searched over extracted text, not
  filenames. Settles whether Orders **2026-01-01** (called in `src/`, present in the models tree,
  absent from every filename here) is documented at all.
- Build the citation-integrity converge loop + `mutants_spapi_doc_guard.py` + hourly
  `com.thc.amzn-api-doc-citations` LaunchAgent, in the container's existing `.claude/checks/` pattern:
  distinct remedies, escalate on unknown signature, goal predicate reads the archive and never the log.
  Baseline to hold: **70 cited `.pdf` tokens, 56 exact + 12 suffix + 2 glob, 0 dangling.**
- Write `docs/03-status.md` — the probed role posture (I&OT held, Amazon Fulfillment not, Brand
  Analytics not and PARKED by OQ5, RDT/PII not), 12/12 endpoints 2xx, `APP_STATE=draft` in production,
  and the measured rate-limit spread — each line cited to the file that observed it.
- Write `START-HERE.md`, `docs/01-getting-started.md`, `docs/02-playbook.md` and
  `docs/04-incident-response-plan.md` on the sibling archive's shape; `04` reuses the Incident Lead
  answer parked on `Amazon_Ads_API/PLAN/specs/SPEC-doc-archive-truth.md` rather than re-asking.
- Rewrite `README.md:5,15` — repoint the asserted coverage bullet at the enumerated index and delete
  the "internal reference" sentence that GitHub contradicts.
- Commit locally, staging paths by name; **do not push** (`org-api-mirror`, `push=no`), and file the
  publish request through `xrepo-relay.py`.
- 🔗 FILED CROSS-REPO (not an item here): `Amazon_Ads_API/README.md:16` and `START-HERE.md:26` both tell
  the team *"This repo is **public**"* and base a credential-handling instruction on it — it is
  **private** (unauthenticated `api.github.com` → 404, vs 200 and `"private": false` for
  `Amazon_SP_API`). This also closes the open **BLOCKER** in that repo's own
  `PLAN/specs/SPEC-doc-archive-truth.md`, which recorded the visibility as UNVERIFIED because `gh` is
  not installed — `curl` against the public API needs no `gh` and no auth.
