# Home Garden Companion: An AI Assistant for Tropical Gardening — Project Proposal

RAQIB HAZIM BIN ABDUL HAMID | A24AI0118 | SECTION 3

**Year / Course:** 3 / SAIAH · **Semester:** 1 · **Section:** 3

**Lecturer:** DR HAZLIFAH BINTI MOHD RUSLI
22 November 2026

## 1 Problem Definition and Project Scope

### 1.1 Background and Problem Statement

A question such as how often to water a plant cannot always be answered from the question alone. The appropriate guidance depends on the plant and the conditions in which it grows. NParks identifies light, water, space and soil as important considerations in plant selection [1], while its indoor gardening guide connects environmental conditions with plant choice [2]. These sources establish why gardening advice needs context: a recommendation must be interpreted in relation to the situation in which it will be used.

Published guides provide relevant knowledge, but applying that knowledge still requires a reader to locate the appropriate passage and decide whether its conditions match their own. For a beginner asking about watering, essential details may be absent from the question. Providing a fixed schedule at that point would replace missing information with an assumption. This proposal investigates how an information service can help the user supply that context and reach guidance whose source can be checked.

Home Garden Companion is proposed as an English-language text assistant for beginner tropical indoor and balcony gardeners. It would retrieve relevant gardening passages, explain the guidance in plain language and identify the supporting document pages. When the question lacks essential context, it would ask for clarification. When the collection cannot support an answer, it would state that limitation. The design therefore treats recognising the limits of an answer as part of providing useful guidance.

A language model is appropriate to investigate because users can express the same need in different ways and may need an explanation that combines information from several passages. Whether that explanation improves access to information remains an empirical question. The project will compare the assistant with keyword search over the same approved documents. No user study has yet established demand for this assistant or an improvement in gardening outcomes; the present evidence supports the importance of context, while the proposed comparison will examine the value of the interaction.

The central question is whether a conversational interface can help beginners obtain correct, source-supported guidance more effectively than searching those documents directly. Addressing it requires a usable source collection, response rules and a way to assess both the answers and the user’s task performance. Requirements and preparation work have established an initial basis for that investigation. Application development and user evaluation remain planned.

### 1.2 Related Work and Engineering Gap

Direct access to official guides is the starting point for the proposed service. NParks resources provide identifiable horticultural material that readers can inspect themselves [1–4]. A conversational interface would add interpretation and explanation to that access. To justify the additional complexity, it must preserve the ability to inspect evidence and demonstrate a benefit over searching the source material. Research on retrieval and generation helps identify the technical conditions under which that benefit can be investigated.

Lewis et al. combine a pretrained generator with retrieved information in retrieval-augmented generation, making external knowledge access part of the answer-generation process [5]. This offers a way to supply gardening passages alongside a user’s question rather than depend entirely on knowledge stored in model parameters. It establishes a basis for the architecture, but applying the approach to a small gardening collection still requires decisions about source coverage, passage selection and response evaluation.

Access to a relevant passage addresses only part of the problem. The generated explanation must also represent that passage accurately. Gao et al.’s ALCE evaluates answer correctness and citation quality as separate dimensions [6]. This distinction matters for Home Garden Companion because an answer could point to a real gardening page while drawing a conclusion that the page does not support. The project therefore needs to assess both whether references are present and whether the referenced evidence supports each factual claim.

Selecting more material does not necessarily resolve that difficulty. Liu et al. show that performance on their long-context tasks can depend on where relevant information appears [7]. For this project, the finding motivates testing the selection and organisation of passages supplied to the model. It does not prescribe an optimal chunk size or retrieval configuration. Those choices must be assessed using the gardening documents and questions that the assistant is intended to handle.

These studies identify connected responsibilities: retrieve suitable evidence, use it faithfully and organise it so that the model can apply it. The practical gap addressed here is how to combine those responsibilities with clarification and explicit task limits for beginner gardening questions. The contribution will be the design and evaluation of that application. The project will investigate whether the complete interaction helps users obtain supported guidance, while recording where missing context, incomplete sources or generation errors prevent it from doing so.

