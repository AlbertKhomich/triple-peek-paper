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

1. Author order, all three ORCIDs, Albert Khomich's email, and the shared affiliation were added from the author's instructions on 25 September 2026. Academic titles are omitted from the byline by publication convention. The title-page conference text remains explicitly a draft.
2. Decide whether to target WWW 2027 demo or wait for ESWC's actual call. Check all final instructions and the page count after edits.
3. The six-endpoint inventory, three Tentris 1.0.0 versions, DICE snapshots, DESCRIBE coverage, eight-core/32-GB hardware, and six search timing observations have now been supplied. Still document test dates, CPU/storage details, exact query strings for each sample, cache state, concurrency, and the catalog source. Record the endpoint/action mapping for custom queries and identify the earlier Uni corpus/Fuseki deployment before asserting a complete compatibility matrix.
4. Prepare the conference demonstration, a short video, and an honestly labeled offline fallback. The manuscript presents these as a plan, not completed supporting materials.
5. If making performance, retrieval-quality, or usability claims later, collect evidence first. Suggested measurements: separately timed search/action latency (median and p95), catalog size/import cost, endpoint request counts, relevance judgments for representative queries, and a consent-based task study. Do not transplant the reference paper's results.
6. Check source/media licensing and any venue-required disclosure of AI-assisted writing against current policy. Add genuine funding and acknowledgments only when provided.

The project intentionally avoids fake benchmark tables, invented participants, unsupported scale claims, fabricated affiliations, and assertions of acceptance or publication.


## Author-supplied deployment evidence — 25 September 2026

Albert Khomich reported testing public Wikidata and DBpedia endpoints, SemRepo, and DICE endpoints serving Wikidata, DBpedia, and a Uni corpus, with deployments including Virtuoso, Tentris, and Fuseki. He also reported loading 20 million entities with labels and aggregated types in one row per entity and finding interactive search still “snappy.” The paper now presents this as exploratory testing and qualitative responsiveness. These observations are supplied by the author, not independently reproduced during this edit. They are distinct from the bundled 10,000-row file and the previously executed mocked regression tests.

The report does not provide exact endpoint-to-engine mappings, hardware, timing logs, workload/concurrency details, or a catalog manifest. Consequently the manuscript does not assign Virtuoso to the canonical Wikidata Query Service, claim that every dataset was tested on every engine, or invent response times. “Uni corpus” is retained as the supplied dataset label and should be identified more precisely for reproducibility. Automatic aggregation of repeated IRIs is also supported by the inspected validation implementation.

SemRepo's description and bibliographic entry were verified against https://github.com/faerber-lab/SemRepo and https://arxiv.org/abs/2605.13310. The ORCID IDs and email were copied from the author's instructions; ORCID profile pages did not provide readable metadata in the browsing tool. No coauthor email addresses were inferred.


## Endpoint and timing clarification — 25 September 2026

The later author message supersedes the absence of concrete endpoints/hardware/timings in the earlier notes above. DESCRIBE succeeded against all six endpoints now listed in Table 1; selected custom buttons were also tested, with no per-endpoint action matrix supplied. The author describes endpoint answers as “instantly”; no remote-endpoint durations were supplied.

- https://sparql.embeddings.cc/sparql — DBpedia and Wikidata embeddings; Tentris 1.0.0 (author supplied).
- https://dbpedia.data.dice-research.org/sparql — DBpedia 2022-12 snapshot; Tentris 1.0.0 (author supplied).
- https://wikidata.data.dice-research.org/sparql — Wikidata 2025-01-22 truthy beta; Tentris 1.0.0 (author supplied).
- https://query.wikidata.org/ — UI for the official service, whose query endpoint is https://query.wikidata.org/sparql. Wikimedia's runbook identifies Blazegraph, correcting the author's tentative Virtuoso attribution: https://wikitech.wikimedia.org/wiki/Wikidata_query_service/Runbook.
- https://dbpedia.org/sparql — Virtuoso, confirmed by DBpedia's official documentation: https://www.dbpedia.org/resources/sparql/.
- https://semrepo.org/sparql — the endpoint UI identifies OpenLink Virtuoso. Its currently displayed version is not asserted as the version at the author's test time.

The supplied snapshot links were retained as author-provided provenance. Direct browsing could not retrieve the dated Wikidata directory; the DBpedia snapshot page redirected to authentication. Neither snapshot was downloaded or independently inspected. No test queries were executed during this edit.

Reported search values in supplied order: 502, 52, 42, 83, 184, 124 ms; n=6, min=42 ms, max=502 ms, median=103.5 ms, arithmetic mean=164.5 ms. They were observed while typing “Berlin place” against 20 million catalog entities. The paper uses raw values, range, and median without inferring per-prefix mappings, outliers, cache warmup, percentiles, or a speedup. “32 RAM” is interpreted as 32 GB RAM. The author subsequently confirmed the browser Network panel as the timing source and an 8-core/32-GB VM hosting both TriplePeek and PostgreSQL in separate Docker Compose containers. These are HTTP search-request durations, excluding the pre-request 300-ms debounce; they neither isolate SQL execution nor time the remote SPARQL endpoints.
