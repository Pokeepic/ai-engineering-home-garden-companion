# Home Garden Companion: An AI Assistant for Tropical Gardening — Speaking Notes

**Presenter:** RAQIB HAZIM BIN ABDUL HAMID, A24AI0118, SECTION 3.
**Finalised against the structured proposal report:** 22 November 2026. Ten slides: title, eight content slides, references. Planned timing totals 7 minutes, followed by 3 minutes of Q&A. Rehearse and adjust to your speaking pace; this is a timing plan, not a recorded rehearsal.

## Slide 1 - Home Garden Companion (10 seconds)

My project is Home Garden Companion, an AI assistant for tropical gardening. I will explain its intended behaviour, the preparation work completed, and the conditions that must be resolved before downstream implementation.

## Slide 2 - The problem (45 seconds)

Beginner gardeners must connect information about light, water, growing media and available space. NParks identifies these environmental conditions as important when choosing and growing plants. Home Garden Companion proposes to help users ask questions in ordinary English and receive an explanation linked to source pages. The engineering problem is keeping that explanation connected to evidence and recognising when context is missing. I have not yet surveyed users, so I am not claiming demonstrated chatbot demand or better plant survival. Official guides already exist. The proposed value is easier access to supported information, which still needs evaluation.

## Slide 3 - Research and engineering gap (45 seconds)

Three research directions inform the design. Lewis and colleagues motivate combining retrieval with generation. Gao and colleagues show why citation quality needs its own evaluation. Liu and colleagues demonstrate that long-context use is not automatically reliable in their tasks. These findings support investigating retrieved evidence and checking claims, but they do not prove Home Garden Companion will work. My engineering gap is a bounded integration of source access, citations, clarification and coverage limits for beginner gardening. I will compare it with keyword search over the same approved collection rather than assume that adding a language model is an improvement.

## Slide 4 - Scope and objectives (45 seconds)

O1 is to validate beginner information needs and establish a reviewed source collection. O2 is to develop a text assistant with citations and appropriate clarification, abstention and refusal. O3 is to evaluate its outcomes against a search baseline. The intended users are beginner tropical indoor or balcony gardeners. Supported topics are light, watering principles, growing media, space and plant comparisons where the documents support them. Image diagnosis, pesticide dosages, ingestion advice and safety guarantees are excluded. The scope also excludes automated watering and environmental sensing.

## Slide 5 - Requirements and evaluation (65 seconds)

FR2 requires a document title, URL and one-based PDF page for factual claims. NFR2 proposes at least 34 correct answers out of 40 answerable questions, with results broken down across four topic groups. Citation completeness is 100%, and passage support must reach at least 95%. A real citation does not automatically support a claim. NFR1 proposes a median response time at most ten seconds and a p95 at most twenty seconds, measured from submission to complete response. These are initial prototype targets, not achieved results or user-validated guarantees. The normal workload has 90 cases: 40 answerable, 10 ambiguous, 20 unsupported and 20 excluded. Privacy and failure tests are separate. Missing answers stay in the relevant denominators. Correctness is checked against reference facts; support is checked claim by claim.

## Slide 6 - Proposed architecture (60 seconds)

The question enters A2, then A3 checks scope, missing context and personal identifiers. A4 retrieves page-tagged evidence from A5. A6 drafts an explanation; A7 checks support and boundaries; A8 displays an answer, clarification, abstention or refusal. A9 evaluates these outcomes. Retrieval adds latency and indexing work, but allows claims to be traced to documents. Temporary context reduces stored personal data at the cost of personalisation. One generation step keeps the prototype simple but gives less opportunity for iterative repair. These are proposed responsibilities, not deployed services. Only source preparation in A5 has been implemented; neither retrieval quality nor model answers have been tested.

## Slide 7 - Data pipeline (55 seconds)

Three NParks PDFs, totalling 46 pages, were inspected. The prepared pilot contains only three selected pages from two sources and five text chunks. I compared fixed character cuts with paragraph-aware packing on identical text. Both produced five chunks, but fixed cuts split two sections and one word. The selected method kept sections intact, accepting a 656-character chunk above the 500-character soft target. It preserves document and page information. The integrated pipeline rereads the originals, validates the export and records hashes and mappings. Two executions matched, and missing-input and checksum-change tests stopped without replacing the valid output. This proves a limited local repeatability result, not answer accuracy.

## Slide 8 - Quality findings (45 seconds)

Topic 4 inspected all five available records. V1 source-reference checks and V2 selected-prose fidelity each passed five out of five. No exact-normalised duplicate texts were found. However, timeliness is not verified, the soil-ratio table was lost during extraction, and plant-profile comparisons are not supported. The profile brochure was deferred because its layout mixed heading and body order. This can bias later retrieval toward generic advice. It is a plausible preparation risk, not proven model unfairness. Passing reference and fidelity checks does not mean the whole intended knowledge domain is covered.

## Slide 9 - HOLD and next steps (40 seconds)

The gate is HOLD for promotion to the intended downstream answer corpus or public service. Permission for the intended use is unresolved, and coverage remains incomplete. The four stages are to resolve rights and source versions, repair coverage and revalidate, build the cited assistant, and evaluate it against keyword search. User-needs validation is also still required. The HOLD does not mean the coursework pipeline failed. It shows that I distinguish technical success from readiness for the intended use. No model accuracy, user benefit or production safety is claimed at this stage.

## Slide 10 - References (10 seconds)

The report contains full research references and links to the project evidence. The slide design comes from the supplied template. I am ready to discuss the assumptions, limitations and next engineering decisions.

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

| Slides | Updated report section | Emphasis |
|---|---|---|
| 2–4 | 1 Problem Definition and Project Scope | Evidence, research limitations, objectives, users and exclusions |
| 5 | 2 Requirements Specification; 3 Evaluation Criteria | FR/NFR/RAI, measurement methods, denominators and proposed targets |
| 6 | 4 AI System Architecture | Information flow, alternative outcomes and accepted trade-offs |
| 7–8 | 5 Data Engineering and Quality | Executed pilot, source lineage, checks and coverage limitations |
| 9 | 6 Implementation Plan and Conclusion | Conditional implementation stages and expected contribution |
| 10 | References | Citation numbers are identical to the report |

**Timing checkpoints:** Slide 1 ends at 0:10; slide 2 at 0:55; slide 3 at 1:40; slide 4 at 2:25; slide 5 at 3:30; slide 6 at 4:30; slide 7 at 5:25; slide 8 at 6:10; slide 9 at 6:50; slide 10 at 7:00. These are rehearsal targets, not measured delivery times.

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