### 1.3 Objectives Target Users and Scope

The objectives of this project are:

1. To identify beginner gardeners’ information needs and establish a verified collection of relevant gardening sources.

2. To develop a text-based gardening assistant that provides source-cited guidance and handles unclear, unsupported and excluded questions appropriately.

3. To evaluate the assistant’s correctness, citation support, clarity, usability and response time, including comparison with keyword search over the same approved documents.

The intended users are beginner gardeners caring for tropical indoor or balcony plants. The initial operating context is an English-language, single-user prototype with temporary conversation context and a bounded document collection. Supported tasks include explaining light requirements, interpreting watering principles, discussing growing media and comparing plants when the sources provide sufficient evidence. Accounts, exact household addresses and persistent personal profiles are not required for these tasks.

The scope excludes image-based identification or diagnosis, pesticide dosages and mixing, ingestion advice, safety guarantees, automated watering and live environmental sensing. These exclusions keep the initial work focused on interpreting written guidance rather than identifying plants, prescribing treatments or controlling equipment. Plant comparisons remain within the intended scope only where reviewed sources support them. The current pilot lacks complete plant profiles and structured soil information, so that coverage must be repaired or the supported task list narrowed before application evaluation.

## 2 Requirements Specification

### 2.1 Functional Requirements

A gardener using the assistant needs more than a fluent response. The guidance must address the supported question, remain understandable and provide a way to check its basis. If essential details are missing or the request cannot be answered within scope, the interaction must explain what prevents an answer. Table 1 turns these needs into observable behaviour, retaining the functional requirements from the Week 2 specification [9].

Table 1. Functional requirements and their boundaries.

| ID | The system shall | The system shall not |
|---|---|---|
| FR1 | Answer supported questions about light, water, growing media, space and plant comparisons. | Invent care facts or unsupported fixed watering schedules. |
| FR2 | Attach a document title, URL and one-based PDF page to factual claims. | Fabricate sources or imply that an unsupported claim is sourced. |
| FR3 | Ask for plant or growing-condition details when they are essential to an answer. | Silently assume conditions that could change the guidance. |
| FR4 | Acknowledge insufficient evidence and refuse excluded tasks. | Provide excluded actionable instructions or safety guarantees. |
| FR5 | Explain guidance in plain language and make uncertainty understandable. | Hide uncertainty behind unexplained technical language. |

The appropriate response depends on why an answer cannot yet be given. Clarification allows the user to supply missing context. Abstention acknowledges that the available sources are insufficient. Refusal identifies a request outside the supported scope. Distinguishing these outcomes helps the user understand the next step and prevents evaluation from treating every unanswered question as the same kind of failure.

### 2.2 Nonfunctional and Responsible AI Requirements

The usefulness of those responses also depends on their quality. Correct guidance that arrives too slowly or is difficult to understand may still obstruct the user’s task. The nonfunctional requirements therefore cover response time (NFR1), correctness (NFR2), reliable operation and controlled failure handling (NFR3), and clarity (NFR4). Assessing them together will show whether the prototype provides an interaction that users can complete, rather than only demonstrating that it can generate text.

The interaction creates risks that require more specific checks. A plausible explanation may overstate its evidence, an excluded request may elicit unsafe instructions, or a user may provide unnecessary identifying details. The responsible AI requirements address these cases through citation support and abstention (RAI1), refusal of excluded requests (RAI2), limits on personal-data use (RAI3), and clarification and disclosure of relevant species or climate limitations (RAI4). Each control has a corresponding evaluation condition so that its effectiveness can be examined.

Personal information can be exposed even when it does not appear in the final answer. Privacy verification must therefore inspect outgoing requests and stored logs as well as visible responses. Diagnostic records will be limited to what is needed to investigate failures, with the privacy tests checking whether the implementation actually follows that restriction.

### 2.3 Alignment with Project Objectives

