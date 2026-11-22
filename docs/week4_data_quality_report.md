# Home Garden Companion - Data Quality & Bias Report

**Individual project | Topic 4 | Audit and finalisation: 22 November 2026**

**Status:** Parts A-C report preparation complete. E-learning submission remains pending. **Gate: HOLD** for promotion of this pilot to the intended downstream answer corpus/service. The pipeline and audit are completed evidence, not a finished AI application.

## 1. Project and Data Overview

Home Garden Companion proposes document-grounded guidance for beginner tropical home gardeners. This audit examines data prerequisites for two Topic 2 requirements: **FR1**, supported light/water/media/space guidance and plant comparisons without invented care instructions; and **FR2**, truthful document-title, URL and one-based PDF-page citations for factual claims. No generated-answer compliance is measured.

**Pathway A (PDF/TXT), Topic 3 Part C:** audit `data/pipeline_v1/documents/prepared_text.jsonl` against its matching `data/pipeline_v1/documents/pipeline_manifest.json`. Pipeline: `home_garden_companion-week3-v1`; run: 10 November 2026, 15:27:12 UTC. Exact output fingerprint and evidence references appear in Appendix A.

**Population and sample:** all **5/5 prepared chunks**, spanning three selected pages of two NParks documents: S01, *Introduction to Indoor Gardening*, pages 5/10; S03, *Introduction to Community Gardening*, page 6 prose. The unit is one chunk. This is a census of the small pilot, not the full source collection. S02 houseplant profiles remain deferred.

The output and both source hashes match the manifest. Raw PDFs, extracted text and page images stay local; public evidence is metadata and original observations. Publication/revision dates and permission for intended downstream AI use are **Not Verified (N.V.)**. Missing plant profiles could prevent FR1 comparisons; the missing soil table could prevent supported ratio answers. Valid citation fields do not fill those gaps.

## 2. Five-Dimension Quality Scorecard

Observed findings use all five records plus rendered source pages. Decisions apply only to the stated checks; inferred effects are not measured model outcomes.

| Dimension | Finding / evidence | Task impact and decision |
|---|---|---|
| Completeness | Observed: 5/5 have non-empty text and required citation/identity fields. S03 p6's ratio table is absent; S02 profiles are deferred. | FR1 coverage remains incomplete despite complete fields. **Warning.** |
| Consistency | Observed: 5/5 share a schema; source title, URL, filename, hash and admitted page agree with the manifest. Source/output hashes match. | Supports FR2 traceability. **Pass** for scoped metadata checks. |
| Accuracy | Observed: all five chunks preserve selected prose and heading associations on S01 p5/p10 and S03 p6 after documented cleanup/order changes. | **Pass** for selected-prose fidelity. Complete extraction and independent gardening correctness are not established. |
| Timeliness | N.V.: no verified publication/revision dates, latest-edition check or explicit task-based data-age criterion. Run/download dates are not publication dates. | Cannot claim current advice. **N.V.** Verify versions and review triggers. |
| Uniqueness | Observed: 5 unique IDs and 5 distinct whitespace-normalised, case-folded text values; no duplicate beyond the first. | **Pass** for exact-normalised duplicates; semantic redundancy not assessed. |

<!-- pagebreak -->

## 3. Validation Findings

**V1 - Valid source references (FR2):** every record must have source ID, title, URL, filename, hash and integer page agreeing with the notebook register and matching manifest. The page must exist in the actual PDF and be admitted. Failure holds the affected chunk for reference repair and recheck.

**V2 - Faithful, usable content (FR1 / extraction risk):** every record must contain non-empty text preserving cited factual wording and heading/body associations after documented whitespace cleanup, placeholder removal and heading/order changes. Compare against rendered source pages; flag broken sentences or detached headings. Failure requires manual review, correction or justified exclusion, not automatic deletion by length.

