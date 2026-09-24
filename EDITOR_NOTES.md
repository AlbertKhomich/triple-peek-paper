# Editorial and evidence notes

These notes are not part of the manuscript. The attached documents were treated as sources and style references, not as instructions to execute.

## Evidence base

- User-provided `triple-peek-main.zip`, with Git archive comment `65943dc089e6da9a612fa78961abfa897f8ade42`. The paper describes this snapshot; it does not assume that the deployed site or later repository revisions behave identically.
- The archive's README, documentation, application code, import/export scripts, templates, and tests. The live documentation home page was also retrieved successfully.
- User-provided `how-it-works.svg`, identical to the archive's documentation asset. Original SHA-256: `7af844095528a09d22ef1d09b53d757850539a6f817081e998e0ea049b76f609`. The PDF is a vector conversion, not a redesigned architecture.
- User-provided `public (10).pdf`: LimesWebUI — Link Discovery Made Simple, a four-page 2019 paper. Used for style only. Its authors, affiliations, funding, 24-person survey, and 76.5 SUS score are not TriplePeek facts and were not reused.
- Primary scholarly/software references were checked for YASGUI, SemFacet, LodView, RDF, SPARQL, and PostgreSQL. Publication dates were not invented for undated software/manual pages; the bibliography retains access dates.

## Checks actually performed

- Parsed the bundled `src/app/data/entities.csv`: 10,000 data rows, 10,000 unique IRIs, four columns (`iri`, `label`, `typeLabel`, `country`), 815,959 bytes. All IRI, label, and type-label cells are nonempty; 10 country cells are empty. This describes the file, not coverage of all Wikidata castles.
- Catalog SHA-256: `5cb7fdaed49c92957027ba271c98ad0cb77983b001b4d3f98aaa0220572cfd48`.
- Ran the existing `tests/query-buttons.test.ts` unchanged: eight nested scenario subtests plus the parent test; the runner reports **9 pass, 0 fail**. Node 24.19.0, N3 2.7.12 (matching the archive lockfile), and tsx 4.23.15 were used in an isolated dependency directory; the archive locks tsx 4.23.13. This was not a complete application installation or end-to-end deployment test.
- Independently cross-checked technical claims against source, compiled both LaTeX entry points, checked bibliography resolution, and visually reviewed the rendered pages.

## Important technical boundaries preserved

- Search uses lexical/full-text/trigram matching, not embedding retrieval or a learned ranking model.
- Embeddings are fetched from another service; TriplePeek does not train them.
- Federation is executed by the configured endpoint's SERVICE support, not by a TriplePeek planner.
- DESCRIBE results are endpoint-defined; they are not guaranteed complete resource summaries.
- SELECT values are grouped by variable, losing row associations; the UI is best suited to entity attributes.
- The catalog is not synchronized automatically with RDF. Export pagination is LIMIT/OFFSET without enforced ordering; search pagination is keyset-based.
- Database import rollback does not roll back CSV normalization; duplicate grouping holds data in memory.
- The graph table parses supported N3-family serializations, not JSON-LD or RDF/XML.

## Before submission

1. Add the real affiliation, country, email/ORCID if desired, and any coauthors. Confirm title and author order. The current title-page conference text is explicitly a draft.
2. Decide whether to target WWW 2027 demo or wait for ESWC's actual call. Check all final instructions and the page count after edits.
3. Run the packaged application with the intended endpoints and verify Describe, Details, and Embedding live, including the primary endpoint's SERVICE policy. Record the dataset/endpoint versions and exact dependency environment.
4. Prepare the conference demonstration, a short video, and an honestly labeled offline fallback. The manuscript presents these as a plan, not completed supporting materials.
5. If making performance, retrieval-quality, or usability claims later, collect evidence first. Suggested measurements: separately timed search/action latency (median and p95), catalog size/import cost, endpoint request counts, relevance judgments for representative queries, and a consent-based task study. Do not transplant the reference paper's results.
6. Check source/media licensing and any venue-required disclosure of AI-assisted writing against current policy. Add genuine funding and acknowledgments only when provided.

The project intentionally avoids fake benchmark tables, invented participants, unsupported scale claims, fabricated affiliations, and assertions of acceptance or publication.