The three objectives require different forms of evidence. Objective 1 depends on identifying user needs and verifying source coverage. Objective 2 depends on implementing the required interaction. Objective 3 tests how well that interaction performs and whether it helps users relative to search. Table 2 makes these links explicit so that progress on preparing data cannot be mistaken for evidence of application performance.

Table 2. Objective and requirement alignment.

| Objective | Relevant requirements | Evidence or planned assessment |
|---|---|---|
| 1. Needs and sources | FR1 scope, FR2 provenance and RAI4 coverage | Source inventory, coverage review and planned user-needs validation. |
| 2. Cited text assistant | FR1–FR5, RAI1–RAI4, NFR1 and NFR3 | Implemented interaction and controls corresponding to architecture elements A2–A8. |
| 3. Evaluate usefulness | NFR1–NFR4 and RAI1–RAI4 | Application tests and comparison with keyword search, recorded through A9. |

The evaluation must consequently examine both individual responses and the task the user is trying to complete. The first establishes whether the system behaves as specified; the second examines whether the added conversational interface is useful.

## 3 Evaluation Criteria

### 3.1 Evaluation Design and Acceptance Criteria

Evaluation will first establish whether the assistant produces correct, supported answers and handles its limits appropriately. Correctness will be assessed against reference facts, while citation assessment will examine the evidence for individual claims. Clarity and response time will indicate how usable the responses are, and refusal, privacy and failure tests will examine the boundaries established in the requirements [10]. A separate comparison with keyword search will then test the proposed benefit to users.

Table 3 defines the principal measures and initial acceptance targets. The targets come from the Week 2 specification and provide a basis for judging the prototype during development. Full citation coverage follows from the requirement that factual claims be traceable. The 85% correctness and 90% clarity thresholds are preliminary engineering goals whose adequacy still needs user validation and error analysis. Similarly, the latency targets express the intended pace of a single-user interaction. Changes to these targets will require a recorded justification; none is presented as an achieved result.

Table 3. Principal evaluation measures and proposed thresholds.

| Requirement | Measurement method and metric | Acceptance target |
|---|---|---|
| NFR2 Correctness | Compare 40 answerable responses with reference facts and pages; report correct-answer rate by topic. | At least 34/40 correct. |
| FR2 / RAI1 Citations | Inspect factual claims for citations and verify support against the cited passages. | 100% citation coverage; at least 95% claim support. |
| RAI1 Abstention | Inspect responses to 20 unsupported questions. | At least 19/20 appropriate abstentions. |
| NFR4 Clarity | Score directness, plain language and readability for the 40 answerable responses. | At least 36/40 score 3/3. |
| NFR1 Latency | Time 40 sequential requests after one excluded warm-up; calculate median and p95. | Median ≤10 seconds; p95 ≤20 seconds. |
| NFR3 Reliability | Check valid response completion on 90 normal cases and controlled handling of five simulated failures. | At least 89/90 normal cases; 5/5 failures handled. |
| RAI3 Privacy | Inspect outgoing payloads, logs and unnecessary requests in 20 synthetic-identifier scenarios. | Zero identifier transmission, persistence or unnecessary requests. |

RAI2 and RAI4 require additional checks. Excluded-task handling must achieve at least 19/20 full refusal-and-redirect successes, with zero excluded actionable instructions or safety guarantees. Ambiguous questions require at least 9/10 appropriate clarifications. All ten designated coverage-limit cases must disclose the relevant limitation. These conditions will be reported separately so that a strong average score cannot conceal a serious boundary failure.

### 3.2 Test Protocol and Failure Treatment

The normal workload comprises 90 cases: 40 answerable, ten ambiguous, 20 unsupported and 20 excluded questions. The answerable set contains ten cases each on light, watering, growing media and space/plant comparisons, including at least eight questions requiring multiple passages. The ten coverage-disclosure cases are a subset of the unsupported set. The 20 privacy scenarios and five simulated service failures are additional tests, avoiding ambiguity about the denominator used for each measure.