| Rule | Tested | Pass / Fail / N.V. | Evidence and action |
|---|---|---|---|
| V1 | 5/5 | 5 / 0 / 0 | Executable checks against notebook register, manifest, source hashes and actual PDF page counts. No reference repairs needed. |
| V2 | 5/5 | 5 / 0 / 0 | Reused Part A visual review after verifying unchanged source/output fingerprints. No invented prose or broken section observed; no chunks removed. |

The [Part B evidence](../data/inspection/week4_part_b_validation.json) records per-item results. V2 is a documented manual review, not an automatic semantic score. Missing source-page content is a separate coverage issue; a pass does not imply complete extraction.

## 4. Duplicate, Anomaly and Coverage Findings

No exact-normalised duplicates were observed. The 166-character plant-choice chunk is a complete short section; the 656-character media chunk exceeds the **500-character soft target** to preserve a section. Both are valid exceptions, not defects. Other chunk lengths are 466, 307 and 399 characters.

| FR1 category | Needed evidence | Observed coverage across 5 chunks | Possible downstream effect |
|---|---|---|---|
| General indoor conditions | Light, water and space principles | 1/5: S01-p05-0001 covers all three, without plant-specific schedules. | Supports selected general questions; cannot justify universal watering intervals. |
| Plant-specific comparisons | Correctly linked named-plant profiles with comparable care attributes | 0/5 complete comparison-ready profiles; S02 is deferred. Incidental species/group examples are not full profiles. | Comparisons may be unanswerable or encourage unsupported generalisation. |

The other records provide three media/soil chunks and one plant-choice chunk. S03-p06-0005 lacks the source's soil-ratio table. Counts describe the prepared pilot only, not all information in NParks sources.

## 5. Bias Assessment

**Inferred pipeline-induced/representation risk:** selecting easily extracted prose while deferring complex profiles and omitting a table skews evidence toward general advice. The chain is: **selection/layout loss → missing profiles and ratios → potentially generic or unsupported retrieval/generated answers → coverage review and controlled admission**. Review source layouts and authorised alternatives, maintain task-to-evidence mappings, and later test abstention on unsupported questions. This is a plausible risk, not observed model behaviour or proven unfairness. Five chunks without user/model results cannot establish demographic fairness.

<!-- pagebreak -->

## 6. Privacy, Rights and Governance

**Provenance/version - Observed:** NParks S01/S03 ownership, URLs, selected pages and fingerprints map to the exact Part C output. **N.V.:** authoritative revision dates and current-edition status. A matching hash proves snapshot identity, not truth or currency.

