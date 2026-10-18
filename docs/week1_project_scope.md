# Week 1 Project Scope

**Student:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)
**Status:** Preliminary — to be refined in Topic 2

---

## 1. Project Name and Domain

**Project Name:** LeadReady — AI Leadership Ranking & Competency Alignment Assistant
**Domain:** AI-Powered Talent Management / Human Resources (Succession Planning)

An AI Engineering system that compares employees against clearly defined role requirements and leadership competencies, and — instead of producing an unexplained leaderboard — generates a justification showing how each employee's documented competencies align (or don't) with a target role. The AI opportunity is specifically in the *explanation*, not just the ranking.

## 2. Problem Statement

Succession planning — identifying who is ready to step into leadership roles — is traditionally done through annual, manual review cycles based on manager opinion and informal reputation. This process is slow, inconsistent across departments, and prone to bias: employees who lead through influence rather than formal authority are often overlooked because they don't match a manager's default mental picture of "leadership material." Where organizations do attempt to rank candidates systematically, the result is typically a leaderboard or score with no stated justification — managers see *who* ranks higher, not *why*, which makes the ranking hard to trust, contest, or act on developmentally. Organizations need a way to compare employees against explicit role requirements and leadership competencies, with a clear, inspectable explanation behind each comparison.

## 3. Evidence of the Problem

- Organizations report low confidence in their leadership pipelines: only 32% of leaders surveyed expressed confidence that they have the right skills to drive transformation in their organizations, underscoring the gap between assumed and actual readiness (Korn Ferry, "Why AI-Readiness Is Vital to Your Leadership Succession Plan").
- Industry analysis of AI-driven succession tools reports measurable gains from moving off manual processes — organizations using continuous, AI-assisted succession tracking report up to 60% faster leadership transitions and more diverse succession pipelines compared with traditional annual reviews (4Spot Consulting, "AI in Succession Planning: 9 Ways to Build Your Future Leadership Pipeline").

## 4. Initial Related Work

| # | Existing Study / Solution | Limitation |
|---|---|---|
| 1 | **Gloat Succession Management Agent** — a commercial AI agent that scores candidate readiness across technical skill, leadership competency, organizational knowledge, and stakeholder relationships. | Proprietary and closed; scoring logic is not visible to candidates or auditable by outside researchers, limiting transparency and academic reproducibility. |
| 2 | **"Reengineering Succession Pipelines in SAP SuccessFactors: An AI-Driven Framework for Ethical, Predictive, and Inclusive Leadership Readiness"** (Zenodo, 2025) — tests decision-tree and logistic-regression models for leadership readiness within SAP SuccessFactors. | Validated only on simulated/anonymized organizational data in a single enterprise platform context; real-world generalizability and bias behaviour on authentic data are not established. |
| 3 | **Phenom Succession Planning** — uses skills ontologies and predictive analytics to surface successors, including less-visible "informal leaders." | Skills-ontology matching can still under-represent employees whose leadership signals are behavioural/relational rather than skill-tagged, per HBR research cited in industry analysis. |

## 5. Engineering Gap / Limitation

Existing AI succession tools are largely commercial, closed-source platforms embedded in enterprise HCM suites (SAP SuccessFactors, Gloat, Phenom). Their scoring logic is opaque to the employees being ranked, and even where a readiness score is shown, the *comparison against role requirements* is rarely surfaced in plain terms — employees and managers see a rank or number, not a competency-by-competency rationale. There is a practical gap for a **small-scale, explainable** leadership-ranking approach: one that compares an employee's documented competencies against a defined role's requirements and states, in plain language, where the alignment is strong and where it's lacking — built on open, inspectable data and logic, suitable for a student/engineering context where auditability matters more than enterprise-scale integration.

## 6. Project Objectives (Initial)

1. Define a structured leadership competency/role-requirement reference (drawn from an open dataset and/or public competency framework) to rank employees against.
2. Build a ranking approach that compares each employee's documented competencies to the defined role requirements and generates a plain-language explanation of the alignment — not just a leaderboard position.
3. Evaluate the ranking approach for demographic bias (e.g., across gender, age group) and document mitigation steps, given the fairness risks identified in related work.

## 7. Target Users

- **Primary:** HR / talent management teams and people managers conducting succession planning reviews.
- **Secondary:** Students and researchers studying applied AI Engineering in HR/talent contexts.

## 8. Data Sources

1. **IBM HR Analytics Employee Attrition & Performance dataset** (Kaggle, public, fictional/anonymized HR data including performance ratings, job level, tenure, and satisfaction fields):
   https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
2. **"Reengineering Succession Pipelines in SAP SuccessFactors"** (Zenodo, open-access publication on AI-driven leadership readiness frameworks, used as a methodological reference):
   https://zenodo.org/records/17500957

## 9. Comparison with EduAdvisor

*Note: based on the course's stated framing of EduAdvisor as a conversational FAQ-style assistant; to be confirmed against the full EduAdvisor example.*

**Similar:** Both projects follow the same AI Engineering lifecycle — a defined problem, a bounded data/document source, an AI component that transforms that source into decision-support output for a specific user group, and planned evaluation and monitoring stages.

**Different:** EduAdvisor is a conversational, free-text Q&A assistant that retrieves and answers questions from a document corpus (an information-retrieval problem). LeadReady is a structured, comparison-driven system that matches employee competencies against defined role requirements and outputs a ranked, explained comparison rather than conversational answers. LeadReady also carries materially higher Responsible AI stakes, since its output could influence real promotion and career decisions, compared with EduAdvisor's lower-stakes informational use case.

## 10. Responsible AI Risks

1. **Bias and fairness:** Historical performance and promotion data can encode existing organizational bias (e.g., against informal leaders, specific demographics, or departments). A model trained on this data risks automating and scaling that bias rather than correcting it.
2. **Privacy and confidentiality:** Readiness and performance data is sensitive personal/HR data. Real organizational data must never be committed to a public repository; only public or synthetic datasets will be used for coursework.
3. **Over-reliance / accountability:** Managers may over-trust a numeric readiness score without understanding its basis, leading to decisions made "because the AI said so" rather than with human judgment and accountability.
