# Week 2 Requirements Specification — LeadReady

**Student:** Nik Muhammad Muqri Hazim Bin Nik Nor Ahmarizam (A24AI0071)

---

## Section 0 — Project Framing & Application Scope Checkpoint

| | |
|---|---|
| **Problem Evidence** | 1) Only 32% of surveyed leaders expressed confidence that they have the right skills to lead transformation, showing a confidence gap in leadership pipelines (Korn Ferry, "Why AI-Readiness Is Vital to Your Leadership Succession Plan"). 2) A peer-reviewed review of ML-based ranking systems confirms that interpretability and fairness of model outcomes remain core, unresolved challenges for ranking systems generally, and names hiring specifically as a domain where this matters (Bitkuri et al., 2025, *A Review of Machine Learning Ranking Systems: Methods, Applications, and Challenges*, J Contemp Edu Theo Artific Intel, DOI: 10.47991/2996-4954/JCETAI-119). This supports the claim that leadership ranking tools showing scores without justification is a known, documented gap, not just an assumption. |
| **Existing Approaches** | 1) **Gloat Succession Management Agent** — commercial AI agent scoring candidates across competency, organizational knowledge, and relationships; proprietary, closed scoring logic. 2) **SAP SuccessFactors AI readiness framework** (Bauskar et al., Zenodo 2025) — tests decision-tree/logistic-regression models for leadership readiness; validated only on simulated enterprise data. 3) **Classical Learning-to-Rank methods** (RankNet, LambdaRank, SVMRank, ListNet, as reviewed in Bitkuri et al., 2025) — established pointwise/pairwise/listwise ranking techniques widely used in search, recommendation, and ads; evaluated mainly via accuracy metrics (Precision, Recall, nDCG) rather than explainability to the people being ranked. |
| **Project / Engineering Gap** | Bitkuri et al. (2025) explicitly identifies a lack of interpretability as a core unresolved challenge for ML-based ranking systems "especially in large-scale applications," and separately flags fairness and ethics as critical in domains "like healthcare, hiring, and education." Current leadership-ranking tools (commercial HR platforms and the broader LTR literature) optimize ranking accuracy but not plain-language, competency-level explanation of *why* one employee ranks above another. This is the specific, literature-supported gap LeadReady addresses: explainable comparison against defined role requirements, not just ranking accuracy. |
| **Objective O1** | To design a leadership ranking approach that compares employee competencies against defined role requirements. |
| **Objective O2** | To develop an explanation component that generates a plain-language justification for each employee's ranking, referencing the specific competency data used. |
| **Objective O3** | To evaluate the ranking and explanation approach for usefulness and demographic bias, using a public HR dataset. |
| **Intended Users** | Primary: HR / talent management teams and people managers running succession planning reviews. Secondary: students/researchers studying applied AI Engineering in HR. |
| **Supported Tasks** | Compare an employee's documented competency profile against a defined role's leadership requirements; produce a ranked list of candidates for a role; produce a per-employee, plain-language explanation of competency alignment and gaps. |
| **Information / Knowledge Domain** | Leadership competency frameworks, role requirement definitions, and employee competency/performance records (using the IBM HR Analytics Employee Attrition & Performance dataset as a public proxy for real organizational HR data). |
| **Operating Context** | Used by HR/managers during periodic succession-planning review cycles (offline, batch-style analysis) — not a real-time, employee-facing chat tool. |
| **Important Constraints** | Only public or synthetic HR data (e.g. the IBM dataset) may be used for coursework — no real organizational data. The dataset has no explicit "leadership competency" labels, so a proxy competency mapping must be defined from available fields (job level, performance rating, years in current role, training count, etc.). Student project timeline and compute are limited — V1 is conceptual only. |
| **Explicit Out-of-Scope Tasks** | The system shall not make final promotion, demotion, or termination decisions. It shall not process real, identifiable employee data. It shall not provide legal, compliance, or HR-policy advice. |
| **Evaluation Focus** | Whether the system's ranked, explained output is more interpretable and actionable to HR users than an unexplained leaderboard, and whether its top-ranked outputs avoid systematic demographic bias. |

---

## Section 1 — Functional Requirements (FR)

| ID | Requirement |
|---|---|
| FR1 | The system shall accept an employee's documented competency profile (e.g., performance ratings, job history, training records) as input. |
| FR2 | The system shall accept a defined target role's leadership competency requirements as input. |
| FR3 | The system shall generate a ranked comparison of a set of employees against a target role's requirements. |
| FR4 | The system shall generate a plain-language explanation for each employee's rank position, stating which competencies are aligned and which are lacking, referencing the specific input data used. The system shall not output a ranking without an accompanying explanation. |
| FR5 | The system shall flag any employee ranking made from incomplete competency data. The system shall not present a low-confidence ranking as equivalent in confidence to a complete one. |

## Section 2 — Non-Functional Requirements (NFR)

| ID | Quality Dimension | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Correctness | Explanations must be factually traceable to source data. | Compare each generated explanation's cited competency values against ground-truth values in the source dataset, for a sample of employees. | % of sampled explanations with no factual errors. | ≥ 95% |
| NFR2 | Reliability | Ranking output must be consistent across repeated runs on the same input. | Run the same employee set and role requirements through the system 3 times; compare rank order. | Rank-order agreement across runs (e.g. Kendall's tau). | ≥ 0.9 |
| NFR3 | Performance | Ranking + explanation output must be produced in reasonable time for a batch review. | Time a full run for a batch of 50 employees against one role. | Average response time (seconds). | ≤ 30 seconds per 50-employee batch |
| NFR4 | Maintainability | Adding or updating a role's competency requirements must not require code changes. | Have a non-developer attempt to add a new role requirement set using only configuration. | Number of manual code edits required. | 0 |

## Section 3 — Responsible AI Requirements (RAI)

| ID | Linked Risk (Topic 1) | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Bias and fairness | The system shall report ranking-outcome distribution across available demographic fields (e.g., gender, age group) for every ranking run. | Compute the selection rate of each demographic group among top-ranked employees for a test run. | Disparate impact ratio (protected group selection rate ÷ reference group selection rate). | ≥ 0.8 for each tracked group (the "4/5ths rule") |
| RAI2 | Privacy and confidentiality | The system shall operate only on public or synthetic data during coursework; it shall not ingest or store real, identifiable employee data. | Manual audit of all data files committed to the repository before each submission. | Count of real/identifiable data files detected. | 0 |
| RAI3 | Over-reliance / accountability | The system shall label all output as decision-support only (never a final decision) and include a disclaimer that human review is required. | Review a sample of system outputs for presence of the required disclaimer. | % of outputs containing the disclaimer. | 100% |

---

### Reflection

**Which Responsible AI requirement in your project will be the most difficult to measure or enforce technically? Why?**

RAI1 (bias and fairness monitoring) is likely the hardest to enforce technically. The IBM HR dataset has no true "leadership readiness" ground-truth label, so any fairness check is only as good as the proxy competency definition used to build the ranking in the first place — if that proxy itself correlates with a protected attribute, a disparate-impact check on the *output* can look fine while the underlying *method* is still biased. Measuring fairness well would require either a cleaner ground-truth label or deliberately testing the proxy definition itself for correlation with demographic fields, which is more involved than a single post-hoc ratio check.

*(Personalize this if your group discussion surfaces a different view — e.g. some groups may find NFR1 explanation-correctness harder to automate than RAI1.)*
