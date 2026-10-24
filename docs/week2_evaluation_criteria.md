# Week 2 Evaluation Criteria — LeadRanking (Leadership Competency Evidence Ranking Assistant)

**Note:** All thresholds are provisional student-project targets, to be reviewed after a baseline test.

---

| Requirement ID | Linked Objective | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold / Expected Outcome |
|---|---|---|---|---|---|---|
| FR1 | O1 | Supported role/category selection works as designed. | Instruction-following capability | Test each configured role/category and verify the selected category is passed to retrieval. | Successful supported selections / total supported selections | 100% — users can define the competency context for exploration. |
| FR2 | O1 | Invalid, empty, or unsupported input receives a clear fallback. | Instruction-following capability | Test empty input, unsupported category, low-relevance input, and malformed examples. | Correct fallback responses / defined test cases | 100% — users are not shown forced or misleading matches. |
| FR3 / NFR1 | O2 | Relevant competency passages appear near the top of the ranked list. | Domain-specific capability | Create a manually curated set of fictional queries; have relevance judged against selected framework passages; compare lexical baseline with semantic similarity. | Mean nDCG@5 | ≥ 0.70 provisional — users can find relevant competency descriptions with less manual searching. |
| FR4 / NFR3 / RAI3 | O2 | Every displayed match can be checked against a source. | Generation capability | Audit all displayed results from the test set against the source document and stored source metadata. | Valid source references / displayed matches | 100% — users can verify the competency wording and context. |
| NFR2 | O3 | Results arrive quickly enough for interactive exploration. | Cost and latency | Run a documented set of repeated queries on the same test environment; measure from submission to complete results. | p95 end-to-end latency | ≤ 5 seconds for the small curated collection — prototype stays usable during a demonstration. |
| RAI4 | O3 | Equivalent fictional evidence does not cause unexplained ranking changes. | Instruction-following capability | Build paraphrase pairs that preserve meaning; compare top-five rankings and investigate differences. | Top-5 overlap or rank-change count; qualitative failure log | No fixed threshold until baseline is known; report every pair and set a justified tolerance. |
| FR6 / RAI2 | O3 | The system does not make employment decisions. | Instruction-following capability | Test requests to rank named real people, select a promotion candidate, or recommend rejection. | Appropriate boundary response rate | 100% of defined test cases — reduces risk the prototype is mistaken for an automated HR decision-maker. |
| FR5 / RAI5 | O3 | Output clearly states what the ranking means and does not mean. | Generation capability | Inspect every result view and sample output against a checklist. | Result views containing limitation statement | 100% — users understand that relevance is not a validated measure of leadership potential. |

## Evaluation Dataset Plan

1. Select a manageable set of public competency passages from the reviewed frameworks.
2. Write fictional behavioural-evidence queries that do not identify real people.
3. Manually label the relevance of candidate passages using a simple scale (0 = not relevant, 1 = partly relevant, 2 = strongly relevant).
4. Document the reason for each relevance label and ask a second reviewer to review a subset if available.
5. Keep a separate list of paraphrase pairs for wording-consistency tests.
6. Compare a lexical retrieval baseline (such as BM25) with semantic similarity only if the implementation and environment support a fair comparison.
7. Report dataset size, how labels were assigned, limitations, and results. Do not claim this small test set validates leadership potential or workforce fairness.

---

### Reflection

**Which evaluation criterion is most important for determining whether your AI application will be useful to its intended users? Why?**

Ranking relevance supported by source traceability (FR3/NFR1 together with FR4/NFR3/RAI3) is the most important. A fast result is not useful if it surfaces unrelated competencies, and a plausible result is not trustworthy if users cannot verify where it came from. Ranking relevance and traceability should be prioritised before adding more complex models.
