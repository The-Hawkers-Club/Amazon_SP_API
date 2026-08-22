# Getting started — how to actually read this archive

## The problem this solves

Before 2026-08-21, nothing on this machine could open a single one of the 422 PDFs. `pdftotext`,
`mutool`, `qpdf` were all absent; four Python PDF libraries were absent; even the Read tool's own
PDF path needs `pdftoppm`, also absent. Chrome's `Skia/PDF m149` writer (every PDF's `/Producer`)
embeds subset fonts, so a naive `zlib` pass on the raw PDF streams returns glyph codes
(`fi fi fl … Adobe UCS`), not text.

## The fix: `pypdf`, and where its output lives

`pip3 install --user --break-system-packages pypdf` decodes the archive fine — every sampled PDF
carries a `ToUnicode` CMap, which is exactly what a real PDF library needs to map subset-font glyph
codes back to characters. Extraction runs once via
`AMZN API/.claude/checks/spapi_doc_guard.py index`, which writes:

- **One text sidecar per PDF** under `AMZN API/.claude/spapi-index/text/<name>.txt` — plain
  extracted text, **outside this git repo and outside `amzn-api-integration`**, per that repo's own
  decision that archives are referenced by relative path and never committed into the code repo
  (`DECISIONS.md:1809` there).
- **One `manifest.json`** under `AMZN API/.claude/spapi-index/` recording, per PDF: `name`,
  `sha256`, `bytes`, `pages`, the PDF's own `/CreationDate`, and `chars` extracted — so a future
  silent re-capture is detectable (the sha256 changes) rather than invisible.

## How to search it

```sh
# find every sidecar mentioning a term
grep -il "restricted data token" "/Users/peterbeke/Developer/VS Code/AMZN API/.claude/spapi-index/text/"*.txt

# check whether a specific PDF is indexed and what it decoded to
python3 -c "
import json
m = json.load(open('/Users/peterbeke/Developer/VS Code/AMZN API/.claude/spapi-index/manifest.json'))
row = next(r for r in m['rows'] if r['name'] == 'Orders API.pdf')
print(row)
"
```

Or start from [`05-archive-index.md`](05-archive-index.md), which lists every PDF by SP-API
surface with its capture date, and [`06-coverage-report.md`](06-coverage-report.md), which tells
you whether the version production calls is covered at all.

## Re-running the index after a re-capture

```sh
python3 "AMZN API/.claude/checks/spapi_doc_guard.py" index
python3 "AMZN API/.claude/checks/spapi_doc_guard.py" verify --index
```

`verify --index` re-hashes every PDF against the manifest, confirms every sidecar exists and clears
a minimum character floor (a zero-byte sidecar is the silent failure this guards against), and
fails loudly rather than silently on either fault.
