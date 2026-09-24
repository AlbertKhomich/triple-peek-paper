# TriplePeek paper

**Title:** TriplePeek: From Entity Search to Live Linked Data Exploration  
**Author:** Albert Khomich  
**Status:** Technical system/demo draft, prepared 24 September 2026. Affiliation and country deliberately remain editable placeholders.

## Open in Overleaf

1. Upload the project ZIP as a new Overleaf project.
2. Choose `main.tex` as the main document and pdfLaTeX with a recent TeX Live version (2025 or newer).
3. Recompile; Overleaf runs the bibliography automatically. If stale citations remain, recompile from scratch.
4. Edit `metadata.tex` for your affiliation and country; add email, ORCID, and any coauthors in `main.tex`.

The diagram is included as a vector PDF so Overleaf does not require SVG conversion or shell escape. The original SVG is retained. Standard LaTeX packages, both document classes, and both bibliography styles are included or available in Overleaf's TeX distribution.

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
- `figures/how-it-works.svg` and `.pdf`: original diagram and LaTeX-ready vector conversion.
- `VENUES.md`: checked calls and recommended target.
- `EDITOR_NOTES.md`: provenance, validation scope, and remaining author decisions.
- `vendor/`: upstream class sources, license notices, and provenance.

No conference submission, external publication, endpoint load test, user study, or performance benchmark was performed. The draft includes the required demo plan and ethical-data section, but supporting demo materials and live checks still need to be completed before submission.
