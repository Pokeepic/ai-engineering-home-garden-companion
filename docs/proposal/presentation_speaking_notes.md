# Home Garden Companion — Revised speaking notes

Updated 22 November 2026. Ten slides: title, eight content slides and references. Seven-minute rehearsal target plus three minutes of Q&A. Bracketed cues are not spoken. Source citations are separate from the spoken script.

## Slide 1 — Home Garden Companion (15 seconds)

Good morning. I’m Raqib. My project is Home Garden Companion, an AI assistant for tropical gardening.

It starts with a question a beginner might ask on their first day.

## Slide 2 — The problem: advice needs context (35 seconds)

“How often should I water my plant?”

It sounds simple. But what plant? How much light does it get? What is it growing in?

Published gardening guidance connects these conditions with plant choice and care. Unsuitable growing conditions can weaken a plant.

The information exists, but the beginner still has to find the right passage and decide whether it applies.

That’s the problem I want to address. I still need to validate beginner needs and test whether a conversational assistant makes this task easier.

## Slide 3 — The proposed solution and scope (45 seconds)

The proposed assistant would ask for missing details, find relevant guidance and explain it with a document and page you can check.

I have three objectives: identify users’ needs and verify the sources, develop the assistant, then evaluate its quality and usefulness against keyword search.

The initial users are beginners with tropical indoor or balcony plants, asking questions in English.

Supported tasks cover light, watering principles, growing media, space and plant comparisons where the evidence is sufficient.

Image diagnosis, pesticide dosages, ingestion advice, safety guarantees and automatic watering are outside scope. This keeps the first version focused on explaining written guidance.

## Slide 4 — What the assistant must do (50 seconds)

These requirements define how the assistant should behave.

It should answer supported questions in plain language and attach the document title, URL and PDF page to factual claims.

If essential details are missing, it should ask. If the documents cannot support an answer, it should say so. If the request is outside scope, it should refuse that task and redirect the user.

Responsible AI adds checks on whether the evidence supports the answer. It also requires clear disclosure of coverage limits and protection of personal information.

For example, the assistant should not need someone’s exact home address to explain plant care. I’ll inspect both outgoing requests and logs to test that restriction.

## Slide 5 — How I will evaluate it (65 seconds)

Here’s how I’ll test those requirements.

Forty answerable questions will have reference facts and supporting pages prepared in advance. At least 34 answers must be correct, and at least 36 must pass the clarity rubric.

I’ll check each factual claim for a citation and whether the cited passage supports it. The targets are complete citation coverage and at least 95 percent support.

Separate cases test clarification, unsupported questions, excluded requests and privacy. The normal workload totals 90 cases, with twenty privacy scenarios and five simulated failures added separately.

I’ll also time responses and check controlled error handling.

Finally, users will try matched tasks with the assistant and keyword search over the same documents. I’ll compare supported task completion and time. All these targets are proposed, and the user study still needs a defined recruitment and allocation plan.

## Slide 6 — Architecture and design choices (65 seconds)

The architecture separates where information is prepared from where an answer is produced.

[Point to the source collection, then follow the main path.]

The user asks through the text interface. Input checks handle scope, missing context and personal identifiers. Retrieval selects passages from the approved collection, keeping their document and page details.

The language model drafts an explanation. Response checks examine support and boundaries before the result reaches the user. Evaluation records the outcome across the interaction.

The design uses external documents so evidence can be inspected and updated. That adds retrieval work and latency. Page metadata makes a reference traceable, but still needs a separate check that the passage supports the claim. I’ll also test which passages to include instead of sending every document.

Temporary context limits personalisation, and one draft gives less opportunity for repair. The model and retrieval technology are still undecided. Only the preparation pilot is complete.

## Slide 7 — Sources and preparation pipeline (55 seconds)

I selected three gardening PDFs for inspection. The indoor guide covers conditions and growing media. The houseplant brochure contains candidate plant profiles. The community guide provides supplementary growing information.

Together they contain 46 pages. The pilot uses selected prose from three pages in the indoor and community guides. The houseplant brochure is deferred because extraction mixed headings and body text.

The pipeline verifies the original files, extracts text page by page, cleans verified artefacts, preserves headings and packs paragraphs into passages.

It then writes staged JSONL and checks it before replacing the valid output.

Each passage keeps its title, URL and page. A manifest records source fingerprints and output mappings so I can trace a passage back to the preparation run.

## Slide 8 — Completed work and remaining risks (50 seconds)

The completed pilot contains five passages.

[Point to the comparison table.]

Fixed-length cuts split two sections and one word. Paragraph-aware packing split neither. I selected that method and accepted variable lengths, including a 656-character passage against a soft target of 500.

