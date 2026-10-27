# TalentRank - Explainable Machine Learning for Employee Promotion Prediction and Ranking

## 1. Project Overview

This project investigates the use of machine learning to predict historical employee promotion outcomes using a public HR Analytics dataset. It compares machine learning models, explores ranking employees according to their predicted promotion probabilities, and explains which recorded features influence the predictions.

The system is intended to support HR Talent Management Specialists and management in analysing historical promotion patterns. It is **not designed to make automatic promotion decisions**.

## 2. Problem Statement

Organisations may need to review employee information when analysing promotion patterns. Comparing many employee records can be challenging, and model predictions may be difficult to interpret without suitable explanations.

This project aims to develop and compare machine learning models that predict historical employee promotion outcomes, explore employee ranking based on predicted probabilities, and explain the features that influence the predictions.

## 3. Project Objectives

- **O1:** To investigate employee features associated with historical promotion outcomes in a public HR dataset.
- **O2:** To develop and compare machine learning models for employee promotion prediction and ranking.
- **O3:** To evaluate model performance and explain the features that influence the predictions.

## 4. Target Users

- **Primary users:** HR Talent Management Specialists.
- **Secondary users:** Department Heads, Directors, General Managers, and senior management.

The system provides analytical information for human review. Final promotion decisions must remain with authorised human decision-makers.

## 5. Dataset

The project uses a public HR Analytics employee promotion dataset containing approximately 54,808 employee records.

The dataset includes features such as:

- Department
- Education
- Gender
- Recruitment channel
- Number of trainings
- Age
- Previous-year performance rating
- Length of service
- Awards won
- Average training score
- Historical promotion outcome

**Dataset source:** [HR Analytics: Employee Promotion Data — Kaggle](https://www.kaggle.com/datasets/muhammadimran112233/employees-evaluation-for-promotion)

The dataset will be inspected before modelling to verify its structure, data quality, feature types, missing values, and target distribution.

## 6. Proposed Methodology

1. Inspect and understand the dataset.
2. Clean and preprocess the data.
3. Explore the relationship between recorded employee features and historical promotion outcomes.
4. Establish a baseline model.
5. Train and compare suitable machine learning models.
6. Evaluate models using appropriate classification metrics, including precision, recall, F1-score, ROC-AUC, and PR-AUC where applicable.
7. Explore ranking employees using predicted promotion probabilities.
8. Use an explainability method, such as SHAP where suitable, to examine features influencing model predictions.
9. Assess responsible AI risks, including potential group disparities and the misuse of predictions.
10. Document results, limitations, and future improvements.

## 7. Expected Outputs

- Dataset exploration and preprocessing results.
- Comparison of machine learning models.
- Evaluation metrics and model comparison.
- Exploratory employee ranking based on predicted probabilities.
- Explanations of features influencing predictions.
- Documentation of limitations and responsible AI considerations.

These are planned outputs; results will be reported after experiments have been conducted.

## 8. Responsible AI and Limitations

The dataset records historical promotion outcomes. It does not directly measure leadership potential or identify the appropriate promotion destination for each employee.

Therefore:

- A predicted probability is not proof that an employee is suitable for promotion.
- A ranking is exploratory and must not be treated as a validated ranking of leadership potential.
- Feature explanations describe how a model uses recorded features; they do not prove causation.
- Historical data may contain existing organisational biases.
- Fairness checks will be performed where the available data and sample sizes allow.
- The system must not be used as the sole basis for employment or promotion decisions.

## 9. Project Status

**Current phase:** Requirements specification and conceptual architecture.

The next phase is to inspect the dataset, establish a baseline, and begin model development and evaluation.

## 10. Repository Structure

```text
project-root/
├── README.md
├── docs/
│   ├── week1_project_scope.md
│   ├── week2_requirements.md
│   ├── week2_evaluation_criteria.md
│   ├── week2_architecture_v1.png
│   └── week2_architecture_decisions.md
├── data/
├── notebooks/
└── src/
```

The folders for data, notebooks, and source code may be updated as implementation progresses. Do not commit private or sensitive employee data to the repository.
