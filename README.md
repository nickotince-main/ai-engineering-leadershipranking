# TalentRank — Explainable Machine Learning for Employee Promotion Prediction and Ranking

**Course:** AI Engineering — Topic 1 and Topic 2
**Project status:** V1 proposal; thresholds and model choices are provisional until a baseline experiment is run.

## 1. Project Overview

TalentRank develops and compares machine learning models that predict historical employee promotion outcomes from a public HR dataset, explore ranking employees by predicted promotion probability, and explain which recorded features influence each prediction. The system supports HR Talent Management Specialists and senior management with analysis - it does not make or automate promotion decisions.

## 2. Problem Statement

Companies need to review employee information when making promotion decisions, but comparing many employees consistently and understanding which factors drive a model's prediction is difficult. This project investigates whether ML classification, exploratory ranking, and explanation methods can support (not replace) that human review process.

## 3. Evidence of the Problem

- A public HR Analytics promotion dataset contains 54,808 employee records and a binary promotion outcome, supporting study of historical promotion patterns (Kaggle, *HR Analytics: Employee Promotion Data*).
- Published research has already applied ML to this dataset for promotion prediction, confirming the task is well-posed while leaving room for a clearly defined model-comparison and explanation workflow (*Analysis and Prediction of Employee Promotions Using Machine Learning*, IEEE, 2022).

## 4. Initial Related Work

- **Analysis and Prediction of Employee Promotions Using Machine Learning** (IEEE, 2022) — https://ieeexplore.ieee.org/document/9943959/ — classification comparison on the same dataset; doesn't establish leadership potential or destination role.
- **Bitkuri et al. (2025), A Review of Machine Learning Ranking Systems** — https://www.cmjpublishers.com/wp-content/uploads/2025/10/a-review-of-machine-learning-ranking-systems-methods-applications-and-challenges.pdf — general ranking methods/evaluation reference.
- **Cecil et al. (2024), Explainability does not mitigate the negative impact of incorrect AI advice in a personnel selection task** — *Scientific Reports* — https://www.nature.com/articles/s41598-024-60220-5 — warns explanations alone don't prevent overreliance on incorrect AI advice.
- **Optimizing employee promotion predictions using machine learning** (2025) — https://www.polipapers.upv.es/index.php/IJPME/article/view/23364 — further model comparisons on the same dataset.

## 5. Engineering Gap

The dataset supports prediction of historical promotion outcomes but does not measure leadership potential or state promotion destination. The engineering task is to compare suitable ML models, investigate exploratory probability-based ranking, and generate non-causal feature explanations — evaluated rigorously rather than assumed to work.

## 6. Initial Project Objectives

- **O1:** Investigate employee features associated with historical promotion outcomes.
- **O2:** Develop and compare machine learning models for promotion prediction and ranking.
- **O3:** Evaluate model performance and explain the features that influence predictions.

## 7. Target Users

- **Primary:** HR Talent Management Specialists reviewing promotion patterns.
- **Secondary:** Department Heads, Directors, General Managers, senior management.
- **Important boundary:** model output supports analysis only; it is never the sole basis for a promotion decision.

## 8. Proposed Data Sources

1. [Kaggle — HR Analytics: Employee Promotion Data](https://www.kaggle.com/datasets/muhammadimran112233/employees-evaluation-for-promotion) — 54,808 records, primary training/evaluation dataset.
2. [Bitkuri et al. (2025) — A Review of Machine Learning Ranking Systems](https://www.cmjpublishers.com/wp-content/uploads/2025/10/a-review-of-machine-learning-ranking-systems-methods-applications-and-challenges.pdf) — methods/evaluation reference.
3. [Cecil et al. (2024) — Scientific Reports](https://www.nature.com/articles/s41598-024-60220-5) — RAI/risk reference.

> Download instructions are in `data/DATASET_SOURCE.txt` — the raw CSV is not committed due to its size; download it from Kaggle before running the notebooks.

## 9. Repository Structure

```text
ai-engineering-talentrank/
├── README.md
├── docs/
│   ├── week1_observation_sheet.md
│   ├── week1_project_scope.md
│   └── week1_system_map.jpeg
│   ├── week2_requirements.md
│   ├── week2_evaluation_criteria.md
│   ├── week2_architecture_v1.png
│   └── week2_architecture_decisions.md
├── data/
│   └── DATASET_SOURCE.txt
├── src/
├── notebooks/
├── evaluation/
└── prompts/
```

## 10. Responsible AI

- Use only the public dataset; never add confidential employee records.
- State clearly that predictions are estimates from historical data, not proof of leadership ability or a specific promotion destination.
- Describe feature explanations as model behaviour, not causal evidence.
- Check performance across relevant groups where the data allows, and report limitations honestly — absence of a detected disparity does not prove fairness.
- Require human review for every output; the system never automates a promotion decision.

## 11. Weekly Progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| Week 1 | Initial observation and project scope | Observation sheet, scope, README | Complete |
| Week 2 | Requirements, evaluation, architecture | Requirements, evaluation criteria, architecture PNG and decisions | Draft V1 (pivoted to TalentRank) |
| Week 3 onward | Data preparation and model implementation | To be defined in later labs | Not started |

## 12. Important Submission Checks

- Verify the exact bibliographic details for every paper before final submission.
- Download the Kaggle dataset locally per `data/DATASET_SOURCE.txt`; do not commit the raw CSV if it exceeds repository size limits.
- Confirm class-imbalance handling and held-out test discipline before reporting any results.
- Commit the files to GitHub and update this README as the project develops.
