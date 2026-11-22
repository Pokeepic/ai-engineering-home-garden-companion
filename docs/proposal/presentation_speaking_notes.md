# Home Garden Companion: An AI Assistant for Tropical Gardening — Speaking Notes

**Presenter:** RAQIB HAZIM BIN ABDUL HAMID, A24AI0118, SECTION 3.
**Aligned with report revision 3cf4b04:** 22 November 2026. Title, eight content slides and references. Seven-minute rehearsal plan, followed by three minutes of Q&A. Timing is a target, not a measured delivery.

## Slide 1 - Home Garden Companion (10 seconds)

My project is Home Garden Companion. It asks whether a conversational assistant can help beginners obtain supported gardening guidance more effectively than searching the same documents.

## Slide 2 - Gardening advice needs context (45 seconds)

Consider the question: how often should I water my plant? NParks connects plant choice with light, water, space and growing conditions. A beginner must still find the relevant passage and decide whether it applies. If essential context is missing, a fixed watering schedule would replace that missing information with an assumption. The proposed assistant would ask for clarification before explaining supported guidance. The evidence establishes why context matters. User demand and benefits remain untested, so the project will compare the assistant with keyword search over the same approved documents.

## Slide 3 - Research and the engineering gap (45 seconds)

Published guides already provide identifiable information. An assistant must preserve access to that evidence and justify the extra complexity. Lewis and colleagues provide the basis for combining retrieval with generation. However, finding a passage does not establish that an answer uses it accurately. Gao and colleagues therefore inform separate correctness and citation-quality checks. Liu and colleagues show why adding more context alone may not solve the problem. The engineering gap is combining suitable retrieval, faithful explanation and explicit response limits for beginner gardening questions. These studies motivate the design, while local evaluation must establish its usefulness.

## Slide 4 - Scope and objectives (45 seconds)

The report has three numbered objectives. First, identify beginner information needs and establish verified sources. Second, develop a text assistant that cites its evidence and handles unclear, unsupported and excluded questions appropriately. Third, evaluate answer quality, usability and response time, including comparison with keyword search. The initial users are English-speaking beginners with tropical indoor or balcony plants. Tasks cover light, watering principles, growing media and supported plant comparisons. Image diagnosis, pesticide dosages, ingestion advice and safety guarantees remain outside scope. The current collection needs more coverage before all intended tasks can be supported.

## Slide 5 - Requirements and evaluation (65 seconds)

The evaluation examines both response quality and the user’s task. The slide shows selected targets from the full requirements. Correctness requires at least 34 of 40 answerable cases to pass. Factual claims need complete citation coverage and at least 95 percent claim support. The timing targets are a median of ten seconds and a p95 of twenty seconds. These are initial prototype goals, not achieved results. The normal workload has 40 answerable, ten ambiguous, twenty unsupported and twenty excluded cases, with additional privacy and failure tests. Missing an answerable question counts as incorrect. Passing these checks would establish technical performance. The matched comparison with keyword search will then measure supported task completion and time to a correct answer. Participant recruitment and allocation remain to be defined.

## Slide 6 - Proposed architecture (60 seconds)

The architecture separates responsibilities so that a failure can be traced to its source. Input checks identify missing context, scope issues and personal identifiers before information reaches an external service. Retrieval supplies passages with document and page metadata. The language model drafts an explanation, and response checks examine its support and boundaries before display. Clarification, abstention and refusal are valid outcomes when an answer cannot proceed. A9 records evaluation across the interaction. Retrieval adds indexing work and latency. Temporary context reduces retention but limits personalisation. One generation step keeps the prototype manageable but limits opportunities for repair. These are logical responsibilities within one application. Only the source-preparation pilot within A5 is complete. The next question is whether the prepared evidence can support this design.

## Slide 7 - Preparing traceable evidence (55 seconds)

The pilot inspected three NParks PDFs with 46 pages, then prepared selected prose from three pages in two sources. This small collection allowed individual records to be checked against the originals. The table compares the same cleaned text: fixed cuts split two sections and one word, while paragraph-aware packing split neither. I selected paragraph-aware packing and accepted variable lengths, including a maximum of 656 characters against a soft target of 500. This supports text preservation, but retrieval performance remains untested. The pipeline keeps source and page metadata, verifies file hashes and validates staged output before replacement. Two local runs matched. Missing-file and changed-checksum tests preserved the valid output. That establishes repeatability for this pilot.

## Slide 8 - Quality and coverage (45 seconds)

Repeatability does not establish that the collection covers the intended tasks. All five records passed reference and selected-prose fidelity checks, but the collection lacks complete plant profiles for comparisons. Extraction also omitted the soil-ratio table. The houseplant brochure was deferred because its layout mixed headings and body text. Keeping easily extracted prose may favour generic advice in later retrieval. That is a preparation risk, not a measured model result. Source currency also remains unverified. These findings show why accurate passages can still form an incomplete collection and explain the conditions on the next stage.

## Slide 9 - Readiness and next steps (40 seconds)

The readiness decision is HOLD for the intended answer corpus and public AI service. Permission, coverage and currency remain unresolved. First, I will resolve source rights or use licensed replacements while validating beginner needs. Next, I will repair coverage or narrow the tasks and repeat validation. An approved collection will support the assistant and a keyword-search baseline over the same documents. Evaluation will then test both response quality and user benefit. The expected contribution is an evaluated application, including evidence of where it does or does not improve on search.

