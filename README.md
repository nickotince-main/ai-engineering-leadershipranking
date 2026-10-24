# Leadership Competency Evidence Ranking Assistant

**Course:** AI Engineering — Topic 1 and Topic 2
**Project status:** Preliminary V1 concept; scope and thresholds are proposed and must be validated.
**Working project name:** Leadership Competency Evidence Ranking Assistant

## 1. Project Overview

This project explores an AI-assisted tool that helps a user connect **fictional profile evidence** with leadership competencies described in public leadership frameworks. The system retrieves and ranks relevant competency descriptions, displays the supporting text and source links, and highlights competencies that may be useful for further development.

The prototype is a **competency exploration and development-support tool**. It is not a validated measure of leadership potential and must not decide who should be hired, promoted, dismissed, or placed in a succession plan.

## 2. Problem and Proposed Approach

Public leadership frameworks describe competencies and expected behaviours, but their descriptions come from different organisations and contexts. A prototype can test whether information retrieval and text-similarity ranking can make relevant competency descriptions easier to find and verify.

The initial approach is to:
1. Use public leadership competency documents as the knowledge base.
2. Accept fictional behavioural evidence and a selected role/category.
3. Retrieve and rank potentially relevant competency passages.
4. Show source-grounded explanations and references.
5. Evaluate relevance, traceability, response time, and consistency.

A lexical retrieval baseline (such as BM25) may be compared with a semantic-similarity approach. A supervised learning-to-rank method will only be considered if a suitable labelled relevance dataset becomes available.

## 3. Scope Boundaries

### In scope
- Explore competency descriptions in public documents.
- Accept fictional, non-identifying behavioural examples.
- Rank relevant competency passages for exploration.
- Show the matched text, source document, and URL.
- Show potential development areas as prompts for reflection.
- Evaluate with a manually curated test set.

### Out of scope
- Predicting actual employee promotion or leadership success.
- Ranking real employees or candidates against one another.
- Hiring, promotion, dismissal, compensation, or succession decisions.
- Processing confidential employee records or sensitive personal data.
- Claiming that similarity scores are validated leadership scores.
- Replacing trained HR professionals or structured assessment processes.

## 4. Public Data Sources

These sources provide competency frameworks, not employee-level outcome labels. Their contents may be used according to each site's terms and applicable copyright rules; the project stores source metadata and short excerpts needed for evaluation rather than republishing whole documents.

1. **University of Minnesota — Leadership Competency Framework**
   https://hr.umn.edu/Professional-Development/Supervisory-and-Leadership-Development/Leadership-Competencies-and-Assessments/Leadership-Competency-Framework
2. **Government of Canada — Key Leadership Competency Profile**
   https://www.canada.ca/en/treasury-board-secretariat/services/professional-development/key-leadership-competency-profile.html
3. **U.S. Office of Personnel Management — Executive Core Qualifications**
   https://www.opm.gov/policy-data-oversight/senior-executive-service/executive-core-qualifications/

The frameworks were developed for different institutional contexts. Competency labels should not be treated as directly interchangeable without documenting the mapping.

## 5. Initial Related Work

- **Bitkuri et al. (2025), "A Review of Machine Learning Ranking Systems: Methods, Applications, and Challenges."**
  https://www.cmjpublishers.com/wp-content/uploads/2025/10/a-review-of-machine-learning-ranking-systems-methods-applications-and-challenges.pdf
  Relevance: summarises pointwise, pairwise, and listwise ranking approaches and general challenges. Limitation: a general ranking review, not validation of a leadership competency assessment system.
- **Groves (2025), "Assessing Leadership Potential for Succession Planning in the Digital Era of Work and Organizations," Academy of Management Proceedings.**
  Official record to be verified through the university library before submission.
  Relevance: shows leadership-potential assessment is already an active research area. Limitation: does not by itself establish the validity of this proposed retrieval-and-ranking design.
- **"Explainable person–job recommendations: challenges, approaches, and comparative analysis" (2025 review).**
  Exact publication record and DOI to be verified through the university library before final submission.
  Relevance: explainability in matching/recommendation is related. Limitation: person–job recommendation is not the same task as leadership competency evidence exploration.

These sources establish relevant areas of prior work; they do not prove that no comparable system exists. The engineering gap should be refined after a focused literature search and hands-on baseline tests.

## 6. Engineering Gap

Can a small, source-grounded prototype rank relevant competency passages from selected public frameworks, show traceable supporting evidence, and provide sufficiently relevant and consistent results for non-decisional competency exploration? This is an engineering question to test, not a claim that no similar product or study exists.

## 7. Initial Project Objectives

- **O1:** Design an AI-assisted system that retrieves and ranks leadership competency passages from selected public frameworks using fictional behavioural evidence.
- **O2:** Implement and compare a lexical retrieval baseline with a semantic-similarity approach, where feasible.
- **O3:** Evaluate ranking relevance, source traceability, response time, wording consistency, and scope-control behaviour.

## 8. Target Users

- Learning and development practitioners exploring leadership competencies.
- HR practitioners preparing non-decisional leadership development resources.
- Individuals who want to explore public leadership competency frameworks.

## 9. Repository Structure

```text
.
├── README.md
└── docs/
    ├── week1_observation_sheet.md
    ├── week1_project_scope.md
    ├── week2_requirements.md
    ├── week2_evaluation_criteria.md
    ├── week2_architecture_v1.png
    └── week2_architecture_decisions.md
```

## 10. Evaluation Plan (Initial)

| Evaluation area | Initial method | Proposed target |
|---|---|---|
| Ranking relevance | Manually label relevance for a curated query set; calculate nDCG@5 | nDCG@5 ≥ 0.70 (provisional; confirm after baseline) |
| Source traceability | Audit every returned match for a valid source reference | 100% of displayed matches have a source |
| Response time | Measure end-to-end latency across repeated test queries | p95 ≤ 5 seconds on the stated test environment |
| Wording consistency | Compare ranking for equivalent fictional evidence phrased differently | Report rank changes; set tolerance after baseline |
| Scope control | Test requests for promotion/rejection decisions | 100% of tested decision requests receive a boundary response |

These are engineering targets for a student prototype, not established industry standards or evidence of real-world validity.

## 11. Responsible AI

- Use fictional examples only; do not upload real employee profiles.
- Display source references and explain that scores represent text relevance, not a person's ability or potential.
- Do not generate a ranked list of real people or recommend an employment action.
- Check whether wording changes alter rankings and report the limitations.
- Keep the human user responsible for interpretation and development discussions.

## 12. Weekly Progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| Week 1 | Initial observation and project scope | Observation sheet, scope, README | Draft; direct group observation evidence added |
| Week 2 | Requirements, evaluation, architecture | Requirements, evaluation criteria, architecture PNG and decisions | Draft V1 |
| Week 3 onward | Data preparation and prototype implementation | To be defined in later labs | Not started |

## 13. Important Submission Checks

- Replace any pending observation fields with your group's actual observations and evidence.
- Verify the exact bibliographic details for every paper before submission.
- Download/review at least 2–3 public domain documents, note parsing issues, and keep only material you are allowed to use.
- Commit the files to GitHub and update this README as the project develops.
