# Home Garden Companion — Presentation speaking notes

RAQIB HAZIM BIN ABDUL HAMID · A24AI0118 · SECTION 3

Updated 22 November 2026. Ten slides: title, eight content slides and references. Seven-minute rehearsal plan plus three minutes of Q&A. Bracketed directions are delivery cues, not spoken text. The interaction is illustrative; application results remain unmeasured.

## Slide 1 — Home Garden Companion (30 seconds)

Good morning. I’m Raqib.

Imagine bringing home your first plant. You find a place for it. You want to take care of it. Then you reach for your phone, because you have one very ordinary question.

[Pause. Advance to the question.]

## Slide 2 — How often should I water it? (40 seconds)

“How often should I water it?”

[Pause for two seconds.]

Before I give you an answer, I need to know what “it” is. What plant? What conditions?

NParks connects plant choice with light, water, space and soil. The guidance exists. But the beginner still has to find the right passage and work out whether it applies.

That moment, between finding information and knowing what to do with it, is where this project begins.

## Slide 3 — A conversation with evidence (50 seconds)

Here is the experience I want to build.

You ask the same question. The assistant starts by asking which plant you have and where you keep it.

[Point to the follow-up question.]

Once it has enough context, it looks for relevant guidance in an approved collection. It explains that guidance and gives you the document and page, so you can check it yourself.

And if the evidence is missing, it says so.

That is Home Garden Companion. This is an illustration of the proposed interaction. The assistant itself has not been built yet.

The aim is simple: make the guidance easier to use while keeping the evidence within reach.

## Slide 4 — A focused first version (40 seconds)

For the first version, I’m keeping the job focused: beginner gardeners, tropical indoor or balcony plants, and questions in English.

My objectives are numbered here. First, understand users’ needs and verify the sources. Second, build an assistant that can answer with citations and recognise its limits. Third, test its quality and usefulness against search.

It will cover light, watering principles, growing media and comparisons that the sources can support. Image diagnosis, pesticide dosages and safety guarantees are outside this version.

That gives me a scope I can actually test.

## Slide 5 — What would count as success? (60 seconds)

So how will I know whether it helps?

First, the answers have to be right. The initial target is at least 34 correct answers out of 40 answerable questions. Every factual claim needs a citation, and at least 95 percent of those claims must be supported by the cited evidence.

The assistant also needs to respond in a reasonable time: a median of ten seconds and a p95 of twenty seconds.

These are targets for later testing. I have not achieved them yet.

Then comes the important comparison: the assistant and keyword search, using the same approved documents. Can users complete the task correctly? How long does it take to reach a supported answer?

That comparison will tell me whether the extra conversation is worth it.

## Slide 6 — How the answer would be built (55 seconds)

Behind that conversation is a short chain of responsibilities.

[Trace the diagram from left to right.]

Check the question. Retrieve relevant passages. Draft an explanation. Check its support before showing it.

Lewis and colleagues provide the retrieval-and-generation foundation. Gao and colleagues show why answer correctness and citation quality need separate evaluation. Liu and colleagues show that the position of evidence in a long context can affect performance, so simply adding more text is not enough.

The engineering work is bringing those ideas together with clarification and response limits.

Retrieval adds work and latency. Temporary context limits personalisation. One generation step gives less opportunity to repair a draft. Those are the initial trade-offs, and testing will determine which choices need to change.

## Slide 7 — Five passages, checked carefully (55 seconds)

There is already some completed work behind this proposal.

I inspected three PDFs containing 46 pages. For the pilot, I prepared five passages from three selected pages in two sources.

Why start small? So I could check what happened to the text.

[Point to the two rows.]

Fixed-length cuts broke two sections and one word. Keeping paragraphs together broke neither. I chose paragraph-aware packing, accepting variable lengths. The longest passage was 656 characters against a soft target of 500.

The pipeline keeps the document and page references. Two local runs produced matching outputs, and the failure tests protected the previous valid output.

That is evidence that the preparation process works for this small pilot. Retrieval still needs to be tested.

## Slide 8 — The collection is not ready yet (40 seconds)

But five clean passages do not give me a complete gardening assistant.

The records passed the reference and selected-text checks. The collection still lacks complete plant profiles for comparisons, and extraction missed a soil-ratio table. Selecting only easy-to-extract prose could leave the answers too general.

Source currency and permission for the intended use also remain unresolved.

So the decision is HOLD on using this collection as the answer corpus or in a public service. The audit has given me a concrete next step: fix the collection before building on it.

## Slide 9 — The next step (40 seconds)

I will start by validating beginner needs and resolving the source rights, using licensed replacements where necessary. Then I’ll fill the coverage gaps, or narrow the supported tasks, and repeat the checks.

With an approved collection, I can build the assistant and compare it with keyword search.

[Pause. Return to the opening question.]

We started with someone asking how to water a plant. The result I want is an answer they can understand, that fits the information they have given, and that they can check.

That is what Home Garden Companion will be tested on.

## Slide 10 — References (10 seconds)

Thank you. These are the research and project sources behind the proposal. I’m happy to take your questions.

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

## Rehearsal and report coverage

| Slides | Coverage |
|---|---|
| 1–2 | Problem and evidence |
| 3–4 | Proposed experience, numbered objectives, users and scope |
| 5 | Requirements, acceptance criteria and user comparison |
| 6 | Related work, engineering gap, architecture and trade-offs |
| 7–8 | Data preparation, executed findings, risks and readiness |
| 9 | Implementation stages and intended contribution |
| 10 | References |

The full evaluation workload remains 90 normal cases: 40 answerable, 10 ambiguous, 20 unsupported and 20 excluded. Twenty privacy cases and five service-failure cases are additional. A missing answer on an answerable case fails correctness. The 10 coverage-disclosure cases are a subset of the unsupported set. These counts follow the Week 2 protocol and are not application results.

Other acceptance criteria remain in the report and Week 2 specification: clarity at least 36/40, normal completion at least 89/90 and handling all five failures, unsupported-case abstention at least 19/20, excluded-case refusal plus redirection at least 19/20 with zero excluded instructions or guarantees, zero identifier leaks in 20 privacy cases, clarification at least 9/10, and disclosure in all 10 coverage cases.

At 40 successful timed responses, nearest-rank p95 is the 38th sorted duration. Failures are reported separately. One warm-up is excluded. Participant recruitment, consent and task allocation must be defined before the user comparison. No deployment, user benefit or model-performance result is claimed.

Timing checkpoints: 0:30, 1:10, 2:00, 2:40, 3:40, 4:35, 5:30, 6:10, 6:50, 7:00. Rehearse aloud and use the pauses. Do not read the citations or cue text.

Presentation reference: Steve Jobs Archive, “Speech at Macworld” (2007), https://book.stevejobsarchive.com/#speech-at-macworld. Used for pacing and the sequence of problem, reveal and explanation, not as evidence for the gardening project. The script is original.

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
