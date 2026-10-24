# Week 2 — V1 Architecture Decisions & Traceability

**Project:** LeadRanking — Leadership Competency Evidence Ranking Assistant
**Version:** Conceptual V1 — technology choices remain provisional.

See `week2_architecture_v1.png` for the full diagram (flow: User Interface → Scope & Input Checks → Public Documents → Retrieval & Ranking → Evidence Assembly → Results to User, with Document Preparation, Source Metadata, and Offline Evaluation as supporting components).

---

## Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| Use public competency documents and fictional inputs only | FR2, FR4, RAI1, RAI2, RAI3 — leadership data can be sensitive, and the prototype has no validated employee-level outcome labels | (a) Use real employee records — rejected: access, consent, privacy, bias, and validation requirements exceed project scope; (b) Use only hard-coded example results — simpler, but would not meaningfully evaluate retrieval/ranking over documents | Use a small, curated set of public frameworks and fictional behavioural evidence; do not collect or rank real employee profiles | Public frameworks support traceable document retrieval but cannot train or validate prediction of actual leadership success; fictional queries may not represent real-world language. |
| Start with a lexical baseline before adding semantic ranking | FR3, NFR1, O2 — the project needs a measurable ranking baseline; supervised learning-to-rank would require relevance labels not yet available | (a) Semantic similarity only — rejected as sole starting point, lacks a simple baseline for comparison; (b) Supervised ranking (RankNet/LambdaRank) — deferred, no suitable labelled dataset established; (c) Manual keyword rules only — simple reference, but brittle for varied wording | Begin with a lexical retrieval baseline (e.g. BM25); add semantic similarity as a comparison if the environment supports it | A lexical baseline may miss semantic matches; semantic similarity may retrieve text that sounds related but isn't. Both must be tested on the same labelled query set. |
| Preserve source metadata through every processing stage | FR4, NFR3, RAI3 — ranking output must be verifiable; metadata lost during extraction/chunking breaks traceability | (a) Return generated summaries without source links — rejected, users cannot verify evidence; (b) Attach only a document-level link — acceptable fallback if page/section data can't be extracted, but less precise | Each passage keeps a document ID, title, URL, passage ID, and section/page information when available; the result builder must not display a passage without its source metadata | Adds implementation and testing work, and PDF extraction may not preserve page/section information perfectly. |
| Keep employment-decision controls separate from ranking relevance | FR5, FR6, RAI2, RAI5 — a ranked list may be mistaken for a judgement about a person, particularly in an HR context | (a) Permit employee ranking with a disclaimer — rejected, a disclaimer alone does not control the core misuse risk; (b) Remove all HR-related content — rejected, the bounded competency-exploration use case remains feasible | Input and output boundaries explicitly exclude real-person ranking and employment recommendations; the interface describes results as document relevance, not an employee score | The prototype cannot be used for actual succession or promotion decisions — intentional and appropriate given the available data and project scope. |

---

## Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|---|
| O1 | FR1 / FR2 | Context selection and fictional input work as designed | User Interface + Scope & Input Checks | [To be collected: test supported options, empty input, and fictional-data guidance] |
| O2 | FR3 / NFR1 | Ranking relevance (nDCG@5 ≥ 0.70 provisional) | Document Preparation + Retrieval & Ranking | [To be collected: evaluate manually labelled query set; compare baseline vs. semantic approach] |
| O2 | FR4 / NFR3 / RAI3 | Source traceability (100% valid references) | Source Metadata + Evidence Assembly | [To be collected: audit every displayed match and its source link] |
| O3 | NFR2 | Response time (p95 ≤ 5s, provisional) | Retrieval & Ranking + Offline Evaluation | [To be collected: measure repeated end-to-end queries] |
| O3 | RAI4 | Wording consistency (tolerance TBD) | Retrieval & Ranking + Offline Evaluation | [To be collected: compare equivalent paraphrase pairs, record rank changes] |
| O3 | FR6 / RAI2 | Employment-decision boundary (100% of tests remain in scope) | Scope & Input Checks | [To be collected: test promotion, rejection, and real-person ranking requests] |
| O3 | FR5 / RAI5 | Limitations shown (100% of result views) | Results to User | [To be collected: inspect all result views for score meaning and limitation text] |

---

### Reflection

**Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?**

Keeping employment-decision controls separate from ranking relevance was the most important trade-off. It was driven directly by RAI2 and RAI5 — the risk that a ranked list of competency passages gets misread as a judgement about a real person. The trade-off accepted is a real limitation on usefulness: the prototype cannot support the succession-planning or promotion use cases that first motivated the problem statement. That was accepted deliberately, because a disclaimer alone was judged insufficient to control the misuse risk — the boundary needed to be enforced structurally (input/output scope checks), not just stated.