Two local runs matched. Missing-file and changed-checksum tests stopped without replacing valid output. All five records passed source-reference and selected-text fidelity checks.

But coverage remains incomplete: plant profiles are missing, and extraction lost a soil-ratio table. Keeping easy-to-extract prose could make later answers too general. Currency and intended-use rights are also unresolved.

So the collection is on HOLD for the intended answer corpus and public service. Passing preparation checks does not mean the assistant is ready.

## Slide 9 — Implementation plan (30 seconds)

The next steps follow directly from those findings.

First, validate user needs and resolve source rights, using licensed replacements where necessary. Then repair the collection or narrow the tasks and rerun validation.

With an approved collection, I can build the assistant, select its configuration using development cases, and run the evaluation against keyword search.

The intended contribution is a tested gardening assistant with traceable evidence. Whether it helps beginners more than search remains something I need to demonstrate.

## Slide 10 — References (10 seconds)

Thank you. I’m happy to take your questions.

## Q&A preparation — not part of the timed script

- **Why use AI?** To investigate whether interpreting varied questions and explaining several passages improves access. The comparison with search tests that benefit; it is not assumed.
- **What is the engineering gap?** Combining source retrieval, faithful explanation, clarification and explicit task limits in a bounded gardening application, then evaluating the complete interaction.
- **Why these sources?** They cover tropical gardening conditions and candidate plant profiles. S02’s extraction problems and unresolved use rights prevent treating all inspected material as an approved corpus.
- **Why five passages?** It is a preparation pilot for inspectable comparisons, not enough coverage for the whole application.
- **Why paragraph-aware packing?** In the controlled comparison it avoided the observed section and word cuts. This does not establish retrieval quality or an optimal chunk size.
- **Why RAG?** It provides access to inspectable external passages, while adding retrieval failure modes and latency. Retrieval does not guarantee factual answers.
- **Which model or vector database?** Undecided. A dedicated vector database is optional. Select technology using development tests after source approval.
- **How do you assess privacy?** Twenty synthetic-identifier scenarios. Inspect outgoing payloads and logs, and check unnecessary identifier requests. Zero leaks, persistence or unnecessary requests are allowed by the specification.
- **How do you avoid hiding failures?** Missing or abstained answers to answerable cases fail correctness. A response with no factual claims gets no perfect citation score. Timing failures are reported separately.
- **What does p95 mean here?** Nearest-rank duration at position ceil(0.95 × n). With 40 successes this is the 38th sorted duration. One warm-up is excluded and failures remain reported.
- **Is the user study ready?** No. Define recruitment, consent, participant count and matched-task allocation before testing. User task time differs from system response time.
- **Are these achieved targets?** No. Only document preparation and audit results are complete. No application-performance or user-benefit result is claimed.
- **What lifts HOLD?** Documented applicable rights or licensed replacements, adequate task coverage, justified source-version/currency checks and repeated validation.

## Evaluation details — for rehearsal and questions

Normal cases: 40 answerable, 10 ambiguous, 20 unsupported and 20 excluded = 90. Add 20 privacy scenarios and 5 simulated service failures. Ten coverage-disclosure cases are a subset of the unsupported set.

Targets: correctness ≥34/40; clarity ≥36/40 at 3/3; citation coverage 100%; claim support ≥95%; clarification ≥9/10; abstention ≥19/20; refusal plus redirection ≥19/20 with zero excluded actionable instructions or guarantees; coverage disclosure 10/10; zero privacy violations; normal completion ≥89/90 and controlled failures 5/5; median latency ≤10 seconds and p95 ≤20 seconds.

Use predefined reference facts and pages, separate development cases from final cases, and record corpus/model/application versions and reviewer decisions. These initial engineering targets require feasibility and user-needs validation.

## Lecturer coverage map

| Criterion | Main slides | Supporting notes |
|---|---|---|
| Problem, objectives and scope | 2–3 | Evidence boundary and user validation |
| Requirements and evaluation | 4–5 | Test inventory, metrics and measurement rules |
| Architecture | 6 | Component roles, alternatives and accepted trade-offs |
| Data engineering and quality | 7–8 | Named sources, pipeline, lineage, results and risks |
| Delivery and visual communication | 1–10 | Seven-minute pacing, readable diagrams and tables |
| Technical understanding and Q&A | 6–9 | Q&A above, assumptions and incomplete work |

Timing checkpoints: 0:15, 0:50, 1:35, 2:25, 3:30, 4:35, 5:30, 6:20, 6:50, 7:00. These are rehearsal targets.

## References — for checking, not spoken

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
