# PlantPal - Data Quality & Bias Report

**Audit date:** 22 November 2026. **Status:** Part A (A1-A3) completed; Parts B and C pending. This is a working report, not the final submission PDF. No overall quality-gate decision has been made.

## 1. Project and Data Overview

PlantPal is a proposed document-grounded assistant for beginner tropical home gardeners. It aims to answer supported English questions with source citations and acknowledge missing coverage.

**A1 - Requirements:** From [Week 2 requirements](week2_requirements.md):

| ID | Existing requirement | Data needed |
|---|---|---|
| FR1 | Answer supported English questions about light, watering principles, growing media, and space, including comparisons between supported plants, using approved documents; do not invent unsupported care instructions, species details or fixed watering schedules. | Readable, correctly associated gardening passages covering the requested topics and plant comparisons; explicit coverage limits. |
| FR2 | Attach a document title, source URL and one-based PDF page reference to each factual gardening claim, allowing shared citations when appropriate; do not fabricate sources or present unsupported claims as approved evidence. | Accurate source identity and page metadata attached to every prepared chunk. This audit checks data prerequisites, not generated-answer compliance. |

- **Pathway:** A, PDF/TXT. Audited artifact: Topic 3 **Part C**, `data/pipeline_v1/documents/prepared_text.jsonl` (local, ignored by Git).
- **Matching manifest:** [pipeline_manifest.json](../data/pipeline_v1/documents/pipeline_manifest.json), pipeline `plantpal-week3-v1`, run timestamp `2026-11-10T15:27:12.681899+00:00`.
- **Output SHA-256:** `66f82bdf2112360c8f4f1f7e5aba86e63951280e6aa2bd067e4d8a6221181204`. Rechecked on the audit date; output and both contributing source hashes match the manifest. The pipeline was not rerun or modified for this audit.
- **Population/sample:** five prepared chunks; inspect all five (a census of the pilot). They represent three selected PDF pages from two documents, not the complete original collection. No claim about unselected pages or the entire intended knowledge base follows from this sample.
- **Sources:** NParks S01, *Introduction to Indoor Gardening*, pages 5/10; S03, *Introduction to Community Gardening*, page 6 prose. Exact URLs, source hashes and ownership are in the manifest and [inventory](week3_data_inventory.md). S02 remains deferred.
- **Version/access:** bytes are pinned by checksum; publication/revision dates remain unverified. Existing inventory records personal working copies and no established open redistribution licence. Current permission for broader use is N.V.; Part B will review responsible-data implications. Original PDFs, full extracted text and rendered pages remain local.
- **Evidence:** [Part A inspection record](../data/inspection/week4_part_a_inspection.json), [Week 3 decisions](week3_pipeline_decisions.md), local prepared records and visual comparison with all three source pages on 22 November 2026.

**A1 checkpoint:** Incomplete species-specific evidence could prevent FR1 plant comparisons. Missing soil-ratio table content could prevent an evidence-supported mixing-ratio answer. Valid citation metadata alone does not fill those gaps; the assistant would need to acknowledge missing support.

## 2. Five-Dimension Quality Scorecard

**A2:** Labels distinguish observed evidence from inferred application risks. Pass means only that the stated scoped check is satisfied; it is not a whole-system acceptance result.

| Dimension | Finding and evidence | Potential task impact | Decision |
|---|---|---|---|
| Completeness | **Observed:** 5/5 chunks contain non-empty record ID, text, source ID/file, title, URL, page and source hash. General space/light/water/media prose exists. S03 p6's visible soil-ratio table is absent from the prepared record; S02 profiles are deferred. | **Inferred risk:** metadata completeness may hide missing task knowledge; full FR1 comparisons and table-based answers are unsupported by this pilot. | **Warning:** complete required fields, incomplete task coverage. |
| Consistency | **Observed:** 5/5 share the same schema; title, URL, filename and source hash agree with their source manifest entry; all pages belong to the declared selected-page set. Output and source fingerprints match the run manifest. | Supports FR2 traceability and reduces mismatched-source citations; does not establish claim support. | **Pass** for inspected metadata consistency. |
| Accuracy | **Observed:** all five chunks were compared with rendered S01 p5/p10 and S03 p6. Selected prose and heading/body associations are preserved; whitespace and documented heading/order changes do not add claims. The removed hidden editorial placeholder is not visible source guidance. S03 table content remains omitted, not invented. | Source fidelity supports FR1/FR2. Independent horticultural correctness and complete extraction have not been established. | **Pass** for selected-prose fidelity; completeness warning remains. |
| Timeliness | **Not Verified:** acquisition/run timestamps identify processing, not publication freshness. No verified revision dates or explicit data-age acceptance criterion were established in the reviewed requirements/inventory. No live latest-version comparison was performed in Part A. | Cannot claim the guidance is current merely because it was downloaded recently; a later revision might change evidence. | **N.V.** Verify versions and define a justified review trigger. |
| Uniqueness | **Observed:** five unique IDs and five distinct text values after whitespace normalisation and case folding; zero duplicate records beyond the first under either check. | Avoids exact duplicate chunks dominating later retrieval. Near-duplicates and semantic redundancy are not measured by this check. | **Pass** for ID and normalised-exact-text uniqueness only. |

