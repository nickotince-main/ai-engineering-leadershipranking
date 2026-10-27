# Week 2 Requirements Specification — TalentRank (Explainable Machine Learning for Employee Promotion Prediction and Ranking)

**Version:** 1.0 — V1 proposal. Thresholds are provisional engineering targets, to be reviewed after a baseline run.

---

## Section 0 — Project Framing & Application Scope Checkpoint

| | |
|---|---|
| **Problem Evidence** | The public HR Analytics employee promotion dataset contains 54,808 employee records and a binary label indicating whether an employee was promoted (Kaggle, *HR Analytics: Employee Promotion Data* — https://www.kaggle.com/datasets/muhammadimran112233/employees-evaluation-for-promotion). Research has applied machine learning to employee promotion prediction using the same general dataset (*Analysis and Prediction of Employee Promotions Using Machine Learning*, 2022, IEEE Xplore — https://ieeexplore.ieee.org/document/9943959/). These sources support studying historical promotion outcomes; they do not establish that the data measures leadership potential or identifies employees suitable for a specific role such as Department Manager, Director, or CEO. |
| **Existing Approaches** | 1) Historical HR review — manual comparison, difficult at scale across many records/features. 2) Machine learning promotion prediction — classification models can estimate likelihood of the historical promotion label, but quality depends on dataset, target definition, and evaluation design. 3) Machine learning ranking methods — can order candidates, but the appropriate method/metric depends on available relevance labels; a probability-based order is not automatically a validated ranking of promotion suitability. 4) Explainable AI methods (e.g. SHAP) — help describe which features influence predictions, but do not prove a feature causes promotion. |
| **Project / Engineering Gap** | The project will compare suitable machine learning models for predicting historical promotion outcomes, investigate ranking employees by model-predicted probability, and explain which recorded features influence the predictions. The engineering question is whether the models provide useful and reliable predictions and explanations on held-out data, while communicating the limitations of the historical promotion label. The project does not claim the dataset validates leadership potential or role-specific promotion suitability. |
| **Objective O1** | To investigate employee features associated with historical promotion outcomes in a public HR dataset. |
| **Objective O2** | To develop and compare machine learning models for employee promotion prediction and ranking. |
| **Objective O3** | To evaluate model performance and explain the features that influence the predictions. |
| **Intended Users** | Primary: HR Talent Management Specialists who review promotion patterns and prepare talent-management analysis. Secondary: Department Heads, Directors, General Managers, and senior management who review HR analysis. Intended use: provide additional information for analysis and human review. Important boundary: model outputs must not be used as the sole basis for an employee promotion decision. |
| **Supported Tasks** | Load and inspect the selected public employee promotion dataset; check data quality, missing values, duplicates, target distribution, and potential data leakage; prepare features and a reproducible train/validation/test split; train and compare selected classification models against a simple baseline; report predicted promotion probabilities and, for exploratory analysis, order records by those probabilities; explain model predictions using an appropriate feature-explanation method; evaluate predictive performance, ranking quality where defensible reference labels are available, and explanation behaviour; display limitations so users do not mistake predictions for proof of employee ability. |
| **Information / Knowledge Domain** | Public employee HR analytics data, historical promotion outcomes, machine learning classification and ranking, and model explanation. The dataset does not contain a validated label for leadership potential or a clear promotion destination for every employee. |
| **Operating Context** | A small academic prototype for training and evaluation using a public dataset. Not a production HR system and not validated for actual employment decisions. |
| **Important Constraints** | Verify dataset documentation, column definitions, access conditions, and data quality before modelling; avoid target leakage and keep the test set separate from model/threshold selection; address class imbalance and report suitable metrics beyond accuracy; treat model explanations as descriptions of model behaviour, not causal evidence; evaluate ranking with suitable relevance labels or reference rankings where possible, and report the limitation if none exists; do not claim the dataset predicts leadership potential or identifies the best candidate for a management level; use only the public dataset — no confidential employee records. |
| **Explicit Out-of-Scope Tasks** | Automatically deciding who should be promoted; claiming to identify the best future Department Manager, Director, or CEO; treating historical promotion as a ground-truth measure of leadership potential; claiming feature importance proves why an employee was promoted; processing confidential company employee records; deploying the prototype for real promotion decisions without further validation, governance, and human oversight. |
| **Evaluation Focus** | Predictive performance on held-out data, performance on the minority promoted class, calibration/probability quality where appropriate, and explanation quality. Ranking metrics used only if a defensible relevance target can be defined. Fairness checks considered where the dataset contains suitable group attributes and enough examples for meaningful analysis. |

---

## Section 1 — Functional Requirements (FR)

