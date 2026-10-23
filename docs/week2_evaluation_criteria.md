# Week 2 Evaluation Criteria — LeadReady

**Student:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)

---

| Requirement ID | Linked Objective | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold / Expected Outcome |
|---|---|---|---|---|---|---|
| FR3 | O1 | Does the system rank employees correctly against the defined role requirements? | Domain-specific capability | Compare the system's rank order for a small test set of employees against a "gold" rank order produced manually by a human rater using the same role requirements. | Rank correlation (Spearman's rho) between system ranking and human gold ranking. | rho ≥ 0.7 — close enough to human judgement to be useful as a decision-support starting point, not a final decision. |
| FR4 | O2 | Does the generated explanation accurately and clearly reflect the competency data behind each rank? | Generation capability | Human review of a sample of generated explanations, checking factual accuracy against source data and clarity (simple rubric). | % of explanations rated "accurate and clear" by the reviewer. | ≥ 90% — users need to trust the explanation enough to act on it; this is the feature that differentiates LeadReady from an unexplained leaderboard. |
| NFR3 | O1, O3 | Can the system produce a full ranked-and-explained batch output within a usable time for an HR review session? | Cost and latency | Timed test runs on batches of 50 employees against one role. | Average response time (seconds) per batch. | ≤ 30 seconds per 50-employee batch — fits a practical review workflow without disrupting the session. |
| RAI1 | O3 | Do the top-ranked outputs show disproportionate representation across demographic groups? | Domain-specific capability | Compute the selection rate of each demographic group among top-ranked employees, across multiple test runs on the dataset. | Disparate impact ratio (protected group selection rate ÷ reference group selection rate). | ≥ 0.8 for each tracked group — meets the commonly used "4/5ths rule" fairness benchmark. |

---

### Reflection

**Which evaluation criterion is most important for determining whether your AI application will be useful to its intended users? Why?**

FR4 (explanation accuracy and clarity) is the most important. LeadReady's entire value proposition over existing tools (Gloat, SAP SuccessFactors, generic LTR-based rankers) is that it explains *why* an employee ranks where they do, rather than returning an unjustified score or leaderboard position — that was the specific engineering gap identified in Section 0. If the ranking itself is accurate (FR3) but the explanation is unclear or factually wrong, HR users gain nothing over the opaque tools reviewed in related work, and the project fails on its own stated objective (O2) even if the underlying ranking logic works.
