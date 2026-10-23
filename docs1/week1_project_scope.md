# Week 1 Project Scope — Leadership Competency Evidence Ranking Assistant

> **Status:** Preliminary scope. This is an engineering prototype proposal, not a claim that the system is a validated leadership assessment tool.

## Project Name
Leadership Competency Evidence Ranking Assistant (working name; not a final title).

## Domain
Human resources development, leadership competency frameworks, information retrieval, explainable AI.

## Problem Statement
Public leadership frameworks describe competencies and behaviours relevant to leadership roles. However, a user may need to consult multiple frameworks and manually locate the descriptions that relate to a particular behavioural example. This project will investigate whether an AI-assisted retrieval and ranking prototype can help users find relevant competency passages more efficiently while keeping the evidence and source visible. The tool will support competency exploration and development reflection only; it will not determine a person's leadership potential or make employment decisions.

## Evidence of the Problem
**Evidence 1:** Public frameworks contain structured descriptions of leadership competencies and expected behaviours, for example the University of Minnesota Leadership Competency Framework and the Government of Canada's Key Leadership Competency Profile.  
**Source:** https://hr.umn.edu/Professional-Development/Supervisory-and-Leadership-Development/Leadership-Competencies-and-Assessments/Leadership-Competency-Framework  
**Source:** https://www.canada.ca/en/treasury-board-secretariat/services/professional-development/key-leadership-competency-profile.html

**Evidence 2:** Published research studies leadership-potential assessment and succession planning, indicating that leadership assessment is an established topic rather than an unexplored problem.  
**Source:** Groves (2025), “Assessing Leadership Potential for Succession Planning in the Digital Era of Work and Organizations,” Academy of Management Proceedings. Verify the final bibliographic record through the university library before submission.

**Evidence limitation:** These sources show that competency frameworks and leadership assessment exist. They do not prove that every organisation experiences the same difficulty, nor do they establish that this proposed system will improve decisions. User testing and a focused review are still needed.

## Initial Related Work (at least 3)

### 1. Machine-learning ranking systems
**Study:** Bitkuri et al. (2025), “A Review of Machine Learning Ranking Systems: Methods, Applications, and Challenges.”  
**Source:** https://www.cmjpublishers.com/wp-content/uploads/2025/10/a-review-of-machine-learning-ranking-systems-methods-applications-and-challenges.pdf  
**Key limitation for this project:** The review covers ranking methods and broad challenges, but it is not a validation study for leadership competency matching.

### 2. Leadership-potential assessment
**Study:** Groves (2025), “Assessing Leadership Potential for Succession Planning in the Digital Era of Work and Organizations.”  
**Source:** Search and verify the official Academy of Management Proceedings record through the university library before final submission.  
**Key limitation for this project:** The work establishes relevant assessment research, but does not establish the accuracy, fairness, or validity of this proposed text-retrieval prototype.

### 3. Explainable person–job recommendation
**Study:** “Explainable person–job recommendations: challenges, approaches, and comparative analysis” (2025 review).  
**Source:** Verify the exact publisher record and DOI before final submission.  
**Key limitation for this project:** Person–job recommendation is related to explainable matching, but is not identical to matching fictional behavioural evidence to public leadership competency descriptions.

## Engineering Gap / Limitation
Ranking algorithms, leadership assessment approaches, and explainability methods are already studied. The engineering question for this project is whether a small, source-grounded prototype can rank relevant competency passages from multiple public frameworks, provide traceable evidence, and remain consistent enough for competency exploration. The gap is **to be investigated**, not a claim that no similar system exists.

## Initial Project Objectives
- **O1:** To design an AI-assisted system that retrieves and ranks leadership competency passages from selected public frameworks using fictional behavioural evidence.
- **O2:** To implement and compare a lexical retrieval baseline with a semantic-similarity approach, where feasible.
- **O3:** To evaluate ranking relevance, source traceability, response time, wording consistency, and scope-control behaviour.

## Target Users
- Learning and development practitioners exploring leadership competencies.
- HR practitioners preparing non-decisional leadership development resources.
- Individuals who want to explore public leadership competency frameworks.

## Data Sources (at least 2)
1. University of Minnesota Leadership Competency Framework — https://hr.umn.edu/Professional-Development/Supervisory-and-Leadership-Development/Leadership-Competencies-and-Assessments/Leadership-Competency-Framework
2. Government of Canada Key Leadership Competency Profile — https://www.canada.ca/en/treasury-board-secretariat/services/professional-development/key-leadership-competency-profile.html
3. U.S. Office of Personnel Management Executive Core Qualifications — https://www.opm.gov/policy-data-oversight/senior-executive-service/executive-core-qualifications/

**Data limitation:** These documents are public frameworks, not employee-level datasets with validated promotion or leadership-success labels. They can support document retrieval and relevance evaluation, but not supervised prediction of actual leadership success.

## Similar to EduAdvisor
- Uses a defined set of public documents as its knowledge base.
- Needs retrieval, source tracking, evaluation, and clear scope controls.
- Must show evidence so users can verify outputs.

## Different from EduAdvisor
- Focuses on ranking competency passages relevant to fictional behavioural evidence, rather than answering academic-advising questions.
- Evaluation focuses on ranking relevance, traceability, response time, and wording consistency.
- It will not recommend an employment or promotion decision.

## Responsible AI Risks
1. **Misinterpretation / overreliance:** A user may mistake a text similarity rank for a validated measure of leadership potential. Mitigation: label scores as relevance scores, show source text, and state limitations.
2. **Bias and inconsistent ranking:** Wording, cultural context, or framework choice may affect which competencies are retrieved. Mitigation: use multiple public frameworks carefully, test equivalent paraphrases, and report differences.
3. **Privacy:** Real employee examples may include sensitive information. Mitigation: use fictional non-identifying profiles only.
4. **Unfair employment use:** Outputs could be misused to rank employees or justify promotion decisions. Mitigation: exclude real-person comparisons and employment recommendations from the system scope.
