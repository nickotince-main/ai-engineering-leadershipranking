# Week 2 — V1 Architecture Decisions & Traceability

**Project:** Leadership Competency Evidence Ranking Assistant
**Student:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)
**Version:** Conceptual V1 — technology choices remain provisional.

See `week2_architecture_v1.png` for the full diagram. Flow: **User input → scope/input validation → curated document retrieval and ranking → evidence/explanation assembly → result display**, with a separate offline evaluation workflow (not part of the user-facing response path).

---

## Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| Use public competency documents and fictional inputs only | FR2, FR4, RAI1, RAI2, RAI3 | (a) Use real employee records; (b) Use only hard-coded example results | (a rejected — access, consent, privacy, bias and validation requirements exceed project scope; (b) rejected — would not meaningfully evaluate retrieval/ranking) → **Public frameworks + fictional evidence** | Public frameworks support traceable document retrieval but cannot train or validate prediction of actual leadership success; fictional queries may not represent real-world language. |
| Start with a lexical baseline before adding semantic ranking | FR3, NFR1, O2 | (a) Semantic similarity only; (b) Supervised ranking (RankNet/LambdaRank); (c) Manual keyword rules only | **Lexical baseline (e.g. BM25) first**, semantic similarity added only as a comparison if feasible | A lexical baseline may miss semantic matches; semantic similarity may retrieve text that sounds related but isn't actually relevant — both must be tested on the same labelled query set. Supervised ranking deferred: no suitable labelled dataset exists yet. |
| Preserve source metadata through every processing stage | FR4, NFR3, RAI3 | (a) Return generated summaries without source links; (b) Attach only a document-level link | **Each passage keeps document ID, title, URL, passage ID, and section/page when available**; result builder must not display a passage without its source metadata | Adds implementation and testing work, and PDF extraction may not preserve page/section data perfectly — accepted because unverifiable output is the core risk this project exists to avoid. |
| Keep employment-decision controls separate from ranking relevance | FR5, FR6, RAI2, RAI5 | (a) Permit employee ranking with a disclaimer; (b) Remove all HR-related content entirely | **Input/output boundary explicitly excludes real-person ranking and employment recommendations**; interface describes results as document relevance, not an employee score | The prototype cannot be used for actual succession or promotion decisions — intentional and appropriate given the available data and project scope; a disclaimer alone was judged insufficient to control the core misuse risk. |

---

## Initial Requirements Traceability Matrix

| Objective | Requirement / Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|
| O1 | FR1/FR2 — context selection and fictional input | User interface + input validation | [To be collected: test supported options, empty input, fictional-data guidance] |
| O2 | FR3/NFR1 — ranking relevance (nDCG@5 ≥ 0.70) | Document preparation + retrieval/ranking | [To be collected: labelled query set evaluation, baseline vs. semantic comparison] |
| O2 | FR4/NFR3/RAI3 — source traceability (100%) | Metadata store + evidence assembly | [To be collected: audit of every displayed match's source link] |
| O3 | NFR2 — response time (p95 ≤ 5s) | Retrieval pipeline + evaluation instrumentation | [To be collected: repeated end-to-end query timing] |
| O3 | RAI4 — wording consistency | Ranking component + offline evaluation | [To be collected: paraphrase pair comparison, baseline + tolerance] |
| O3 | FR6/RAI2 — employment-decision boundary (100%) | Input/output scope control | [To be collected: promotion/rejection/real-person-ranking test cases] |
| O3 | FR5/RAI5 — limitations shown (100%) | Result presenter | [To be collected: inspection of all result views for limitation text] |

---

## Known Limitations

- Public frameworks are not a labelled dataset; the system can retrieve relevant text but cannot infer real leadership success.
- Frameworks use different terminology from different contexts — mapping across them requires care.
- Semantic similarity can produce plausible but incorrect matches; a citation does not automatically guarantee relevance.
- Synthetic paraphrase tests provide limited evidence and cannot prove fairness across real people or groups.
- The architecture is conceptual — specific libraries, model choices, hosting, and data storage are selected after a small prototype and evaluation.

---

### Reflection

**Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?**

Keeping employment-decision controls separate from ranking relevance was the most important trade-off. It was driven directly by RAI2 and RAI5, and by the project's own problem framing: a ranked list can easily be mistaken for a judgement about a person, especially in an HR-adjacent context. Accepting this decision means the prototype is permanently unable to support the exact use case (real succession/promotion decisions) that first motivated the topic — but a disclaimer alone was judged insufficient to control that misuse risk, so the scope boundary was built into the architecture itself rather than left to interface wording.
