# TriplePeek paper

**Title:** TriplePeek: From Entity Search to Live Linked Data Exploration  
**Authors:** Albert Khomich, Mohamed Ahmed Sherif, Axel-Cyrille Ngonga Ngomo

**Status:** Technical system/demo draft, updated 25 September 2026 with author information and an explicit six-endpoint test inventory and two sets of six observed search timings for a 20-million-entity catalog.

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

The revised draft incorporates Albert Khomich's exploratory endpoint tests and qualitative experience with a 20-million-entity catalog. These tests were not rerun during the editorial update. The author-supplied search durations, including the additional localhost Network-panel capture with browser caching disabled, are reported as exploratory observations, not a controlled benchmark; no numerical endpoint latency, throughput, or user-study results are asserted. The draft includes the demo plan and ethical-data section. The tests took place on 25 September 2026 on a VMware VM with 8 vCPUs (Intel Xeon Platinum 8462Y+), 31 GiB RAM, and a 1 TB ext4 virtual disk; application and database ran in separate containers on this VM. Evaluation separates local search performance from button and catalog-generator compatibility; external endpoint response times are outside scope. Prepare supporting demo materials before submission.

## Reproducibility paths

### Quick Start
Clone https://github.com/dice-group/triple-peek and follow https://dice-group.github.io/triple-peek/ using the bundled 10,000-entity catalog. This reproduces the live visitor demonstration: search for Neuschwanstein Castle, navigate with Describe, open Details, and retrieve the precomputed representation with Embedding. Live actions require the configured endpoints. The separate catalog/template configuration walkthrough is operator-led.

### Large-catalog experiment
Download the archived 20-million-entity CSV from https://zenodo.org/records/22958238, then follow the documented validation and PostgreSQL import pipeline. With the catalog loaded, use localhost and disable browser caching. Reproduce the captured search request sequence with limit=20: neusch, italy, italy cast, neusch, muse, museum. Record request durations in the browser Network panel. These observations are distinct from the earlier Berlin place typing session, whose exact per-request prefixes were not recorded. Search operates locally; do not time external SPARQL services or repeat the same search workload merely because the remote endpoint changes.
