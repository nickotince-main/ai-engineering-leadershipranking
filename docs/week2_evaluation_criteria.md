# Week 2 Evaluation Criteria — TalentRank (Explainable Machine Learning for Employee Promotion Prediction and Ranking)

**Version:** 1.0. Thresholds are proposed targets, not measured results — review after the first baseline experiment and update with reasons if needed.

The evaluation uses the public 54,808-record employee promotion dataset to study **historical promotion outcomes**. Its label does not validate leadership potential or suitability for a particular management role. A probability-sorted list is therefore an exploratory ordering unless a defensible ranking reference is available.

---

| Requirement ID | Linked Objective | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold / Expected Outcome |
|---|---|---|---|---|---|---|
| FR1 | O1 | Dataset quality and target understanding | Domain-specific capability | Run a documented data audit before modelling: check dimensions, target distribution, missing values, duplicate rows, feature definitions, and possible target leakage. | Data-audit checklist completion; counts/percentages for missing values, duplicates, each target class | 100% of planned checks reported; unresolved issues and assumptions documented before training. |
| FR3 / NFR1 | O2 | Comparison with a simple baseline | Domain-specific capability | Train at least two suitable classifiers and a simple baseline using the same train/test split and preprocessing pipeline; compare on held-out data. | F1-score and PR-AUC as primary metrics; also precision, recall, ROC-AUC | Selected model should improve PR-AUC over baseline, or show a justified trade-off; report the actual result either way. |
| FR5 | O2 | Held-out predictive performance | Domain-specific capability | Evaluate the final selected model once on the held-out test set after model selection; report confusion matrix and classification metrics. | Precision, recall, F1-score, ROC-AUC, PR-AUC, confusion matrix | Report all applicable metrics and the baseline comparison; no claim of a universal minimum score before observing baseline results. |
| FR4 / NFR4 | O2 | Ranking validity and limitations | Domain-specific capability | Sort test records by predicted promotion probability; first determine whether defensible relevance labels or a reference ranking exist; if so calculate a suitable ranking metric, otherwise describe the ordering as exploratory. | Availability/documentation of a valid ranking target; NDCG@k only if suitable | 100% of ranking claims state their target and limitations; no validated ranking quality claimed without a defensible reference. |
| FR6 / RAI3 | O3 | Explanation clarity and non-causal wording | Generation capability | Review a sample of feature explanations and output text against a checklist confirming explanations describe model behaviour, not causation. | % of reviewed explanations passing the non-causal wording checklist | 100% avoid causal claims; unsuitable explanations corrected or flagged. |
| RAI1 | O1, O3 | Group-wise performance and fairness limitations | Domain-specific capability | Where relevant group attributes, sufficient sample sizes, and appropriate permissions are available, compare group-level error or selection-rate measures; record sample sizes and uncertainty. | Group-level metric differences and record of checks/sample sizes/limitations | Complete and report every planned group check; no claim the model is fair solely because differences are small or data insufficient. |
| RAI2 / RAI5 | O3 | Transparency of intended use and dataset target | Instruction-following capability | Inspect project documentation, interface, and result/report views for the required limitation statement. | % of relevant views/sections containing the statement | 100% state that predictions support analysis only, require human review, and represent historical outcomes — not validated leadership potential. |
| NFR2 | O2 | Reproducibility of the experiment | Cost and latency | Re-run the documented pipeline with the same split, preprocessing, configuration, and random seeds; compare predictions and metrics. | Difference in reported metrics/predictions under the same configuration | Deterministic steps reproduce identical results; any expected variation explained and documented. |
| NFR3 | O2 | Practical experiment runtime | Cost and latency | Record end-to-end training/evaluation time for the selected dataset on the documented development environment. | Total training and evaluation runtime | Provisional: complete a full experiment within 10 minutes; reassess after the first baseline run. |

## Evaluation Notes

1. **Use a held-out test set.** Do not use test-set results to select features, tune model parameters, or choose a decision threshold.
2. **Account for class imbalance.** Report precision, recall, F1-score, and PR-AUC where suitable; accuracy alone is insufficient.
3. **Keep ranking claims narrow.** Sorting by predicted probability is not the same as validating promotion suitability — use NDCG@k or another ranking metric only if a defensible relevance target is available.
4. **Interpret explanations carefully.** Feature importance or SHAP-style values describe how the model uses features; they do not establish causation.
5. **Treat fairness results as limited evidence.** Report group sample sizes, uncertainty, and missing attributes — absence of a detected disparity does not prove fairness.
6. **Record actual results later.** This file specifies the evaluation plan; fill in measured scores and observations after running the experiments.

---

### Reflection

**Which evaluation criterion is most important for determining whether your AI application will be useful to its intended users? Why?**

RAI2/RAI5 (transparency of intended use and dataset target) is the most important. The project's central risk is not that the model performs poorly — it's that an accurate-looking prediction gets mistaken for a validated measure of leadership potential and used to justify a real promotion decision. Every other criterion in this table (predictive performance, ranking validity, explanation quality) only matters if users correctly understand what the output does and doesn't mean. If the transparency requirement fails, even a technically strong model becomes actively harmful rather than merely unhelpful — which is a stronger failure mode than, for example, a model that simply underperforms the baseline.
