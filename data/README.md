# Data handling

The initial corpus is defined in [the project scope](../docs/week1_project_scope.md#data-sources).

This folder now includes metadata-only Week 3 Part A inspection evidence. Three personal working-copy PDFs were inspected locally and remain ignored under `data/raw/`. Store permitted local downloads in `data/raw/` and extracted content in `data/processed/`; both are ignored by Git. Record source URL, publisher, title, retrieval date, version, checksum, and usage terms when ingestion begins. Preserve document/page identifiers for citations. Do not assume that a public URL grants redistribution rights.

## Dataset and Source References

See the [research shortlist](../docs/dataset_references.md) for NParks guides, the Indoor Plants Dataset, Plantational/EcoSage, Plantfolio, and the NParks compendium, with access links and review notes. The three original NParks PDFs have now been downloaded and inspected locally for Week 3 Part A. Other shortlisted datasets remain unacquired candidates. Inspection does not admit all source content into the answer corpus.

## Part A Inspection Evidence

See [inspection report](inspection/week3_part_a_inspection.json) and [data inventory](../docs/week3_data_inventory.md). Part A evidence is retained separately from the Part B outputs below. Public notebook outputs contain limited samples, not full source text.

## Part B Prepared Data

[Comparison evidence](inspection/week3_part_b_comparison.json) records the two chunking methods. [Common manifest](week3_manifest.json) records two sources contributing to one prepared JSONL file, their hashes, admitted pages and processing limitations. Five chunks cover S01 pages 5/10 and extracted prose from S03 page 6. S02 is deferred; the S03 soil-ratio table is missing from extraction and is not reconstructed.

Run all notebook cells to recreate `data/processed/prepared_text.jsonl` and the two local candidate JSONL files. These outputs contain source text and are ignored by Git. The public manifest references local files that will not exist in a fresh clone until regeneration. Metadata and code are public; source copies and extracted text are not redistributed. Part C remains pending.