A fair assessment requires questions that the source collection can actually answer. Reference facts and supporting pages will therefore be established before questions are assigned to the answerable set. Development cases will be separate from the final evaluation set, and each run will retain the corpus version, model configuration, date and reviewer notes. Correctness, support and clarity will be scored on the same generated responses, allowing weaknesses to be compared without introducing a different answer for each measure.

Failure treatment is part of the protocol. A missing response, error or abstention to an answerable question fails correctness. For citation assessment, a claim is an independently checkable factual assertion. One citation may support several claims only when its passage supports each of them. A response containing no factual claims has no meaningful citation denominator and cannot receive a perfect support score merely by avoiding an answer.

Latency will include retrieval, generation and retries, measured from submission to completion. Unsuccessful requests will be reported separately rather than treated as fast successes. For 40 successful responses, the nearest-rank p95 is the 38th sorted duration. Recording both completion behaviour and timing makes it possible to distinguish a responsive assistant from one that appears fast because requests fail early.

### 3.3 Comparison with Keyword Search

Meeting response-level targets would establish technical performance, but would not show whether the assistant makes information easier to use. The planned user comparison will address that question through matched tasks with the assistant and keyword search over the same approved documents. Both conditions will require a correct answer and supporting evidence. Supported task completion and time to a correct, supported answer will be recorded, with condition order varied to reduce learning effects.

Task completion includes the time spent finding and interpreting information, so it must be measured separately from system latency. Participant count, recruitment, consent and task allocation remain to be specified before the exploratory study begins. The collection also needs enough coverage to support the reference tasks. Using the same collection in both conditions will help distinguish the effect of the interface from differences in access to information.

## 4 AI System Architecture

### 4.1 Components and Information Flow

The proposed architecture separates the responsibilities needed to produce and assess an answer. Input checks establish whether the question can proceed, retrieval supplies evidence, generation explains it, and response checks determine whether the draft meets the task boundaries. Figure 1 shows these as logical responsibilities within one small application [11]. Their separation makes it possible to investigate where a failed response originated.

The home gardener, A1, submits a question through the text interface, A2. Input controls in A3 inspect scope, essential context and personal identifiers before information is sent to an external service. A4 retrieves candidate passages from the source collection, A5, retaining the document and page metadata required for citations. The language component, A6, uses that evidence to draft an explanation. A7 checks the draft’s support and task boundaries before A8 presents the outcome. A9 provides evaluation and minimal diagnostic records across the interaction.

The response path changes when the conditions for an answer are not met. Missing context leads to clarification, insufficient evidence to abstention, and excluded tasks to refusal. Service failures should produce a clear error rather than an invented answer. The methods for detecting identifiers and assessing semantic support still require development experiments. Recording failures at each stage will help distinguish inadequate source coverage from retrieval, generation or response-checking errors.

![Conceptual architecture](../week2_architecture_v1.png)

Figure 1. Home Garden Companion conceptual architecture [11]. The completed preparation pipeline develops A5; the application components remain proposed.

### 4.2 Design Rationale and Accepted Trade Offs

External retrieval gives the assistant access to identifiable gardening documents and allows the source collection to be reviewed independently of the model. It also introduces indexing work, retrieval errors and additional latency. The choice is justified by the need for source-supported guidance, while the keyword-search comparison will test whether generating an explanation adds sufficient value to warrant that complexity.

To make citations dependable, document titles, URLs and page numbers will remain attached to passages throughout preparation and retrieval. The model should not reconstruct these details from memory. This creates additional metadata and validation work, but allows a reviewer to locate the source of a claim. A7 will then assess the relationship between the claim and that evidence, implementing the distinction between reference validity and claim support identified in the literature [6].

Input and output checks address failures at different points. A3 can limit unnecessary transmission and identify questions that need clarification before generation. A7 can examine claims that emerge only in the draft. These controls complement each other, but their effectiveness will depend on tests covering missed identifiers, misleadingly plausible claims and excluded instructions.

Temporary context and the absence of accounts or persistent profiles reduce retention and implementation scope. The trade-off is less personalisation and debugging detail. Logs should use case identifiers and error categories where possible, with privacy tests checking actual transmission and storage.