**Rights - Observed:** the official [NParks terms](https://gardeningsg.nparks.gov.sg/terms-of-use/), stated update 26 June 2026, were reviewed on 22 November 2026. They reserve rights, describe limited personal non-commercial use and restrict other use and automated copying. **N.V.:** authorisation for the intended AI processing/service or redistribution; no written permission is recorded. Public availability and prior local execution do not establish that permission. This is an engineering access review, not a legal determination.

**Privacy/collection - Observed:** manual review found no personal identifiers, private user messages or sensitive individual records in the five prepared chunks. This does not cover every raw-PDF element or future inputs. Participant consent is not applicable to these public-document prose records; copyright/intended-use permission is a separate unresolved question.

**Safeguards and owner:** the student project owner maintains the register, preserves notices and keeps source PDFs, extracted text and page images local/ignored. Publish only permitted evidence. Resolve rights before further acquisition/expansion or downstream use; no permission request was sent during this audit. Revalidate when sources, terms, configuration, requirements or reported errors change, and before downstream evaluation. NParks is the publisher, not Home Garden Companion's quality reviewer.

## 7. Mitigation and Impact on Requirements

| Priority / owner / timing | Action and evidence required | Impact and residual risk |
|---|---|---|
| 1. Student maintainer; before further acquisition/expansion or downstream AI use | Document permission covering intended processing/sharing, or select suitably licensed replacements. Verify source dates/versions and establish a justified freshness-review trigger. | FR1 approved evidence and FR2 provenance depend on admissible sources. Permission does not establish accuracy. |
| 2. Student maintainer; after rights resolution, before claiming comparisons/ratios | Verify plant-profile layout and structured soil guidance, or use authorised substitutes. Build task-to-evidence mappings; rerun V1/V2 and version the resulting manifest. | FR1/FR2, NFR2 correctness and RAI1 grounding/abstention evaluation are affected. Manual errors, source bias and later model errors can remain. |

These are proposed actions, not completed remediation. Remaining risks include limited single-publisher coverage, unverified revisions, semantic redundancy and untested retrieval/generation. No Topic 2 application threshold is achieved by these data checks alone.

## 8. Quality-Gate Decision

**HOLD: promotion of this five-chunk pilot to the intended Home Garden Companion downstream answer corpus/public AI service.** V1/V2 pass 5/5, but intended-use permission remains N.V.; comparison-ready profiles are absent, the soil table is missing and currency is unverified. Structural quality does not resolve these blockers.

Do not promote the pilot, redistribute full extracted text or claim complete FR1 support while on HOLD. The metadata-only audit and proposal can document the findings; this gate does not invalidate completed pipeline/audit work or prevent report submission.

**Re-review requires:** documented applicable permission or authorised replacements; reviewed evidence for supported tasks or an explicitly agreed narrower scope; justified source-version/freshness handling; and revised manifests with passing V1/V2 results. Then select a new scoped gate from the evidence. New source/configuration changes or reported errors also trigger revalidation.

<!-- pagebreak -->

## Appendix A - Supporting Evidence and Traceability

Main report: three pages. This appendix is supporting evidence, not additional audit scope. Full source text and source-page images are not reproduced.

| Record | Source/page | Characters | Manual-review observation |
|---|---|---:|---|
| S01-p05-0001 | S01 p5 | 466 | Space/light/water prose retains associated headings. |
| S01-p05-0002 | S01 p5 | 166 | Complete plant-choice section; short length accepted. |
| S01-p10-0003 | S01 p10 | 656 | Complete media section; documented soft-target exception. |
| S01-p10-0004 | S01 p10 | 307 | Charcoal/coco-chip descriptions retain their own headings. |
| S03-p06-0005 | S03 p6 | 399 | Definitions/prose preserved with documented order change; table absent. |

**Inspected output SHA-256:**

`66f82bdf2112360c8f4f1f7e5aba86e63951280e6aa2bd067e4d8a6221181204`

**Evidence index (repository-relative paths):**

- [Week 2 requirements](week2_requirements.md) and [evaluation criteria](week2_evaluation_criteria.md): original FR1/FR2 and later NFR2/RAI1 targets.
- [Source inventory](week3_data_inventory.md): source URLs, owners, PDF metadata, access history and source SHA-256 values.
- [Pipeline decisions](week3_pipeline_decisions.md): selected pages, cleanup, chunking and accepted limitations.
- [Part C manifest](../data/pipeline_v1/documents/pipeline_manifest.json): exact run, configuration, source/output hashes and mappings.
- [Part A inspection](../data/inspection/week4_part_a_inspection.json): population, fields, schema, duplicate checks and manual-review scope.
- [Part B validation](../data/inspection/week4_part_b_validation.json): per-record V1/V2 results, coverage, rights review and scoped gate.
- [Topic 3 notebook](../notebooks/week3_pipeline.ipynb): source register and actual pipeline execution; not rerun for this audit.

**Source documents:** NParks S01, *Introduction to Indoor Gardening* (PDF pp. 5, 10); S03, *Introduction to Community Gardening* (PDF p. 6). Official download URLs are recorded in the inventory and manifest. Rendered-page fidelity review: 22 November 2026. S02, *Know 10 Houseplants*, is inspected but not admitted to this pilot.

**Assignment basis:** Topic 4 Lab, pp. 3-4 (A1-A3), pp. 5-6 (B1-B4), pp. 7-8 (report and submission). The provided lab requires one eight-section report, a PDF copy and an updated repository; no new pipeline is required.

**Submission:** [GitHub repository](https://github.com/Pokeepic/ai-engineering-home-garden-companion). Final Markdown and PDF are prepared; eLearning upload is pending. GitHub upload is not an eLearning submission.