| ID | Requirement |
|---|---|
| FR1 | The system shall load the selected public employee promotion dataset and report its dimensions, target distribution, missing values, and duplicate records. It shall not silently assume the dataset is clean or that every column has a verified meaning. |
| FR2 | The system shall prepare features using a documented preprocessing pipeline, including handling missing values and categorical variables as required. It shall not use information from the held-out test set to fit preprocessing or model parameters. |
| FR3 | The system shall train and compare at least two suitable machine learning models and a simple baseline for the historical promotion target. It shall not claim a model is best based only on training results or accuracy. |
| FR4 | The system shall produce a predicted promotion probability for each test record and allow records to be ordered by this probability for exploratory ranking. It shall not present this ordering as a validated ranking of leadership potential or role-specific promotion suitability. |
| FR5 | The system shall report model evaluation metrics on a held-out test set, including precision, recall, F1-score, ROC-AUC, and a precision-recall metric where suitable. It shall not hide the effect of class imbalance or report only accuracy. |
| FR6 | The system shall provide a feature-level explanation of model predictions using a documented method such as SHAP, if compatible with the selected model. It shall not describe feature contributions as proof of causation. |
| FR7 | The system shall display a clear explanation that results reflect patterns in historical promotion data and require human review. It shall not recommend or automatically approve/reject an employee for promotion. |

## Section 2 — Non-Functional Requirements (NFR)

| ID | Quality Dimension | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Predictive performance | The selected model shall outperform or provide a justified trade-off against a simple baseline on held-out data. | Compare the same test split and report precision, recall, F1-score, ROC-AUC, and PR-AUC where suitable. | Test-set F1 and PR-AUC compared with baseline | Provisional: improve PR-AUC over baseline; report actual values and uncertainty; do not claim success if no improvement is observed. |
| NFR2 | Reproducibility | The training and evaluation process shall be repeatable using documented preprocessing, data splits, model settings, and random seeds where applicable. | Run the documented pipeline again and compare test predictions and metrics under the same environment. | Difference in reported metrics under the same configuration | Provisional: identical results for deterministic steps; document any expected variation. |
| NFR3 | Processing performance | The prototype shall train and evaluate the selected models within a practical time on the documented development environment. | Record end-to-end training and evaluation time for the selected dataset and environment. | Total runtime | Provisional: complete a full experiment within 10 minutes on the documented environment; revise after a baseline run if necessary. |
| NFR4 | Ranking evaluation validity | Any ranking claim shall use an appropriate ranking metric only when a defensible relevance label or reference ranking is available. | Document the ranking target and calculate a suitable metric, such as NDCG@k, if the target supports it; otherwise report ranking as exploratory. | Availability of a defensible ranking target; NDCG@k if applicable | 100% of ranking claims state the target and limitation; no validated ranking claim without suitable reference labels. |

## Section 3 — Responsible AI Requirements (RAI)

| ID | Linked Risk (Topic 1) | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Historical bias and unfair ranking | The project shall inspect model performance across relevant groups where suitable attributes and adequate sample sizes are available, and shall document limitations. | Compare relevant group-level error or selection-rate measures; inspect sample sizes and uncertainty. | Group-level metric differences and documented limitations | Report all planned group checks; do not claim fairness is established solely from a small or incomplete analysis. |
| RAI2 | Overreliance on AI predictions | The interface and report shall state that predictions support analysis only and must not be the sole basis for a promotion decision. | Inspect all result views and report sections for the disclaimer and human-review boundary. | Presence of the required limitation statement | 100% of relevant result views and report sections include the limitation. |
| RAI3 | Misinterpreting feature importance | The system shall describe explanations as factors influencing the model's output, not as causal reasons for promotion. | Review generated explanation text and sample outputs against a checklist. | Proportion of reviewed explanations that avoid causal claims | 100% of reviewed explanations use non-causal wording. |
| RAI4 | Data privacy and misuse | The prototype shall use only the selected public dataset and shall not request or store confidential employee records. | Inspect data inputs, project files, and interface prompts for private-data collection paths. | Number of private-data collection paths in the prototype | 0 intentional private employee-data collection paths. |
| RAI5 | Data and target limitations (misleading claims about leadership potential) | The system shall state that the dataset's label represents historical promotion and does not validate leadership potential or promotion readiness for a particular role. | Inspect documentation and result views for the target definition and limitation. | Presence of the target limitation statement | 100% of relevant documentation and result views state the limitation. |

---

### Reflection

**Which Responsible AI requirement in your project will be the most difficult to measure or enforce technically? Why?**

RAI1 (checking for historical bias across employee groups) is likely the hardest to enforce technically. Unlike RAI2–RAI5, which can be checked with a clear pass/fail audit (does a disclaimer appear? does the explanation avoid causal wording?), fairness analysis depends on having suitable group attributes and adequate sample sizes in the dataset — and even then, the *absence* of a detected disparity does not prove fairness, only that none was found within the limits of the test. This makes RAI1 a continuous, judgement-dependent check rather than a simple binary requirement, and its result must always be reported alongside its own limitations rather than as a clean pass/fail.
