# PlantPal - Data Quality & Bias Report

**Audit date:** 22 November 2026. **Status:** Parts A and B completed; Part C finalisation/PDF submission pending. Quality gate: HOLD for promotion of the audited pilot to the intended downstream answer corpus. This is a working report, not the final submission PDF.

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
- **Version/access:** bytes are pinned by checksum; publication/revision dates remain unverified. Existing inventory records personal working copies and no established open redistribution licence. Permission for intended downstream AI use remains N.V.; the Part B review is recorded in Section 6. Original PDFs, full extracted text and rendered pages remain local.
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

**A3 / B1:** The rules below were applied on 22 November 2026. V1 uses explicit register, manifest and PDF checks. V2 reuses Part A visual comparisons after confirming the output and source hashes are unchanged. No model-based semantic score is claimed.

| Rule | Risk / requirement | Checkable condition and evidence | Action if failed |
|---|---|---|---|
| V1 - Valid source references | Incorrect or missing citations; FR2 | For each of all five chunks, source ID, title, URL, filename, hash and one-based integer page must be present and agree with the source register/matching manifest. Page must exist in the referenced PDF and belong to the admitted-page set. Check metadata against the register, manifest and PDF page count. Every record needs a valid reference because each may supply citation evidence. | Hold the affected chunk from downstream use; correct the mapping using the actual source and recheck. Do not fabricate missing fields. |
| V2 - Faithful, usable content | Lost context or changed meaning from extraction/chunking; FR1 and documented Topic 3 preparation risk | For each of all five chunks, text must be non-empty and preserve the cited section's factual wording and heading/body association after documented whitespace cleanup, placeholder removal and heading/order changes. Manually compare with the rendered cited page; flag mid-sentence or detached-heading cuts. Use source/record IDs to document exceptions. This does not require reproducing every source-page element. | Flag for manual review; correct or exclude an affected chunk based on evidence. Do not delete short or oversized-but-intact chunks merely because of length. Missing table/topic coverage is recorded separately, not converted into invented text. |

### B1 - Actual rule results

| Rule | Tested | Pass / Fail / N.V. | Evidence and action |
|---|---:|---|---|
| V1 | 5/5 chunks | 5 / 0 / 0 | Every chunk agrees with the notebook source register and Part C manifest; actual source hashes match; integer pages exist and are admitted. No record requires reference repair. |
| V2 | 5/5 chunks | 5 / 0 / 0 | Reused documented visual review of all five unchanged chunks against S01 p5/p10 and S03 p6. Selected prose and headings remain faithful; no broken-sentence cut observed. No chunk is removed. Missing table content is a coverage gap, not a fabricated-text failure. |

[Part B evidence](../data/inspection/week4_part_b_validation.json) records every ID and V1 subcheck, V2 review basis, denominators and scope. A V2 pass establishes fidelity of selected text, not complete coverage or independent gardening correctness. The 656-character chunk passes because its complete section exceeds a soft target; the 166-character section is valid too.

## 4. Duplicate, Anomaly and Coverage Findings

**Observed:** all five IDs and whitespace-normalised/case-folded texts are distinct (Part A evidence). No exact duplicates were found. Semantic duplication was not assessed. Short or oversized intact chunks are documented exceptions, not automatic defects.

**B2 - Two FR1-relevant categories:** inspection unit is a chunk; all five were reviewed. These counts describe this pilot, not the full NParks collection.

| Category | Expected evidence | Observed evidence / gap | Possible downstream effect |
|---|---|---|---|
| General indoor growing conditions | Documented light, water and space principles | 1/5 chunks, `S01-p05-0001`, covers these three topics. It gives general guidance, not species-specific intervals. | Can support selected general questions; cannot justify universal fixed watering schedules. |
| Plant-specific care comparisons | Correctly associated named-plant profiles covering comparable care attributes | 0/5 chunks provide complete profiles supporting such comparisons. S02 was deferred because headings/bodies extract ambiguously. Incidental plant examples elsewhere are not comparison-ready profiles. | FR1 plant comparisons could be unanswerable or tempt unsupported generalisation; later test-set coverage must reflect this gap. |

Other observed content: three chunks discuss growing media/soil; one gives general plant-choice advice. S03-p06-0005 omits the visible ratio table, so ratio-based questions are not supported. Categories are task-focused evidence groups, not class-balance or fairness scores.

## 5. Bias Assessment

**Inferred risk - pipeline-induced and representation bias:** manual selection admits easy-to-extract general prose while deferring complex species profiles and omitting the soil table. This can skew the prepared collection toward general advice and away from concrete comparisons/structured guidance. Later retrieval might surface generic passages for species-specific questions, and generation might overgeneralise if it does not acknowledge missing evidence.

**Evidence chain:** documented S02 extraction limitation and S03 table loss → 0/5 comparison-ready profiles and omitted ratios → possible unsupported/uneven answers across FR1 tasks → verify layout associations, admit reviewed content only when use is authorised, maintain a coverage register, and test unsupported-question abstention before user-facing use. This is a plausible downstream risk, not observed model behaviour or demonstrated unfairness. No demographic fairness claim can be made from five text chunks without users, labels or model evaluation.

## 6. Privacy, Rights and Governance

