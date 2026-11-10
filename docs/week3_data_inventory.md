# PlantPal - Week 3 Data Inventory

**Date:** 10 November 2026

**Stage:** Topic 3, Part A (A1-A4)

**Execution status:** All eight code cells of [week3_pipeline.ipynb](../notebooks/week3_pipeline.ipynb) executed sequentially in local Python. The notebook is VS Code/Jupyter-ready and also supports Colab. No Colab runtime execution or VS Code UI execution is claimed. Local runtime details and actual results are recorded in the [metadata-only inspection report](../data/inspection/week3_part_a_inspection.json).

## A1 - Requirements to Data Needs

| Requirement ID | Needed information / feature | Selected sources | Why usable / constraint |
|---|---|---|---|
| FR1 | Supported gardening guidance about light, watering principles, media and space | S01, S02; relevant portions of S03 | NParks documents fit the tropical home-gardening domain. Source content outside PlantPal's task boundaries does not expand the application scope. |
| FR2 | Document title, official URL and one-based PDF page identity | S01-S03 plus the source register | Page-by-page extraction retains provenance for eventual citations. A byte hash identifies an exact snapshot, not truth or rights. |
| RAI1 | Evidence supporting claims and explicit limitations where evidence is absent | S01-S03 compared with visible original pages | Reading order, hidden text and icon loss can affect whether citations support an answer. Successful extraction does not establish full suitability. |

This extends architecture element **A5 Approved Sources** and prepares inputs for **A4 Knowledge Access**. It supports source-verification work under O1 and future correctness/citation-support evaluation under O3. User-needs interviews, a fully verified corpus, and model evaluation remain pending. The additional datasets in [the research shortlist](dataset_references.md) remain candidates, not admitted data.

## A4 - Source Inventory

