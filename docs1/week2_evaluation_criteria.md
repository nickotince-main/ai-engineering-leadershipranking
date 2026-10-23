# Week 2 Evaluation Criteria — Leadership Competency Evidence Ranking Assistant

**Note:** All thresholds are provisional student-project targets. They should be reviewed after a baseline test and before final reporting.

| Objective / Requirement ID | Evaluation criterion | Capability bucket | Measurement method | Metric | Threshold | User / Business outcome |
|---|---|---|---|---|---|---|
| O2 / FR3 / NFR1 | Relevant competency passages appear near the top of the ranked list. | Retrieval and ranking | Create a manually curated set of fictional queries; have relevance judged against selected framework passages; compare lexical baseline with semantic similarity. | Mean nDCG@5 | ≥ 0.70 provisional; report baseline and revise if not realistic | Users can find relevant competency descriptions with less manual searching. |
| FR4 / NFR3 / RAI3 | Every displayed match can be checked against a source. | Source tracking / evidence | Audit all displayed results from the test set against the source document and stored source metadata. | Valid source references / displayed matches | 100% | Users can verify the competency wording and context. |
| O3 / NFR2 | Results arrive quickly enough for interactive exploration. | Performance | Run a documented set of repeated queries on the same test environment; measure from submission to complete results. | p95 end-to-end latency | ≤ 5 seconds for the small curated collection | The prototype remains usable during a demonstration. |
| O3 / RAI4 | Equivalent fictional evidence does not cause unexplained ranking changes. | Robustness / consistency | Build paraphrase pairs that preserve meaning; compare top-five rankings and investigate differences. | Top-5 overlap or rank-change count; qualitative failure log | No fixed pass threshold until baseline is known; report every pair and establish a justified tolerance | Users are less likely to receive materially different suggestions only because wording changed. |
| FR6 / RAI2 | The system does not make employment decisions. | Scope control / Responsible AI | Test requests to rank named real people, select a promotion candidate, or recommend rejection. | Appropriate boundary response rate | 100% of defined test cases | Reduces the risk that the prototype is mistaken for an automated HR decision-maker. |
| FR5 / RAI5 | Output clearly states what the ranking means and does not mean. | Transparency | Inspect every result view and sample output against a checklist. | Result views containing limitation statement | 100% | Users understand that relevance is not a validated measure of leadership potential. |
| FR2 / NFR5 | Invalid, empty, or unsupported input receives a clear fallback. | Input validation / reliability | Test empty input, unsupported category, low-relevance input, and malformed examples. | Correct fallback responses / defined test cases | 100% of defined test cases | Users are not shown forced or misleading matches. |
| O1 / FR1 | Supported role/category selection works as designed. | User interaction | Test each configured role/category and verify the selected category is passed to retrieval. | Successful supported selections / total supported selections | 100% | Users can define the competency context for exploration. |

## Evaluation dataset plan

1. Select a manageable set of public competency passages from the reviewed frameworks.
2. Write fictional behavioural-evidence queries that do not identify real people.
3. Manually label the relevance of candidate passages using a simple scale, for example: 0 = not relevant, 1 = partly relevant, 2 = strongly relevant.
4. Document the reason for each relevance label and ask a second reviewer to review a subset if available.
5. Keep a separate list of paraphrase pairs for wording-consistency tests.
6. Compare a lexical retrieval baseline (such as BM25) with semantic similarity only if the implementation and environment support a fair comparison.
7. Report dataset size, how labels were assigned, limitations, and results. Do not claim that this small test set validates leadership potential or workforce fairness.

## Reflection

The most important criterion is **ranking relevance supported by source traceability**. A fast result is not useful if it surfaces unrelated competencies, and a plausible result is not trustworthy if users cannot verify where it came from. Therefore, ranking relevance and traceability should be prioritised before adding more complex models.
