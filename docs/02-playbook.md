# Playbook — how this archive is maintained

This repo has no runtime, no package manifest, no test runner, no CI. Everything that keeps it
honest runs from the container's existing check directory, not from inside this repo.

## The four moving parts

1. **`index`** — extracts text from every `*.pdf` into a sidecar, writes `manifest.json`
   (sha256/bytes/pages/CreationDate/chars per file). Run manually after any re-capture; not run by
   the hourly agent (it needs `pypdf`, which the hourly agent's interpreter deliberately does not
   have — see below).
2. **`verify [--index] [--citations] [--coverage]`** — report-only, never writes. Confirms the
   manifest matches the PDFs on disk, that every `*.pdf` citation in `../amzn-api-integration`
   resolves to a real file here or in `../Amazon_Ads_API`, and that the coverage report names a
   verdict for every SP-API prefix production calls.
3. **`converge`** — the hourly loop. Re-reads the archive and the citing repo from scratch every
   run (never trusts its own log), spends **distinct** remedies for a dangling citation
   (suffix re-resolve, then a case-insensitive search for a renamed twin in the manifest), and
   **escalates** the first token neither remedy explains rather than retrying it.
4. **`render --archive-index` / `render --coverage`** — regenerates
   [`05-archive-index.md`](05-archive-index.md) and [`06-coverage-report.md`](06-coverage-report.md)
   from the manifest.

All four verbs live in one file: `AMZN API/.claude/checks/spapi_doc_guard.py`.

## Why the hourly agent runs a different Python than `index`

`index` needs `pypdf` to decode the archive's subset fonts — nothing in the standard library can.
`verify` and `converge` never touch PDF bytes; they read the manifest and sidecars `index` already
produced. So the hourly LaunchAgent (`com.thc.amzn-api-doc-citations`, `converge` only) runs on
`/usr/bin/python3` — the same stdlib-only interpreter the container's other hourly guards use — and
cannot be taken down by a Homebrew or venv change that would take a `pypdf`-dependent script down.
`index` itself is invoked with `/opt/homebrew/bin/python3` (the interpreter `pypdf` was installed
against), by hand, after a re-capture.

## The citation-integrity invariant this loop holds

`../amzn-api-integration` hangs adopted decisions and specs on 41 exact `*.pdf` filenames in this
archive — `DECISIONS.md:1862` there cites `Authorization Limits.pdf` as the evidence line under an
**adopted** decision. Measured 2026-08-21: **70 distinct backticked `*.pdf` tokens across that
repo — 56 resolve exactly, 12 resolve by suffix** (the Ads archive embeds `:` path segments in
filenames the Markdown backtick form strips), **2 are globs, 0 dangle.** The loop's job is to keep
that `0` at `0`, or say loudly the day it isn't.

## Renaming a PDF is refused, not just discouraged

Because of the citation set above, this playbook does not offer a "clean up the filenames" task.
If a PDF must be renamed, the citing lines in `../amzn-api-integration` have to move first, in the
same change — otherwise the guard's next hourly run reports `ESCALATE_CITATIONS` correctly.

## Re-capturing the archive

1. Re-download the PDFs (out of scope for this playbook — a separate, manual capture pass).
2. `python3 "AMZN API/.claude/checks/spapi_doc_guard.py" index` — re-extracts every sidecar and
   rewrites the manifest; sha256 for a re-captured file will legitimately change.
3. `python3 "AMZN API/.claude/checks/spapi_doc_guard.py" render --archive-index --coverage` —
   regenerates the two derived docs.
4. `python3 "AMZN API/.claude/checks/spapi_doc_guard.py" --selftest` — proves the guard can still
   detect a fault before trusting its next `verify` run.