| Source ID | Filename / URL | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | `introduction_to_indoor_gardening.pdf`; [official PDF](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf) | Unstructured PDF text. Primary indoor-care guide; light, space, water and growing media. | NParks; creation metadata `D:20201013090212+08'00'`; accessed 10 November 2026. | Public download; personal inspection copies only. No open redistribution licence established; see rights notes below. | 24 pages; page 2 has zero extracted characters and is visually a photograph. Pages 5/10 sampled; hidden editorial content on page 10. |
| S02 | `know_10_houseplants.pdf`; [official PDF](https://isomer-user-content.by.gov.sg/316/43fdd8a1-d385-428f-8cc2-d5b9b36f6a38/know%2010%20house%20plants.pdf) | Unstructured PDF text. Species-level candidate source with ten houseplant profiles. | NParks; creation metadata `D:20230127115509Z`; accessed 10 November 2026. | Public download; personal inspection copies only. No open redistribution licence established; see rights notes below. | 2 pages; both contain extractable text. Page 2 has multi-column profiles; extracted order and grouped name headings differ from the layout. |
| S03 | `introduction_to_community_gardening.pdf`; [official PDF](https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf) | Unstructured PDF text. Supplementary growing guidance; community-garden sections need scope filtering. | NParks; creation metadata `D:20220602102149+08'00'`; accessed 10 November 2026. | Public download; personal inspection copies only. No open redistribution licence established; see rights notes below. | 20 pages; no empty-text pages. Pages 5/12 sampled; icon-based care information is not represented as linked plain-text attributes. |

PDF creation timestamps are file metadata, **not confirmed publication dates or evidence of current advice**. An edition number has not been verified; the SHA-256 values below identify the inspected snapshots.

## A2 - Workspace and Source Identity

The local workspace is the PlantPal repository. In VS Code, open the repository folder and select a Python kernel for the notebook. In Colab the same setup cell uses `/content/week3_project`.

| Storage | Purpose | GitHub policy |
|---|---|---|
| `data/raw/` | Three original personal working-copy PDFs, unchanged | Ignored by Git; retain source notices. |
| `data/processed/` | Reserved for later prepared data | Created but no Part B output is claimed; ignored by Git. |
| `data/inspection/week3_part_a_inspection.json` | Part A counts, fingerprints, metadata and observed-check results | Included; no full source text or page images. Not the Part B/C pipeline manifest. |
| `notebooks/week3_pipeline.ipynb` | Setup, acquisition/verification, inspection and short displayed samples | Included with real local outputs; absolute local workspace paths redacted. |

All three downloads were verified as PDFs and loaded successfully. The notebook selects exact filenames instead of taking the first `.pdf` found. It stops if a source's expected hash changes, a PDF is unreadable/encrypted, or a source contains no extractable text. A changed source requires a new review rather than silently inheriting the old inventory.

| Source | Bytes | PDF pages | Extracted characters | Empty-text pages | SHA-256 |
|---|---|---|---|---|---|
| S01 | 3,178,940 | 24 | 13,273 | 2 | `21d6ae22ac7f4bbebfa38225d1fb942d2210376a119d350146fc15888a573533` |
| S02 | 1,720,974 | 2 | 9,439 | None | `2208509f38b4c3400270c06b3c20a7c2ddd1812ce4433a2fe3e4dd0b9bd60120` |
| S03 | 2,450,552 | 20 | 7,762 | None | `33a4f05c6a55d110e2bcda45562c928b7edd440d750e214e1183717b30ab0096` |

Character counts use `len(page.extract_text() or '')` with pypdf 6.10.0, including extracted whitespace. They are inspection measurements, not measures of accuracy or token counts. Total: **3 files, 46 PDF pages**.

## A3 - Representative Inspection Evidence

The notebook displays short loaded-text samples and character counts for these actual pages. The full text stays in memory. PDF page numbers below are one-based file positions rather than assumed printed page labels.

| Source / subset | What was inspected | Observed result | Implication for later preparation |
|---|---|---|---|
| S01, page 5 | Indoor garden considerations | Text contains several topic blocks rather than a single continuous paragraph. | Preserve the topic headings and page identity when preparing passages. |
| S01, page 10 | Growing-media discussion and two illustrated material descriptions | A hidden editorial image-placeholder sentence is present in extracted text but not visible in the rendered page. | Flag it as an extraction artefact. Any removal belongs to a documented Part B cleaning decision. |
| S02, page 1 | Brochure introductory material | Extracted material includes institutional/contact information and introductory gardening text. | Distinguish useful scope context from repeated contact/footer content later. |
| S02, page 2 | Ten houseplant profiles | Visible page is a grid. Extraction starts with the bottom-right profile and puts several common-name headings together near the end. | Do not attach plant names to the next paragraph solely by linear text position. Compare layout-aware methods and preserve scientific names. |
| S03, page 5 | Mixed planning and growing-condition blocks | Relevant light/soil information shares a page with community participation planning. | Select relevant sections without treating the whole page as universally applicable home-care guidance. |
| S03, page 12 | Illustrated plant entries | Names are readable, but sun/water care icons are not extracted as corresponding text fields. | Do not infer species-level care values from plain text alone. Verify symbols and their association or exclude those claims. |

Additional visual checks: S01 page 2 is a photograph, explaining its empty extraction. S03 page 11 provides an icon legend; page 9 includes an excluded chemical-control topic. These pages illustrate why the raw corpus must be scoped before use. No full-document factual audit or verified list of ten supported plants is claimed.

Visual comparisons were performed on local renderings, separate from the notebook's text extraction. Source page images remain private working artefacts. Automated snapshot checks in the notebook reproduce the empty-text page, hidden editorial text, S02 start-of-page order, and presence of a sample S03 plant name. They do not replace manual layout review.

## Access and Rights Review

The [official NParks resource directory](https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/) lists all three documents. The [GardeningSG terms](https://gardeningsg.nparks.gov.sg/terms-of-use/) were reviewed on 10 November 2026. They describe personal non-commercial use while reserving other uses and reproduction rights. No open redistribution licence has been established for these files. File metadata is not a licence.

The PDFs remain personal local working copies with their notices intact. The public repository contains code, links, metadata, limited excerpts and original inspection observations, not source PDFs, full extraction or page images. Permission for public deployment, model training, redistribution, and publishing prepared source text is **not established** by this inspection. Review those uses before later stages. This records an access constraint, not a legal assurance.

## Preparation Pathway Decision for Part B

**Select pathway A: PDF/TXT documents.** PlantPal remains a text-based, document-grounded assistant. Embedded photos/icons do not automatically justify building an image-recognition pipeline.

- Start from raw, unchanged copies and preserve document/page identifiers.
- Compare simple extraction with heading/layout-aware handling where reading order is unreliable, especially S02.
- Record any later whitespace or editorial-text cleanup and compare before/after samples.
- Preserve warnings and conditions. Exclude unsupported symbol-only claims unless their association can be verified.
- Review source coverage and scope before admitting passages; S03 is supplementary, not a blanket expansion to community-garden or chemical advice.
- Defer chunk-size selection, prepared JSONL export, embeddings and the executable V1 transformation pipeline to Parts B/C.

No preparation comparison has yet been performed, so no method is claimed to be the best. The current Part A report is not a cleaned corpus or a completed answer dataset.

## Completion Checkpoint

- [x] Actual PlantPal sources selected and linked to three Topic 2 requirements.
- [x] Source identity, filenames, access notes and fingerprints recorded.
- [x] Local workspace initialised; selected inputs verified and loaded.
- [x] Three files and six representative page subsets inspected; short loaded samples saved in notebook outputs.
- [x] Layout/ingestion limitations recorded and a relevant Part B pathway selected.
- [x] Notebook and metadata-only inventory/evidence prepared for the existing repository.
- [ ] Run the same notebook in a connected Colab runtime if required for the course platform checkpoint. The user requested VS Code/local notebook work for this stage.
- [ ] Complete Topic 3 Parts B and C separately.

The repository can show completed local Part A ingestion/inspection, but cannot claim the Colab platform checkpoint or later pipeline work has been completed.
