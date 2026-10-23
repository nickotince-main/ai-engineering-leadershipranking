# LeadReady - AI Leadership Ranking & Competency Alignment Assistant

An AI Engineering project that compares employees against defined role requirements and leadership competencies, generating a plain-language explanation of each employee's alignment — rather than an unexplained leaderboard — to support succession planning decisions.

**Author:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)
**Course:** AI Engineering — Semester Project
**Status:** Week 1 — Preliminary scoping

---

## Problem Statement

Succession planning is traditionally manual, inconsistent across departments, and prone to bias: employees who lead informally are often overlooked because they don't match a manager's default picture of "leadership material." Where ranking is attempted, it typically produces a leaderboard with no stated justification. Organizations need a consistent way to compare employees against explicit role requirements, with a clear explanation behind each comparison.

## Evidence of the Problem

- Only 32% of surveyed leaders expressed confidence that they have the right skills to lead transformation in their organizations (Korn Ferry).
- Organizations using continuous, AI-assisted succession tracking report up to 60% faster leadership transitions and more diverse succession pipelines than traditional annual review cycles (4Spot Consulting).

## Initial Related Work / Existing Approaches

| Approach | Limitation |
|---|---|
| Gloat Succession Management Agent | Proprietary, closed scoring logic; not auditable |
| SAP SuccessFactors AI succession framework (Zenodo, 2025) | Validated on simulated data only; real-world generalizability unproven |
| Phenom Succession Planning | Skills-ontology matching can still miss informal/relational leadership signals |

## Engineering Gap / Limitation

Existing AI succession tools are closed, enterprise-platform-bound, and show a rank or score without a competency-by-competency rationale. There is a gap for a small-scale, **explainable** leadership-ranking approach built on open data, where the comparison against role requirements is visible and auditable.

## Initial Project Objectives

1. Define a structured leadership competency/role-requirement reference to rank employees against.
2. Compare each employee's documented competencies to role requirements and generate a plain-language alignment explanation — not just a leaderboard position.
3. Evaluate and document the ranking approach's demographic bias and mitigation steps.

## Target Users

- HR / talent management teams and people managers running succession planning.
- Students and researchers studying applied AI Engineering in HR/talent contexts.

## Proposed Data Sources

1. [IBM HR Analytics Employee Attrition & Performance dataset](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) — Kaggle, public
2. [Reengineering Succession Pipelines in SAP SuccessFactors](https://zenodo.org/records/17500957) — Zenodo, open access

## Weekly Progress

| Week | Progress |
|---|---|
| Week 1 | Completed group AI system analysis (Claude.ai) and conceptual system map; scoped LeadReady project; set up GitHub repository and folder structure |

---

## Repository Structure

```
ai-engineering-leadready/
├── README.md
├── docs/
│   ├── week1_observation_sheet.md
│   ├── week1_system_map.jpeg
│   └── week1_project_scope.md
├── data/
├── src/
├── notebooks/
├── evaluation/
└── prompts/
```

> ⚠️ This is a public repository. No API keys, credentials, confidential data, or restricted university information will be committed.
