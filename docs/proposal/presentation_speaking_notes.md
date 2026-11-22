# PlantPal proposal speaking notes

**Presenter:** RAQIB HAZIM BIN ABDUL HAMID, A24AI0118, SECTION 3.
**Draft:** 22 November 2026. Ten slides: title, eight content slides, references. Planned timing totals 7 minutes, followed by 3 minutes of Q&A. Rehearse and adjust to your speaking pace; this is a timing plan, not a recorded rehearsal.

## Slide 1 - PlantPal (10 seconds)

My proposal is PlantPal, a document-grounded home gardening assistant. I will explain its intended behaviour, the preparation work completed, and the conditions that must be resolved before downstream implementation.

## Slide 2 - The problem (45 seconds)

Beginner gardeners must connect information about light, water, growing media and available space. NParks identifies these environmental conditions as important when choosing and growing plants. PlantPal proposes to help users ask questions in ordinary English and receive an explanation linked to source pages. The engineering problem is keeping that explanation connected to evidence and recognising when context is missing. I have not yet surveyed users, so I am not claiming demonstrated chatbot demand or better plant survival. Official guides already exist. The proposed value is easier access to supported information, which still needs evaluation.

## Slide 3 - Why this approach (45 seconds)

Three research directions inform the design. Lewis and colleagues motivate combining retrieval with generation. Gao and colleagues show why citation quality needs its own evaluation. Liu and colleagues demonstrate that long-context use is not automatically reliable in their tasks. These findings support investigating retrieved evidence and checking claims, but they do not prove PlantPal will work. My engineering gap is a bounded integration of source access, citations, clarification and coverage limits for beginner gardening. I will compare it with keyword search over the same approved collection rather than assume that adding a language model is an improvement.

## Slide 4 - Scope and objectives (45 seconds)

O1 is to validate beginner information needs and establish a reviewed source collection. O2 is to develop a text assistant with citations and appropriate clarification, abstention and refusal. O3 is to evaluate its outcomes against a search baseline. The intended users are beginner tropical indoor or balcony gardeners. Supported topics are light, watering principles, growing media, space and plant comparisons where the documents support them. Image diagnosis, pesticide dosages, ingestion advice and safety guarantees are excluded. The decorative cat photograph is part of the supplied template, not evidence that PlantPal provides pet-safety advice.

## Slide 5 - Success criteria (65 seconds)

FR2 requires a document title, URL and one-based PDF page for factual claims. NFR2 proposes at least 34 correct answers out of 40 answerable questions, with results broken down across four topic groups. Citation completeness is 100%, and passage support must reach at least 95%. A real citation does not automatically support a claim. NFR1 proposes a median response time at most ten seconds and a p95 at most twenty seconds, measured from submission to complete response. These are initial prototype targets, not achieved results or user-validated guarantees. Separate tests cover unsupported questions, clarification, refusal, clarity, service failure and synthetic privacy identifiers. Missing answers stay in the relevant denominators. The full evaluation specification is in the report.

## Slide 6 - Proposed architecture (60 seconds)

A2 accepts the question and keeps temporary context. A3 checks missing information, scope and personal identifiers before external processing. A4 obtains relevant page-tagged evidence from A5. A6 drafts an answer, while A7 checks support and boundaries before A8 displays the selected outcome. A9, described in the report, measures performance and records minimal diagnostics. If the question is ambiguous, the system should clarify. If evidence is missing, it should abstain. If the task is excluded, it should refuse. Failures should produce an error, not invented advice. These are proposed responsibilities, not deployed microservices. So far, the source-preparation work in A5 has been implemented; model and retrieval behaviour remain untested.

## Slide 7 - Data pipeline (55 seconds)

Three NParks PDFs, totalling 46 pages, were inspected. The prepared pilot contains only three selected pages from two sources and five text chunks. I compared fixed character cuts with paragraph-aware packing on identical text. Both produced five chunks, but fixed cuts split two sections and one word. The selected method kept sections intact, accepting a 656-character chunk above the 500-character soft target. It preserves document and page information. The integrated pipeline rereads the originals, validates the export and records hashes and mappings. Two executions matched, and missing-input and checksum-change tests stopped without replacing the valid output. This proves a limited local repeatability result, not answer accuracy.

## Slide 8 - Quality findings (45 seconds)

Topic 4 inspected all five available records. V1 source-reference checks and V2 selected-prose fidelity each passed five out of five. No exact-normalised duplicate texts were found. However, timeliness is not verified, the soil-ratio table was lost during extraction, and plant-profile comparisons are not supported. The profile brochure was deferred because its layout mixed heading and body order. This can bias later retrieval toward generic advice. It is a plausible preparation risk, not proven model unfairness. Passing reference and fidelity checks does not mean the whole intended knowledge domain is covered.

## Slide 9 - HOLD and next steps (40 seconds)

The gate is HOLD for promotion to the intended downstream answer corpus or public service. Permission for the intended use is unresolved, and coverage remains incomplete. The next actions are to resolve rights or select suitably licensed alternatives, verify source versions and repair coverage. Then I can revalidate, decide a new gate and implement the assistant. The HOLD does not mean the coursework pipeline failed. It shows that I distinguish technical success from readiness for the intended use. No model accuracy, user benefit or production safety is claimed at this stage.

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

## Slide references

1. NParks, Choosing Plants: https://gardeningsg.nparks.gov.sg/gardening-resource-library/choosing-plants/
2. NParks, Introduction to Indoor Gardening, PDF p5: source URL in `docs/week3_data_inventory.md`.
3. Lewis et al. (2020), Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks: https://arxiv.org/abs/2005.11401
4. Gao et al. (2023), Enabling Large Language Models to Generate Text with Citations: https://aclanthology.org/2023.emnlp-main.398/
5. Liu et al. (2024), Lost in the Middle: https://aclanthology.org/2024.tacl-1.9/
6. PlantPal Week 3/4 evidence: https://github.com/Pokeepic/ai-engineering-plantpal
7. NParks Terms of Use, reviewed 22 November 2026: https://gardeningsg.nparks.gov.sg/terms-of-use/

Research is design motivation, not PlantPal performance evidence. Template photos are decorative and are not source data or observed project outcomes.
