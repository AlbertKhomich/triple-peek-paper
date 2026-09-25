# TriplePeek paper

**Title:** TriplePeek: From Entity Search to Live Linked Data Exploration  
**Authors:** Albert Khomich, Mohamed Ahmed Sherif, Axel-Cyrille Ngonga Ngomo

**Status:** Technical system/demo draft, updated 25 September 2026 with author information and an explicit six-endpoint test inventory and seven visible search-request timings for a 17,795,730-entity catalog.

## Open in Overleaf

1. Upload the project ZIP as a new Overleaf project.
2. Choose `main.tex` as the main document and pdfLaTeX with a recent TeX Live version (2025 or newer).
3. Recompile; Overleaf runs the bibliography automatically. If stale citations remain, recompile from scratch.
4. Author names, the shared DICE/Paderborn affiliation, all three ORCIDs, and Albert Khomich's email are in `metadata.tex`. Both layouts use this metadata.

The diagram is included as a vector PDF so Overleaf does not require SVG conversion or shell escape. The compact SVG is editable, and the original diagram is retained. Standard LaTeX packages, both document classes, and both bibliography styles are included or available in Overleaf's TeX distribution.

`main.tex` uses the ACM double-column review format required by The Web Conference 2027 demo call. `reference-style.tex` uses the official LNCS class, matching the presentation style of the supplied LimesWebUI reference. Both use the same `abstract.tex`, `body.tex`, and `references.bib`; edit the content only once. The LNCS layout is an alternative for further editing, not a verified ESWC 2027 submission format.

## Local compilation

With a standard TeX Live installation:

```sh
latexmk -pdf main.tex
latexmk -pdf reference-style.tex
```

Or run `pdflatex`, `bibtex`, and `pdflatex` twice. Both entry points were also compiled and visually checked with Tectonic 0.17.0. Recheck the page count after changing authors, affiliation, wording, or compiler.

## Files

- `main.tex`: recommended ACM submission entry point.
- `reference-style.tex`: LNCS alternative.
- `metadata.tex`: editable title and author information.
- `abstract.tex`, `body.tex`: shared paper text.
- `references.bib`: verified bibliographic references.
- `figures/how-it-works-compact.svg` and `.pdf`: compact workflow used by both paper layouts.
- `figures/how-it-works.svg` and `.pdf`: original diagram retained for reference.
- `VENUES.md`: checked calls and recommended target.
- `EDITOR_NOTES.md`: provenance, validation scope, and remaining author decisions.
- `vendor/`: upstream class sources, license notices, and provenance.

The draft incorporates author-supplied endpoint compatibility checks and a browser capture with the 17,795,730-entity catalog loaded. Seven visible search requests took 256–1,370 ms (median 420 ms); the panel footer lists 17 requests, but unseen rows are not analyzed. The updated experiment environment is an Intel Xeon Silver 4310 server (12 physical cores, 24 hardware threads, 2.10 GHz), 62 GiB RAM, and two Samsung 240 GB SSDs in RAID 1 with ext4 for PostgreSQL data. Application and database use Docker Compose. Tests are dated 25 September 2026. This supersedes the earlier VM description and timing samples in the manuscript. External SPARQL response times are outside scope.

## Reproducibility paths

### Quick Start
Clone https://github.com/dice-group/triple-peek and follow https://dice-group.github.io/triple-peek/ using the bundled 10,000-entity catalog. This reproduces the live visitor demonstration: search for Neuschwanstein Castle, navigate with Describe, open Details, and retrieve the precomputed representation with Embedding. Live actions require the configured endpoints. The separate catalog/template configuration walkthrough is operator-led.

### Large-catalog experiment
Download the archived 17,795,730-entity CSV from https://zenodo.org/records/22963871 and follow the documented validation and PostgreSQL import pipeline. For live actions on these DBpedia resources, replace the default endpoint in `.env` with:

```dotenv
SPARQL_ENDPOINT=https://dbpedia.data.dice-research.org/sparql
```

Apply the updated configuration through Docker Compose and use DBpedia-compatible SPARQL button templates. The author reports that this Tentris service hosts the full DBpedia 2022-12 snapshot used for the setup. The official DBpedia service has limited dataset coverage and query limits (https://www.dbpedia.org/resources/sparql/); it is not used for this large-catalog exploration path. Endpoint configuration affects live actions, not the independent local search workload.

With the catalog loaded and browser caching disabled, issue these searches in order with `limit=20`: `dublin`, `irlnad`, `irland`, `paderborn`, `hein nixdor`, `hein nixdorf`, `henin nixdorf`. Preserve the misspellings, which are present in the supplied capture. Record HTTP request durations in the browser Network panel. The seven visible samples are 707, 307, 1,370, 305, 636, 420, and 256 ms. Do not infer the ten unseen requests from the footer's total of 17. Do not time external SPARQL services or repeat search merely because the remote endpoint changes.