### Item-level manual inspection evidence

| Record ID | Source page | Characters | Observed content and exception |
|---|---|---:|---|
| S01-p05-0001 | S01 p5 | 466 | Space, light and watering prose retains the corresponding headings. |
| S01-p05-0002 | S01 p5 | 166 | Plant-choice advice is a complete section. Short length is not a defect. |
| S01-p10-0003 | S01 p10 | 656 | General media prose remains intact. Exceeding 500 characters is the documented soft-target exception, not automatic failure. |
| S01-p10-0004 | S01 p10 | 307 | Charcoal and coco-chip descriptions remain associated with their own headings. |
| S03-p06-0005 | S03 p6 | 399 | Soil definitions/general prose is retained; title and prose order differ as documented. The table is absent and cannot be treated as available evidence. |

## 3. Validation Findings

**A3 - Rule definitions only.** Formal Part B application/results are pending. Part A observations above and existing Week 3 checks may be reused as evidence; no new pipeline or standalone Week 4 notebook is needed.

| Rule | Risk / requirement | Checkable condition and evidence | Action if failed |
|---|---|---|---|
| V1 - Valid source references | Incorrect or missing citations; FR2 | For each of all five chunks, source ID, title, URL, filename, hash and one-based integer page must be present and agree with the source register/matching manifest. Page must exist in the referenced PDF and belong to the admitted-page set. Check metadata against the register, manifest and PDF page count. Every record needs a valid reference because each may supply citation evidence. | Hold the affected chunk from downstream use; correct the mapping using the actual source and recheck. Do not fabricate missing fields. |
| V2 - Faithful, usable content | Lost context or changed meaning from extraction/chunking; FR1 and documented Topic 3 preparation risk | For each of all five chunks, text must be non-empty and preserve the cited section's factual wording and heading/body association after documented whitespace cleanup, placeholder removal and heading/order changes. Manually compare with the rendered cited page; flag mid-sentence or detached-heading cuts. Use source/record IDs to document exceptions. This does not require reproducing every source-page element. | Flag for manual review; correct or exclude an affected chunk based on evidence. Do not delete short or oversized-but-intact chunks merely because of length. Missing table/topic coverage is recorded separately, not converted into invented text. |

Part B will record the denominator, passes/fails/N.V., supporting item references and justified action for each rule.

## 4. Duplicate, Anomaly and Coverage Findings

Part B synthesis pending. Part A observations are recorded in Section 2; two-category coverage assessment has not yet been completed.

## 5. Bias Assessment

Pending Part B: distinguish a plausible source/preparation risk from demonstrated system unfairness.

## 6. Privacy, Rights and Governance

Pending Part B responsible-data review. Existing access/provenance status is recorded in Section 1; no new permission has been assumed.

## 7. Mitigation and Impact on Requirements

Pending Part B: prioritise two actions, assign responsibility/timing and document residual risk.

## 8. Quality-Gate Decision

**Pending Part B.** No GO, GO WITH CONDITIONS or HOLD decision has been assigned. Part C will finalise the report, export the submission PDF and verify the repository handoff.

Lab basis: Topic 4 Lab, Part A A1-A3 (pp. 3-4); final report structure follows p. 7. Existing artifacts are linked above; no full source text or source-page images are included in this public report.
