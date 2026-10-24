# Leadership Competency Evidence Ranking Assistant

An AI Engineering project that helps users find relevant leadership competency descriptions across multiple public frameworks, using fictional behavioural evidence — ranked, source-grounded, and explicitly non-decisional (it does not assess, rank, or make employment recommendations about real people).

**Author:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)
**Course:** AI Engineering — Semester Project
**Status:** Week 2 — V1 conceptual proposal; scope and thresholds are provisional and must be validated.

---

## Problem Statement

Public leadership frameworks describe competencies and behaviours relevant to leadership roles, but a user may need to consult multiple frameworks and manually locate the descriptions that relate to a particular behavioural example. This project investigates whether an AI-assisted retrieval and ranking prototype can make relevant competency passages easier to find and verify, for competency exploration and development reflection only.

## Evidence of the Problem

- Public frameworks (University of Minnesota, Government of Canada) contain structured competency descriptions, but scattered across separate documents with no unified way to search by behavioural evidence.
- Published research (Groves, 2025, Academy of Management Proceedings) already studies leadership-potential assessment and succession planning, confirming this is an active, established area.

## Initial Related Work / Existing Approaches

| Approach | Limitation |
|---|---|
| Manual consultation of leadership frameworks | Authoritative, but users must locate/compare passages themselves |
| Leadership assessment instruments | Validated procedures, but this prototype does not reproduce or replace them |
| Bitkuri et al. (2025), ML ranking systems review | General ranking review, not validation for leadership competency matching |
| Groves (2025), leadership-potential assessment | Establishes the research area; doesn't validate this specific prototype |
| Explainable person–job recommendations (2025 review) | Related explainability work, but a different task (job matching, not competency exploration) |

## Engineering Gap / Limitation

Can a small, source-grounded prototype rank relevant competency passages from selected public frameworks, show traceable supporting evidence, and remain sufficiently relevant and consistent for non-decisional competency exploration? This is an open engineering question to test — not a claim that no similar system exists.

## Initial Project Objectives

1. Design an AI-assisted system that retrieves and ranks leadership competency passages from selected public frameworks using fictional behavioural evidence.
2. Implement and compare a lexical retrieval baseline (e.g. BM25) with a semantic-similarity approach, where feasible.
3. Evaluate ranking relevance, source traceability, response time, wording consistency, and scope-control behaviour.

## Target Users

- Learning and development practitioners exploring leadership competencies.
- HR practitioners using public frameworks for development discussions (non-decisional).
- Individuals exploring leadership competencies for personal development.

## Proposed Data Sources

1. [University of Minnesota — Leadership Competency Framework](https://hr.umn.edu/Professional-Development/Supervisory-and-Leadership-Development/Leadership-Competencies-and-Assessments/Leadership-Competency-Framework)
2. [Government of Canada — Key Leadership Competency Profile](https://www.canada.ca/en/treasury-board-secretariat/services/professional-development/key-leadership-competency-profile.html)
3. [U.S. OPM — Executive Core Qualifications](https://www.opm.gov/policy-data-oversight/senior-executive-service/executive-core-qualifications/)

## Responsible AI

- Fictional examples only — no real employee profiles accepted or stored.
- Every result shows its source document and link; scores are labelled as text relevance, not validated leadership potential.
- The system will not rank real people or recommend an employment action (hire/promote/dismiss).
- Wording-consistency is explicitly tested (paraphrase pairs) and limitations are reported, not hidden.
- The human user remains responsible for interpretation and any development discussion.

## Weekly Progress

| Week | Progress |
|---|---|
| Week 1 | Completed group AI system analysis (Claude.ai) and conceptual system map; scoped initial project direction |
| Week 2 | Revised project scope per lecturer consultation (pivoted to public-framework, non-decisional design); completed requirements (FR/NFR/RAI), evaluation criteria, and V1 architecture with ADRs and traceability matrix |

---

## Repository Structure

```
ai-engineering-leadready/
├── README.md
├── docs/
│   ├── week1_observation_sheet.md
│   ├── week1_project_scope.md
│   ├── week2_requirements.md
│   ├── week2_evaluation_criteria.md
│   ├── week2_architecture_v1.png
│   └── week2_architecture_decisions.md
├── data/
├── src/
├── notebooks/
├── evaluation/
└── prompts/
```

## Important Submission Checks

- Verify the exact bibliographic details for the Groves (2025) and "Explainable person–job recommendations" sources before final submission.
- Review at least 2–3 public framework documents, note any parsing issues, and keep only material you're permitted to use (check each site's terms).
- No API keys, credentials, confidential data, or restricted university information will be committed. This is a public repository.
