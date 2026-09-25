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
3. Use the current server experiment in the final section of these notes: Intel Xeon Silver 4310, 62 GiB RAM, mirrored Samsung SSDs, and seven visible timing samples with 17,795,730 catalog entities loaded. Earlier hardware and timings in these historical notes are superseded. The current Zenodo record is https://zenodo.org/records/22963871. A complete endpoint/action matrix and concurrent-load workload are not supplied.

4. Prepare the conference demonstration, a short video, and an honestly labeled offline fallback. The manuscript presents these as a plan, not completed supporting materials.
5. If making performance, retrieval-quality, or usability claims later, collect evidence first. Suggested measurements: local search latency (median and p95) and throughput, catalog size/import cost, button compatibility and generator completion/output validity across endpoints, relevance judgments for representative queries, and a consent-based task study. External endpoint response-time benchmarking is outside scope. Do not transplant the reference paper's results.
6. Check source/media licensing and any venue-required disclosure of AI-assisted writing against current policy. Add genuine funding and acknowledgments only when provided.

The project intentionally avoids fake benchmark tables, invented participants, unsupported scale claims, fabricated affiliations, and assertions of acceptance or publication.


## Author-supplied deployment evidence — 25 September 2026

Albert Khomich reported testing public Wikidata and DBpedia endpoints, SemRepo, and DICE endpoints, as detailed below. Fuseki support was checked using a temporary endpoint; no university corpus is declared. The author reported a loaded catalog of 17,795,730 entities with labels and aggregated types in one row per entity. These observations were not independently reproduced during the editorial updates and are distinct from the bundled 10,000-row file and mocked regression tests. Automatic aggregation of repeated IRIs is supported by the inspected validation implementation.

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

Reported search values in supplied order: 502, 52, 42, 83, 184, 124 ms; n=6, min=42 ms, max=502 ms, median=103.5 ms, arithmetic mean=164.5 ms. They were observed while typing “Berlin place” against 17,795,730 catalog entities. The paper uses raw values, range, and median without inferring per-prefix mappings, outliers, cache warmup, percentiles, or a speedup. “32 RAM” is interpreted as 32 GB RAM. The author subsequently confirmed the browser Network panel as the timing source and an 8-core/32-GB VM hosting both TriplePeek and PostgreSQL in separate Docker Compose containers. These are HTTP search-request durations, excluding the pre-request 300-ms debounce; they neither isolate SQL execution nor time the remote SPARQL endpoints.

## Evaluation scope and environment correction — 25 September 2026

The author confirmed 25 September 2026 as the date for all reported deployment tests and search measurements. The exact environment supersedes earlier rounded hardware descriptions: VMware VM, 8 vCPUs (Intel Xeon Platinum 8462Y+), 31 GiB RAM, 1 TB virtual disk formatted with ext4. TriplePeek and PostgreSQL shared the VM in separate Docker Compose containers.

Evaluation concerns the local search service plus functional query-button and catalog-generator compatibility across endpoints, not external endpoint response times. The search layer remains unchanged when only the endpoint changes; with the same catalog and configuration, repeating search timings for each endpoint is unnecessary. Different catalog contents could affect search performance, and the draft does not claim otherwise. The author confirms cross-endpoint generator checks, but no complete endpoint/action/generator matrix or generation timings were supplied.

Generator queries should be adapted to the endpoint and desired metadata. Configurable page size permits small chunks; row and file-size limits bound exported output. Smaller pages trade smaller responses for more requests; bounds trade catalog coverage for extraction scope. These options do not establish an optimal query or eliminate server-side query cost. Earlier qualitative endpoint responsiveness is omitted from the manuscript as outside evaluation scope.

## Localhost capture and scope clarification — 25 September 2026

The author confirmed localhost measurement and disabled browser caching. The supplied Network-panel screenshot shows six HTTP 200 fetch requests, each with limit=20, in order: neusch 142 ms; italy 117 ms; italy cast 114 ms; neusch 88 ms; muse 129 ms; museum 48 ms. Range 48–142 ms; median 115.5 ms. These are a second sample set, not a replacement or relabeling of the Berlin typing measurements. The screenshot was read directly; request bodies and database execution times are not visible. Browser cache disabling does not establish cold database/OS caches.

The manuscript reports local search-service durations on the loaded database. Catalog source is not requested as a condition for reporting these observations. SPARQL interaction is not timed; functional endpoint compatibility remains separate. No search repetition per remote endpoint is needed with the local catalog and search configuration held fixed.

## Figure, contribution, and reproducibility revision

Both layouts now use the compact editable SVG converted to a vector PDF. The original figure is retained. The introduction explains independent catalog maintenance, vocabulary curation, reuse of the selected IRI across actions, and CSV/template configuration without per-dataset frontend implementation. Related-work distinctions are architectural, with no comparative superiority claim.

The author supplied https://zenodo.org/records/22963871 as the archive for the 17,795,730-entity CSV. The web tool could not access the record during this edit; archive contents, filename, checksum, and license were not independently inspected. No filename, DOI, or archive metadata was inferred. The manuscript and README distinguish Quick Start from the large-catalog import/search path. The exact six-query capture is replayable; the earlier Berlin typing sequence lacks per-request prefixes.

The proposed demonstration now has four preloaded hands-on visitor actions followed by an operator-led catalog/template adaptation walkthrough.

## Current server experiment — supersedes earlier hardware and timings

The latest author correction replaces the manuscript's VMware/8-vCPU/31-GiB environment and earlier timing sets. Current hardware: Intel Xeon Silver 4310 (12 physical cores, 24 hardware threads, 2.10 GHz), 62 GiB RAM; two Samsung 240 GB SSDs in RAID 1, ext4 for PostgreSQL; application/database in Docker Compose. Catalog: 17,795,730 entities loaded. Current screenshot: dublin 707 ms; irlnad 307 ms; irland 1.37 s; paderborn 305 ms; hein nixdor 636 ms; hein nixdorf 420 ms; henin nixdorf 256 ms. All seven visible rows show HTTP 200 and limit=20. Median 420 ms, range 256–1,370 ms. The 17-request footer is not a 17-sample dataset. Earlier cache-disabled setup is retained; a client/server network topology or cold database cache is not inferred for this new server run. Earlier historical notes above are superseded where they conflict.

Current archive URL: https://zenodo.org/records/22963871. The browser tool could not access this record; its contents were not independently inspected. The author supplies the full-snapshot rationale for using the Tentris DBpedia endpoint. DBpedia's official documentation confirms restricted dataset coverage and query limits. The verified configuration key is SPARQL_ENDPOINT. The manuscript now separates this live-exploration requirement from local search measurement.
