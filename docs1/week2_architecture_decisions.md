# Week 2 Architecture Decisions and Traceability

**Project:** Leadership Competency Evidence Ranking Assistant  
**Version:** Conceptual V1  
**Status:** Proposed architecture; technology choices remain provisional.

## 1. Architecture summary

The V1 design follows the smallest flow that supports the defined requirements:

**User input → scope/input validation → curated document retrieval and ranking → evidence/explanation assembly → result display**

A separate evaluation workflow tests relevance, traceability, latency, wording consistency, and scope boundaries. It is not part of the normal user-facing response path.

## 2. Architecture needs derived from requirements

| Requirement / evaluation need | Required capability | V1 architecture response |
|---|---|---|
| FR1 / FR2: select context and accept fictional evidence | User interaction and input validation | Input interface with supported category selection and a clear fictional-data notice |
| FR3 / NFR1: rank relevant passages | Search/index and ranking | Curated document loader, passage segmentation, lexical baseline, optional semantic-similarity ranker |
| FR4 / NFR3 / RAI3: verifiable sources | Metadata preservation and evidence assembly | Store document title, URL, section/page when available, and passage ID; attach source metadata to each result |
| FR5 / RAI5: explain limitations | Output formatting and explanation | Result presenter labels results as text relevance and includes a limitation statement |
| FR6 / RAI2: refuse employment decisions | Scope control | Input/output boundary checks and tested response templates for real-person ranking or promotion decisions |
| FR7 / NFR5: no forced answer | Low-relevance fallback | Use a threshold selected after baseline testing; return a no-good-match message when appropriate |
| NFR2: latency | Measurement and optimisation | Record end-to-end query latency during evaluation |
| RAI1: privacy | Data minimisation | Use only fictional examples; do not persist user profile text by default in the prototype |

## 3. V1 conceptual data flow

1. **User interface (grey):** user selects a supported competency area and enters fictional behavioural evidence.
2. **Input validation and scope control (orange):** checks empty input, unsupported requests, and requests to make employment decisions.
3. **Public document collection (green):** curated competency frameworks and metadata (title, URL, section/page where available).
4. **Document preparation (green):** extract text, preserve source metadata, split into manageable passages, and prepare a search index.
5. **Retrieval and ranking (blue):** lexical retrieval baseline; semantic-similarity method may be added for comparison if feasible.
6. **Evidence and explanation assembly (blue):** packages ranked passages with their source references and describes why they matched in terms of query-to-text relevance, without claiming personal assessment validity.
7. **Result display (grey):** shows ranked competency passages, source links, and development-reflection prompts.
8. **Evaluation and monitoring (purple, offline):** curated test queries, relevance labels, nDCG@5, traceability audit, latency, paraphrase consistency, and scope-control tests.

## 4. Architecture Decision Records (ADRs)

### ADR-1: Use public competency documents and fictional inputs only

**Context:** Leadership-related data can be sensitive, and the prototype does not have validated employee-level outcome labels.

**Decision:** Use a small, curated set of public frameworks and fictional behavioural evidence. Do not collect or rank real employee profiles.

**Alternatives considered:**
- Use real employee records: rejected because access, consent, privacy, bias, and validation requirements exceed the project scope.
- Use only hard-coded example results: simpler, but would not meaningfully evaluate retrieval/ranking over documents.

**Trade-off:** Public frameworks support traceable document retrieval but cannot train or validate prediction of actual leadership success. Fictional queries may not represent real-world language.

**Requirements supported:** FR2, FR4, RAI1, RAI2, RAI3.

### ADR-2: Start with a lexical baseline before adding semantic ranking

**Context:** The project needs a measurable ranking baseline. A supervised learning-to-rank model would require relevance labels and enough suitable training data.

**Decision:** Begin with a lexical retrieval baseline (for example BM25). Add semantic similarity as a comparison if the chosen environment supports it. Do not promise supervised learning-to-rank in V1 unless suitable labelled data and evaluation design are available.