The initial response path will aim for one generation step using selected evidence. This limits latency and implementation complexity, while allowing less opportunity for iterative repair. Context-selection experiments will examine how the chosen passages and their organisation affect responses [7]. Model/API choice, retrieval technology and the need for a dedicated vector database remain open until development provides a basis for selection. Before those experiments can be meaningful, the project needs passages whose content, source references and task coverage can be verified.

## 5 Data Engineering and Quality

### 5.1 Source Selection and Preparation

The preparation pilot addresses that dependency by testing whether published gardening documents can become usable, traceable passages. Three NParks PDFs were inspected: S01, Introduction to Indoor Gardening, with 24 pages; S02, Know 10 Houseplants, with two pages; and S03, Introduction to Community Gardening, with 20 pages [2–4, 12]. They contain material relevant to the proposed tasks and differ in layout, making them useful for examining both extraction feasibility and the information lost during preparation.

The inspection covered 46 pages, but preparation was deliberately limited to selected prose from S01 pages 5 and 10 and S03 page 6. These three pages produced the five-chunk pilot. The small collection allows individual records to be checked against their sources; it does not yet provide the coverage needed for the complete proposed task set.

For those records to support later citations, their origin must remain identifiable after extraction. The notebook checks exact filenames and expected SHA-256 values, confirms that each PDF can be read, and extracts text page by page using pypdf 6.10.0. It preserves the originals and retains source identity, document title, URL and one-based PDF page with the extracted material. The hashes identify the file versions used in preparation. Separate review is still needed to establish their currency and permission for the intended use.

Extraction exposed problems that a successful file read alone would not reveal. An image-only page in S01 yielded no text, another contained a hidden editorial placeholder, and S02’s multi-column profiles mixed headings with body text. Some structured or icon-based content in S03 was also absent from the text output. Verified cleanup removed the placeholder and repaired known section boundaries while preserving source wording. The houseplant brochure was deferred because an incorrect association between a plant name and its care guidance could produce misleading answers later.

### 5.2 Chunking Storage and Lineage

After cleanup, the comparison examined whether dividing the text damaged its structure. Fixed 500-character cuts and paragraph-aware packing were applied to the same selected text and each produced five chunks. Fixed cuts split two verified sections and one word; paragraph-aware packing split neither. The latter was therefore selected to preserve section boundaries, accepting variable lengths and source-specific preparation rules. Its longest chunk contained 656 characters, showing that 500 characters was a soft packing target. Retrieval performance has not yet been tested, so this result supports text preservation rather than an optimal retrieval setting.

Because the inputs are document snapshots, preparation can run as a batch extract-transform-load process. The prepared records are stored as JSONL, while a manifest records configuration, source mappings and fingerprints. These records allow a passage to be traced back to its source file and page, and make it possible to identify which preparation run produced it.

The public repository records evidence of this process without redistributing full source text. Raw PDFs and extracted passages remain local and are excluded from Git; metadata, original observations and validation evidence are committed. This allows the preparation work to be reviewed while permission for using the source material in the intended assistant remains unresolved.

### 5.3 Pipeline Execution and Verification

The next check was whether the selected preparation process could be repeated from the original files. The integrated V1 runner re-reads the PDFs, verifies their identity and prepares the selected records. It writes a staged JSONL output, then validates the read-back before replacing the previous valid output. This sequence protects the valid output if an input is missing or has changed. Figure 2 shows the processing path and its validation checks [13].

Two local executions produced identical source/output fingerprints, sizes, record counts and mappings. Their five records also matched the Part B output byte for byte. The missing-file and altered-checksum tests both stopped without replacing valid output. These results demonstrate local repeatability and controlled failure handling for the preparation pilot. The notebook supports Colab paths, but a connected Colab execution has not been recorded.

![Preparation pipeline](../week3_pipeline_diagram.png)

Figure 2. Executed document-preparation pipeline [12, 13]. The output supplies the preparation responsibility within A5.

These checks establish that the selected output can be reproduced and protected against the tested input failures. Readiness for the assistant also depends on what that output contains. The quality audit therefore examined the accuracy of the records alongside their coverage, currency and suitability for use.

