# Week 2 — V1 Architecture Decisions & Traceability — TalentRank

**Version:** 1.0 — V1 conceptual design; implementation choices may change after baseline experiments.

See `week2_architecture_v1.png` for the full diagram (flow: HR Specialist → Prototype Interface → Use & Scope Control → Public HR Dataset → Data Inspection & Preprocessing → Experimental Data Split → Model Training & Comparison → Prediction & Exploratory Ranking + Offline Evaluation → Model Explanation + Responsible AI Review → Results Dashboard/Report → Human Review by HR/Management).

## Architecture Needs Summary

| Requirement ID / Objective | What the requirement needs | Architecture response |
|---|---|---|
| O1 / FR1 | Inspect the public dataset and understand its target, features, missing values, class balance. | Data inspection & preprocessing stage reporting dataset shape, target distribution, missing values, duplicates, feature types. |
| O1 / FR2 | Prepare usable model inputs without leaking test information. | Reproducible preprocessing pipeline + documented train/validation/test split; transformations fit on training data only. |
| O2 / FR3 | Compare models fairly against a simple baseline. | Model-training component running a baseline and selected classifiers on the same split and protocol. |
| O2 / FR4 | Show a probability-based ordering for exploratory analysis. | Prediction component sorting records by estimated probability; labeled explicitly as exploratory, not validated promotion readiness. |
| O3 / FR5 | Report predictive performance, including the minority promoted class. | Offline evaluation component reporting precision, recall, F1, ROC-AUC, PR-AUC. |
| O3 / FR6 | Explain which features influence model outputs. | Feature explanation component (importance / SHAP-style if compatible); explanations stated as non-causal. |
| O3 / RAI1 | Check for possible disparities across relevant groups where data permits. | Fairness audit stage reporting group sample sizes and metric differences, noting when data is insufficient. |
| RAI2 / RAI5 | Prevent the prototype from being mistaken for an automated promotion decision. | Visible disclaimer in interface and report; outputs require human review; states the dataset only labels historical outcomes. |

---

## Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| Use the public labelled dataset as the starting data source | O1 / FR1 — project scope is limited to the available historical binary label | Collect private company HR records; use a public dataset; create synthetic data only | Use the public 54,808-record HR Analytics dataset for the initial experiment | Accessible for reproducible coursework, but its labels and features may not reflect current organisational practices or role-specific suitability. |
| Compare a simple baseline with a small set of classifiers | O2 / FR3 — evaluation should show whether more complex models add value | Use one model only; compare many models; compare a baseline with a manageable number of models | Start with a simple baseline and compare a small set (e.g. Logistic Regression, Random Forest); add another model only if time/compute permit | Easier to reproduce, but may not cover every potentially useful algorithm. |
| Keep prediction and ranking exploratory | O2 / FR4 — dataset has a historical binary label, not destination role or validated readiness labels | Present ranking as definitive readiness; sort predicted probabilities with clear limitations; omit ranking entirely | Show sorted predicted probabilities for exploratory review, explicitly stating what the score represents | Easy to inspect but cannot establish who deserves promotion or who is suitable for a specific job level. |
| Use model-appropriate explanations | O3 / FR6 — users need an understandable account of model behaviour | Show predictions without explanations; use one explanation technique regardless of model; use suitable feature importance or SHAP-style explanations | Use a method compatible with the final model and report its limitations | Improves inspectability but may still be misunderstood as causal reasons or definitive judgments about an employee. |
| Evaluate class-sensitive performance, not accuracy alone | O3 / FR5 — promoted cases may be a minority class | Report accuracy only; report precision/recall/F1 and threshold-independent metrics; optimise one metric without context | Report precision, recall, F1, ROC-AUC, PR-AUC, confusion matrix, and class distribution | More metrics require careful interpretation; the preferred trade-off depends on intended analytical use. |
| Separate model evaluation from displayed exploratory results | O2 / NFR2 — performance must be measured on unseen data | Evaluate on training data; repeatedly tune against test data; use a held-out test set | Use a documented split and reserve the held-out test set for final evaluation | Available training data is reduced, but evaluation is more credible and leakage risk is lower. |
| Keep V1 technology-neutral and simple | Topic 2 asks for a conceptual architecture before committing to specific technologies | Commit now to a full production stack; use functional component names and refine technology later | Describe data processing, model training, evaluation, explanations, audit, and interface by function | Less implementation detail now, but avoids unnecessary complexity before requirements are tested. |
| Do not automate promotion decisions | RAI2 / RAI5 — historical labels are not a sufficient basis for consequential employment decisions | Automatically approve/reject candidates; display a ranking without caveats; provide analytical results with a clear human-review boundary | Keep the system as a research prototype for analysis and human review only | Cannot provide an automated decision workflow, but reduces the risk of over-relying on an unvalidated model. |

---

## Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|---|
| O1 | FR1 | Dataset structure and data-quality report | Data source; data inspection & preprocessing | [To be collected: dataset shape, feature types, missing values, duplicates, target distribution report] |
| O1 / O2 | FR2 / NFR2 | Reproducible preprocessing and split | Preprocessing pipeline; split configuration | [To be collected: re-run pipeline with fixed configuration and compare outputs] |
| O2 | FR3 | Fair model comparison | Model training and comparison | [To be collected: model comparison table using the same held-out test set and metrics] |
| O2 | FR4 | Exploratory probability-based ordering | Prediction and exploratory ranking | [To be collected: inspect sorting logic; label scores and limitations in the results view] |
| O3 | FR5 | Held-out classification performance | Offline evaluation | [To be collected: precision, recall, F1, ROC-AUC, PR-AUC, confusion matrix on held-out data] |
| O3 | FR6 | Explanation coverage and interpretability | Model explanation | [To be collected: example global/local explanations; wording review for non-causal interpretation] |
| O3 | RAI1 | Group-level disparity checks where feasible | Responsible AI review | [To be collected: group metrics, sample sizes, uncertainty, limitations] |
| O2 / O3 | RAI2 / RAI5 | Intended-use and target limitations visible | Scope control; results interface and report | [To be collected: inspect relevant screens/report sections for the required disclaimer] |
| O2 | NFR3 | Practical experiment runtime | Training/evaluation pipeline | [To be collected: end-to-end runtime and environment used] |

---

### Reflection

**Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?**

"Do not automate promotion decisions" was the most important trade-off. It was driven directly by RAI2 and RAI5 — the risk that a historical-promotion model's output gets treated as a validated promotion recommendation. The trade-off accepted is a real limitation on the system's usefulness: it cannot provide the automated decision-support workflow that would make it most convenient for HR to adopt quickly. That limitation was accepted deliberately, because the related work (Cecil et al., 2024) specifically found that explanations alone do not reliably stop people from over-trusting incorrect AI advice — so a disclaimer plus explanation was judged insufficient on its own, and the architecture needed to enforce human review structurally rather than just recommend it.
