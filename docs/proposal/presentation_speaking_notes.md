# Home Garden Companion: An AI Assistant for Tropical Gardening — Speaking Notes

**Presenter:** RAQIB HAZIM BIN ABDUL HAMID, A24AI0118, SECTION 3.
**Updated against the rewritten proposal report:** 22 November 2026. Ten slides: title, eight content slides and references. Seven-minute timing plan, followed by three minutes of Q&A. Timing is a rehearsal target, not a measured delivery.

## Slide 1 - Home Garden Companion (10 seconds)

My project is Home Garden Companion, an AI assistant for tropical gardening. It investigates how to connect a beginner’s question with relevant, verifiable guidance.

## Slide 2 - Gardening advice needs context (45 seconds)

Consider the question: how often should I water my plant? An answer depends on the plant, light and growing medium. NParks presents these conditions together, but a reader still has to find the relevant guidance and apply it. Home Garden Companion would ask for essential missing context and explain supported guidance with source pages. The intended users are beginner indoor and balcony gardeners. I have not yet validated chatbot demand or improved plant survival. The proposal therefore treats easier access to information as a benefit to test. Research helps turn that problem into engineering choices.

## Slide 3 - Research shapes the design (45 seconds)

The research contributes three connected design principles. Lewis and colleagues combine document retrieval with language generation, motivating access to external evidence. Gao and colleagues evaluate citation quality separately from answer correctness, showing why a page reference also needs a claim-support check. Liu and colleagues find that relevant information’s position can affect long-context performance, motivating tests of context selection. Together, these studies support an assistant that retrieves evidence, checks how it is used and recognises its limits. The engineering gap is integrating those behaviours for beginner gardening. The project evaluates that integration against keyword search over the same approved collection.

## Slide 4 - Scope and objectives (45 seconds)

These principles lead to three objectives. O1 validates beginner information needs and establishes reviewed source coverage. O2 develops the cited text assistant, including clarification, abstention and refusal. O3 evaluates correctness and usefulness against keyword search. The prototype supports English questions about light, watering principles, growing media and space. Plant comparisons require supporting profiles. It uses temporary conversation context without accounts or persistent profiles. Image diagnosis, pesticide dosages, ingestion advice, safety guarantees, automated watering and sensing are outside scope. These boundaries define what a successful response must do, which leads to the requirements and evaluation plan.

## Slide 5 - Requirements and evaluation (65 seconds)

The requirements translate that scope into measurable behaviour. FR2 requires a document title, URL and one-based PDF page for factual claims. NFR2 sets an initial target of 34 correct answers out of 40. RAI1 requires complete citation coverage and at least 95 percent claim support. Correctness and support are assessed separately against reference facts and cited passages. NFR1 targets a median of ten seconds and a p95 of twenty seconds. These are proposed acceptance targets. The normal workload contains 40 answerable, ten ambiguous, twenty unsupported and twenty excluded cases. Privacy and failure scenarios are additional tests. A missing answer to an answerable question counts as incorrect. Later, a matched user comparison with keyword search will measure supported task completion and time to a correct answer. The architecture must make these outcomes observable.

## Slide 6 - Proposed architecture (60 seconds)

The question enters the text interface. A3 checks scope, essential context and personal identifiers before external processing. A4 retrieves page-tagged evidence from A5. A6 drafts the explanation, A7 checks support and boundaries, and A8 displays the appropriate response. Missing context leads to clarification, insufficient evidence to abstention, and an excluded task to refusal. A9 evaluates these outcomes. Retrieval adds latency and indexing work, while preserving evidence access. Page metadata makes claims inspectable but still needs semantic support checks. Temporary context limits retention at the cost of personalisation. One generation step keeps the prototype manageable but offers less opportunity for repair. These are logical responsibilities within one small application. The completed work currently covers source preparation in A5, so I will next explain that evidence.

## Slide 7 - Preparing traceable evidence (55 seconds)

I inspected three NParks PDFs containing 46 pages. The prepared pilot uses three selected pages from two sources and contains five chunks. On identical cleaned text, fixed character cuts split two verified sections and one word. Paragraph-aware packing split neither, so I selected it while accepting variable lengths. The longest chunk is 656 characters against a soft target of 500. Document titles, URLs and page numbers remain with the text. The pipeline rereads source files, checks their hashes, validates staged JSONL and records lineage before replacing output. Two local runs matched, and missing-file and changed-checksum tests preserved the valid output. These results establish preparation repeatability. The next question is whether the prepared collection is ready for its intended tasks.

## Slide 8 - Quality and coverage (45 seconds)

The Week 4 audit checked all five prepared records. Source-reference and selected-prose fidelity checks each passed five out of five. However, the collection has no complete plant profiles for the intended comparisons, and extraction omitted the soil-ratio table. The profile brochure was deferred because its layout mixed headings and body text. Selecting easily extracted prose could therefore favour generic advice in later retrieval. That is an identified preparation risk, not a measured model outcome. Source currency also remains unverified. The audit connects successful technical checks to a broader decision about coverage and readiness.

## Slide 9 - Readiness and next steps (40 seconds)

The decision is HOLD for downstream corpus use because intended-use permission, task coverage and source currency remain unresolved. The next stages are to resolve rights or obtain licensed replacements and validate user needs, repair coverage and rerun checks, implement the cited assistant, then evaluate it against keyword search. The completed preparation and audit provide the foundation. The expected contribution is an evaluated application with traceable evidence. Its user benefit remains a question for the planned evaluation.

## Slide 10 - References (10 seconds)

The report and speaking notes contain the full references and project evidence. Thank you. I welcome questions about the design choices and evaluation plan.

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