### 5.4 Quality Findings and Readiness Decision

The Week 4 audit examined all five prepared records, using the chunk as the unit of analysis [14]. Every record contained the required citation fields and consistent metadata. V1 checked references against the source register, PDFs and manifest; V2 checked selected-prose fidelity and heading/body associations through documented manual comparison. Both checks passed 5/5. No duplicate identifiers or whitespace-normalised exact duplicate texts were found. The 166-character and 656-character chunks were accepted exceptions because length alone did not indicate a content defect.

The records passed those checks, but the collection still omitted information needed for some intended tasks. It contained general guidance without complete plant profiles for comparisons, and extraction had omitted the soil-ratio table. These findings explain why accurate individual passages are insufficient to establish adequate task coverage. Deferring complex layouts while retaining readily extracted prose may favour generic advice in later retrieval; this is a preparation risk rather than an observed model outcome. Timeliness remains Not Verified because publication/revision status and a task-based freshness criterion have not been established.

Suitability for use also requires a separate review of privacy and source permissions. No personal identifiers or private conversations were found in the five inspected prose records, although that finding cannot establish how future user inputs will be handled. The rights review found no recorded authorisation for the intended AI processing/service or redistribution. Public availability was not taken to establish an open licence, and the intended use still needs to be assessed against the NParks terms [8].

The audit therefore records HOLD on using the pilot as the intended answer corpus or in a public AI service. The unresolved issues are permission, incomplete task coverage and unverified currency. The completed preparation remains useful coursework evidence and identifies what must change before implementation can proceed on an approved collection. The next review will require documented use rights or licensed replacements, coverage of the agreed tasks, verified versions and repeated validation of the revised records.

## 6 Implementation Plan and Conclusion

### 6.1 Implementation Stages and Expected Contribution

The implementation sequence follows from those findings. First, intended-use rights and source versions must be confirmed, or the material replaced with appropriately licensed sources. Beginner information needs must also be validated and translated into an agreed task list. Establishing these conditions together will prevent the collection from expanding without a clear relationship to the questions the assistant is expected to answer.

Second, preparation will address the identified coverage gaps through reviewed plant profiles and structured information, or the supported scope will be narrowed. Each supported task will be linked to source evidence. Reference and fidelity checks will be repeated, and manifests updated, before a new decision on readiness. Subsequent source changes, revised requirements or reported errors will trigger revalidation.

Third, an approved collection will support implementation of the text interface, retrieval, cited drafting and response controls. Model and retrieval configurations will be selected using development cases. A keyword-search interface will access the same documents, establishing a comparison that tests the effect of the conversational interaction while holding the available information constant.

Fourth, application testing will assess the proposed acceptance criteria and record the reasons for failures. Results will include the denominators and topic breakdowns needed to interpret correctness, alongside claim support, clarity, timing and boundary handling. The exploratory user comparison will proceed after recruitment, consent and task-allocation procedures are defined. Any resulting changes will be versioned so that improvements can be linked to the observations that motivated them.

The expected contribution is an evaluated gardening assistant supported by traceable sources and a repeatable preparation process. The existing pilot establishes part of that foundation. The remaining work will determine whether the proposed interaction meets its technical requirements and offers a measurable benefit to its intended users.

### 6.2 Conclusion

Home Garden Companion investigates whether a conversational interface can help beginners obtain correct, source-supported gardening guidance. The context required to interpret gardening advice motivates clarification; the risk of misrepresenting source material motivates citations and claim-support checks. The evaluation combines those technical requirements with a comparison against keyword search, so that a working implementation can be assessed in terms of the task it is intended to support.

The completed preparation pilot shows that selected prose can be converted into repeatable records with document and page references. Its audit also shows why further source work is necessary: the current collection has unresolved permission, coverage and currency issues. Resolving those issues will create a basis for implementation and testing. The proposal’s eventual contribution will depend on the evidence from that evaluation, including cases where the assistant does not improve on direct search.


## References

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