## Slide 10 - References (10 seconds)

The numbered sources match the report. Full research references and project evidence are in the notes. Thank you. I welcome questions about the design and evaluation.

## Q&A preparation

- **Why use AI instead of search?** It may help interpret varied questions and explain multiple passages. That benefit is a hypothesis; the keyword-search comparison tests it.
- **Why only five chunks?** This is a verified preparation pilot. It is insufficient for the complete proposed task set. Expanding it needs rights resolution and reviewed source coverage.
- **Why HOLD if the checks pass?** The checks establish source references and selected-text fidelity. They do not establish permission, completeness or currency.
- **Why 500 characters?** It was a controlled illustrative comparison target, not a model limit or optimised retrieval setting. Paragraph integrity was preferred, with an explicit oversize exception.
- **Does RAG prevent hallucinations?** No. Retrieval can miss evidence and generation can misuse it. Claim-support evaluation and abstention are required.
- **Have you met 85% correctness?** No. That is a proposed acceptance criterion for later application tests. Five passing data records are not five correct model answers.
- **Are the thresholds scientifically established?** No. They are initial reviewable prototype goals. User needs, feasibility and errors must inform any justified, versioned revisions.
- **Which model and vector database?** Not selected. A vector database is not mandatory for the conceptual architecture. Choose technology after source readiness and development experiments.
- **Is the system already running in Colab?** The notebook executed locally. It supports Colab paths, but no connected Colab runtime is claimed.
- **What would lift the gate?** Applicable permission or licensed replacements, evidence supporting the agreed scope, justified version/freshness handling and passing validation on revised outputs.

## Report alignment and rehearsal cues

| Slides | Rewritten report section | Emphasis |
|---|---|---|
| 2–4 | 1 Problem Definition and Project Scope | Evidence, research limitations, objectives, users and exclusions |
| 5 | 2 Requirements Specification; 3 Evaluation Criteria | FR/NFR/RAI, measurement methods, denominators and proposed targets |
| 6 | 4 AI System Architecture | Information flow, alternative outcomes and accepted trade-offs |
| 7–8 | 5 Data Engineering and Quality | Executed pilot, source lineage, checks and coverage limitations |
| 9 | 6 Implementation Plan and Conclusion | Conditional implementation stages and expected contribution |
| 10 | References | Citation numbers are identical to the report |

**Timing checkpoints:** Slide 1 ends at 0:10; slide 2 at 0:55; slide 3 at 1:40; slide 4 at 2:25; slide 5 at 3:30; slide 6 at 4:30; slide 7 at 5:25; slide 8 at 6:10; slide 9 at 6:50; slide 10 at 7:00. These are rehearsal targets, not measured delivery times.

**Narrative:** context-dependent gardening question, research principles, bounded objectives, measurable behaviour, architecture, preparation evidence, readiness and evaluation.

**During rehearsal:** point to the architecture flow while explaining it. Do not read the reference list aloud. Keep data-validation results distinct from future model evaluation. The photos are decorative template assets, not observed outcomes or pet-safety evidence.

## References matching the report

[1] National Parks Board. Choosing Plants. GardeningSG, 17 July 2023. https://gardeningsg.nparks.gov.sg/gardening-resource-library/choosing-plants/ (accessed 22 November 2026).

[2] National Parks Board. Introduction to Indoor Gardening. PDF, pp. 5 and 10. https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf (accessed 10 November 2026; publication date not verified).

[3] National Parks Board. Introduction to Community Gardening. PDF, p. 6. https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf (accessed 10 November 2026; publication date not verified).

[4] National Parks Board. Know 10 Houseplants; Downloadable resources. https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/ . Brochure inspected locally; excluded from pilot preparation.

[5] Lewis, P., et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. NeurIPS 33. https://arxiv.org/abs/2005.11401

[6] Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling Large Language Models to Generate Text with Citations. EMNLP, 6465–6488. https://aclanthology.org/2023.emnlp-main.398/

[7] Liu, N. F., et al. (2024). Lost in the Middle: How Language Models Use Long Contexts. TACL 12, 157–173. https://aclanthology.org/2024.tacl-1.9/

[8] National Parks Board. Terms of Use. Page states 26 June 2026 update. https://gardeningsg.nparks.gov.sg/terms-of-use/ (reviewed 22 November 2026).

## Project evidence references

[9] Home Garden Companion project repository. Week 2 requirements, version 1.1, 26 October 2026. docs/week2_requirements.md.

[10] Home Garden Companion project repository. Week 2 evaluation criteria. docs/week2_evaluation_criteria.md.

[11] Home Garden Companion project repository. Week 2 architecture decisions and traceability. docs/week2_architecture_decisions.md.

[12] Home Garden Companion project repository. Week 3 data inventory and pipeline decisions. docs/week3_data_inventory.md; docs/week3_pipeline_decisions.md.

[13] Home Garden Companion project repository. Executed notebook and Part C validation. notebooks/week3_pipeline.ipynb; data/inspection/week3_part_c_validation.json; data/pipeline_v1/documents/pipeline_manifest.json.

[14] Home Garden Companion project repository. Week 4 Data Quality & Bias Report, 22 November 2026. docs/week4_data_quality_report.md; data/inspection/week4_part_b_validation.json.

Repository for [9]–[14]: https://github.com/Pokeepic/ai-engineering-home-garden-companion . These are author-created project artifacts and execution evidence, not independent research studies.