**Alternatives considered:**
- Semantic similarity only: rejected as the sole starting point because it would lack a simple baseline for comparison.
- Supervised ranking (e.g. RankNet/LambdaRank): deferred because no appropriate labelled dataset has been established.
- Manual keyword rules only: useful as a simple reference, but potentially brittle for varied wording.

**Trade-off:** A lexical baseline may miss semantic matches; semantic similarity may retrieve text that sounds related but is not actually relevant. Both must be tested on the same labelled query set.

**Requirements supported:** FR3, NFR1, O2.

### ADR-3: Preserve source metadata through every processing stage

**Context:** Ranking output must be verifiable. If source metadata is lost during text extraction or chunking, the system cannot reliably show where a result came from.

**Decision:** Each passage keeps a document ID, title, URL, passage ID, and section/page information when available. The result builder must not display a passage without its source metadata.

**Alternatives considered:**
- Return generated summaries without source links: rejected because users cannot verify the evidence.
- Attach only a document-level link: acceptable fallback if page/section data cannot be extracted, but less precise.

**Trade-off:** Metadata handling adds implementation and testing work, and PDF extraction may not preserve page/section information perfectly.

**Requirements supported:** FR4, NFR3, RAI3.

### ADR-4: Keep employment-decision controls separate from ranking relevance

**Context:** A ranked list may be mistaken for a judgement about a person, particularly in an HR context.

**Decision:** Input and output boundaries explicitly exclude real-person ranking and employment recommendations. The interface describes results as document relevance, not an employee score.

**Alternatives considered:**
- Permit employee ranking with a disclaimer: rejected because a disclaimer alone does not control the core misuse risk.
- Remove all HR-related content: rejected because the bounded competency-exploration use case remains feasible.

**Trade-off:** The prototype cannot be used for actual succession or promotion decisions; this is intentional and appropriate for the available data and project scope.

**Requirements supported:** FR5, FR6, RAI2, RAI5.

## 5. Traceability matrix

| Objective | Requirement / evaluation criterion | Architecture component | Verification activity | Later test / result |
|---|---|---|---|---|
| O1 | FR1 / FR2: context selection and fictional input | User interface + input validation | Test supported options, empty input, and fictional-data guidance | To be completed during implementation |
| O2 | FR3 / NFR1: ranking relevance | Document preparation + retrieval/ranking | Evaluate manually labelled query set using nDCG@5; compare baseline and semantic approach | To be completed after baseline |
| O2 | FR4 / NFR3 / RAI3: source traceability | Metadata store + evidence assembly | Audit every displayed match and its source link | Target: 100% valid source references |
| O3 | NFR2: response time | Retrieval pipeline + evaluation instrumentation | Measure repeated end-to-end queries | Target: p95 ≤ 5 seconds, provisional |
| O3 | RAI4: wording consistency | Ranking component + offline evaluation | Compare equivalent paraphrase pairs and record rank changes | Baseline and tolerance to be established |
| O3 | FR6 / RAI2: employment-decision boundary | Input/output scope control | Test promotion, rejection, and real-person ranking requests | Target: 100% of defined tests remain in scope |
| O3 | FR5 / RAI5: limitations shown | Result presenter | Inspect all result views for score meaning and limitation text | Target: 100% of result views |

## 6. Trade-offs and known limitations

- Public frameworks are not a common labelled dataset; the system may be able to retrieve relevant text but cannot infer real leadership success.
- Frameworks use different terminology and were created for different contexts. Mapping across them requires care.
- Semantic similarity can produce plausible but incorrect matches; source citations do not automatically guarantee relevance.
- Synthetic paraphrase tests provide limited evidence and cannot prove fairness across real people or groups.
- The architecture is conceptual. Specific libraries, model choices, hosting, and data storage will be selected after a small prototype and evaluation.

## 7. Architecture review checklist

- [x] Every major component maps to at least one requirement or evaluation need.
- [x] Source tracking is included in the data flow.
- [x] Privacy and scope controls are included.
- [x] Evaluation is represented as an offline workflow.
- [x] Supervised learning-to-rank is not assumed without suitable labels.
- [ ] Validate all requirements against the implemented prototype.
- [ ] Update decisions and traceability after actual test results.