**B3 review, 22 November 2026:**

| Topic | Finding / status | Safeguard or responsibility |
|---|---|---|
| Provenance/version | **Observed:** NParks sources S01/S03, exact filenames/URLs/hashes and selected pages map to the audited Part C output; fingerprints match. **N.V.:** authoritative publication/revision dates and latest-edition status. | Student maintainer records verified dates when available; revalidates on source/configuration change instead of treating download date as freshness. |
| Rights | **Observed:** official [Terms of Use](https://gardeningsg.nparks.gov.sg/terms-of-use/), page dated 26 June 2026, reviewed on audit date, reserve rights and describe limited personal non-commercial use. The terms also restrict other use and automated copying. **N.V.:** permission covering the intended AI processing/service and redistribution. No written authorisation is held in this repository. | Do not treat public access as an open licence or the audit as permission. Resolve intended-use permission with the rights holder, or choose appropriately licensed alternatives, before further acquisition/expansion or downstream use. No contact was sent as part of this review. |
| Privacy | **Observed:** manual review of all five prepared prose records found no personal identifiers, private user messages or sensitive individual records. This conclusion does not cover every raw-PDF element or future user input. | Keep raw PDFs, extracted text and source renderings local/ignored; share original observations and metadata only. Review any future source or user-data additions separately. |
| Consent/collection basis | No human participants or user data are represented in the five chunks, so participant consent is not applicable to this sample. Public-document access does not settle copyright or intended-use permission. | Preserve provenance and notices; resolve rights separately rather than claiming consent from availability. |
| Maintenance | Student project owner is the responsible maintainer; NParks is the source publisher, not PlantPal's quality reviewer. | Review before corpus expansion or downstream evaluation and when sources, terms, parsing settings, requirements or reported errors change; version corrected outputs and rerun checks. |

The terms review informs a conservative engineering gate, not a legal determination. Earlier local pipeline execution is not proof of authorisation for broader use. Raw sources and full extracted text have not been newly published during this audit.

## 7. Mitigation and Impact on Requirements

**B4 priorities:** proposed actions, not completed remediation.

| Priority | Action, owner and timing | Requirements/evaluation affected | Evidence needed and residual risk |
|---|---|---|---|
| 1 - Resolve rights and source currency | Student project owner documents permission for the intended processing/sharing scope, or selects suitably licensed replacements, **before further acquisition/expansion or downstream AI use**. Verify publication/revision information and agree a task-based freshness review trigger. | FR1 approved-source availability; FR2 traceable provenance; later answer/citation evaluation depends on an admissible corpus. | Written permission or applicable licence covering intended use, source register and verified versions (or explicitly justified remaining uncertainty). Permission alone does not prove accuracy. |
| 2 - Repair task coverage and verify source fidelity | After rights resolution, student maintainer reviews plant-profile layout and structured soil guidance, or substitutes authorised sources. Build a task-to-evidence coverage list and rerun V1/V2 **before claiming support for comparisons or ratios**. | FR1 comparisons; FR2 citation support; NFR2 correctness and RAI1 grounding/abstention evaluation could otherwise be distorted by unanswerable test cases. | Reviewed profile/attribute mappings and table values, revised manifest and actual rule results; later answerable/unsupported cases explicitly distinguished. Source bias and model/retrieval errors may remain. |

Residual risks include a small single-publisher corpus, manual review error, missing source revisions, unresolved semantic redundancy and untested retrieval/generation. No Week 2 application metric has been achieved merely by passing data checks.

## 8. Quality-Gate Decision

**HOLD — promotion of this five-chunk NParks pilot to the intended PlantPal downstream answer corpus/public AI service.** This gate is scoped to downstream dataset use, not a claim that the coursework audit or pipeline execution failed.

Evidence supporting the decision:

1. **Observed:** V1 and V2 pass 5/5; prepared text is traceable and faithful within its selected scope. These checks do not resolve usage permission or missing tasks.
2. **Not Verified:** permission for intended downstream AI use is unresolved; publicly downloadable content is not established as openly licensed.
3. **Observed:** 0/5 comparison-ready profiles, S02 deferred and S03's table missing; the pilot cannot support the full FR1 task range. Source currency is also not verified.

The two priorities in Section 7 must be addressed before re-review. Do not promote the pilot, publish full source-derived text or claim complete FR1 support while on HOLD. The metadata-only audit and proposal may still document these actual findings; Part C report/PDF preparation can proceed without lifting this dataset gate.

**Re-review triggers:** documented intended-use permission or authorised replacement sources; reviewed evidence for the proposed supported tasks (or an explicitly agreed narrower scope); verified source/version status with a justified maintenance plan; new manifests and passing V1/V2 checks for the revised artifact. Source/configuration changes or newly reported errors trigger revalidation. Only then select a new scoped GO / GO WITH CONDITIONS / HOLD decision from the evidence.

**Part C remains pending:** concise final report, PDF export for eLearning, final README/repository verification and submission. This intermediate Part B commit is not an eLearning submission.

Lab basis: Topic 4 Lab, A1-A3 pp. 3-4, B1-B4 pp. 5-6, report headings p. 7. Public supporting evidence contains metadata and original observations only.
