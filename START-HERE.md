# START HERE — Amazon SP-API Documentation Archive

Welcome. This repo is **not** the SP-API integration — it is the offline reference archive a
**live** integration cites by filename. The integration is
[`The-Hawkers-Club/amzn-api-integration`](https://github.com/The-Hawkers-Club/amzn-api-integration)
(`src/spapi/`, `src/spine/`), already live with **12 of 12 probed endpoints returning 2xx** against
a real seller connection. If you came here looking for the integration itself, go there.

## What's in this repo

**422 PDFs** of Amazon's Selling Partner API documentation, captured 2026-07-04, plus a small set
of markdown guides. `The-Hawkers-Club/Amazon_SP_API` is currently **public** on GitHub — see
`README.md` for the founder ruling on whether that stays true.

## What to read, in order

1. **[docs/01-getting-started.md](docs/01-getting-started.md)** — how to actually search this
   archive: the manifest, the extracted-text sidecars, and why you can't just `grep` a PDF.
2. **[docs/02-playbook.md](docs/02-playbook.md)** — how the archive is maintained: the indexing
   guard, the citation-integrity loop, when and how it gets re-captured.
3. **[docs/03-status.md](docs/03-status.md)** — the real role posture of the live integration
   (which surfaces return 200, which return 403 and why), cited line by line.
4. **[docs/04-incident-response-plan.md](docs/04-incident-response-plan.md)** — the
   data-incident-response plan covering material handled through this archive's tooling.
5. **[docs/05-archive-index.md](docs/05-archive-index.md)** — every PDF on disk, grouped by
   SP-API surface, with its capture date.
6. **[docs/06-coverage-report.md](docs/06-coverage-report.md)** — which SP-API family/version
   prefixes production actually calls are, and are not, documented here at the 2026-07-04 capture.

## Filenames are load-bearing — don't rename them

`../amzn-api-integration` cites 41 of these filenames **exactly**, one of them
(`Authorization Limits.pdf`) as the evidence line under an adopted decision
(`DECISIONS.md:1862` there). An hourly guard
(`AMZN API/.claude/checks/spapi_doc_guard.py converge`) checks every `*.pdf` citation in that repo
still resolves against a real file here, and escalates rather than silently tolerating drift.

## ⚠️ This archive republishes Amazon's copyrighted documentation

Never commit anything here beyond the archive's own PDFs and the markdown guides above. No
credential, no client data, and no Amazon API response body belongs in this repo — the extracted
text sidecars this archive's tooling produces live outside it, in the container's
`.claude/spapi-index/`, never inside either git tree.
