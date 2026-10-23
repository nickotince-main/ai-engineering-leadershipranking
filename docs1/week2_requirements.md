# Week 2 Requirements — Leadership Competency Evidence Ranking Assistant

**Status:** V1 proposal. Requirements and thresholds are provisional until a test set and baseline results are available.

## Section 0 — Project Framing and Application Scope

### 0.1 Problem evidence
Public leadership competency frameworks provide structured descriptions of competencies and behaviours. Related research exists on leadership-potential assessment, ranking systems, and explainable matching. The project will investigate whether a small retrieval-and-ranking application can make relevant public competency passages easier to locate and verify.

The evidence does **not** establish that all organisations have the same problem or that the proposed tool is a valid measure of leadership potential. That limitation must remain explicit.

### 0.2 Existing approaches
1. **Manual consultation of leadership frameworks:** authoritative source material, but users must locate and compare relevant passages themselves.
2. **Leadership assessment instruments and structured assessment processes:** can provide context and validated procedures, but this prototype does not reproduce or replace them.
3. **General text search / lexical retrieval:** simple and interpretable baseline, but may miss relevant passages when query wording differs from framework wording.
4. **Semantic similarity / embedding-based retrieval:** may match related wording, but can return plausible yet irrelevant passages and requires evaluation.
5. **Learning-to-rank methods:** possible later option, but require suitable relevance labels and sufficient data; not assumed feasible for V1.

### 0.3 Engineering gap to investigate
Can a small, source-grounded prototype rank relevant competency passages from selected public frameworks, show traceable supporting evidence, and provide sufficiently relevant and consistent results for non-decisional competency exploration? This is an engineering question to test, not a claim that no similar product or study exists.

### 0.4 Objectives
- **O1:** Design an AI-assisted system that retrieves and ranks leadership competency passages from selected public frameworks using fictional behavioural evidence.
- **O2:** Implement and compare a lexical retrieval baseline with a semantic-similarity approach, where feasible.
- **O3:** Evaluate ranking relevance, source traceability, response time, wording consistency, and scope-control behaviour.

### 0.5 Target users
- Learning and development practitioners.
- HR practitioners using public frameworks for development discussions.
- Individuals exploring leadership competencies for personal development.

### 0.6 Supported tasks
- Select a role/category or competency area from the supported scope.
- Enter fictional, non-identifying behavioural evidence.
- Retrieve and rank related competency passages from the selected documents.
- View the matching source excerpt and a source link.
- Review potential development areas as reflection prompts.

### 0.7 Domain and operating context
The prototype operates over a small, curated collection of public leadership competency documents. It is intended for demonstration and evaluation in a student project environment, not production HR use.

### 0.8 Constraints
- One-semester student project.
- Public documents only, subject to source terms and copyright.
- No employee-level promotion labels or validated leadership outcome data are assumed to exist.
- Fictional, non-identifying input only.
- Limited number of documents and manually curated evaluation queries.
- The three frameworks originate from different institutional contexts and should not be assumed equivalent.

### 0.9 Out of scope
- Predicting actual leadership success, promotion, or job performance.
- Ranking real employees or candidates.
- Recommending who to hire, promote, dismiss, reward, or include in a succession plan.
- Replacing validated assessment instruments or qualified human judgement.
- Processing confidential HR records or sensitive personal data.
- Training a supervised model on invented labels and presenting it as validated.

### 0.10 Evaluation focus
Primary focus: ranking relevance and source traceability. Secondary focus: end-to-end response time, consistency under equivalent paraphrases, and adherence to the non-decision-making boundary.

---

## Section 1 — Functional Requirements

| ID | Requirement | Acceptance condition / verification |
|---|---|---|
| FR1 | The system shall allow a user to select a supported role/category or competency area. | Test each supported option and verify the selected scope is applied. |
| FR2 | The system shall accept fictional, non-identifying behavioural evidence as input. | Valid fictional input is accepted; empty or clearly out-of-scope input is handled with a helpful message. |
| FR3 | The system shall retrieve and rank competency passages from the curated public document collection. | For each evaluation query, the system returns a ranked list up to the configured result limit. |
| FR4 | Each displayed match shall include a source document reference and link; where feasible, it shall include the supporting passage. | Audit displayed matches and verify the source points to the document from which the passage was extracted. |
| FR5 | The system shall present results as competency-exploration or development prompts, not as a judgement of a person's potential. | Output wording describes text relevance and avoids validated-sounding personal scores or employment recommendations. |
| FR6 | The system shall respond safely to requests to rank real employees or decide promotion/rejection. | In test cases, the system declines the employment-decision task and restates the tool's intended scope. |
| FR7 | The system shall indicate when no sufficiently relevant match is found, rather than always forcing a confident result. | Low-relevance test queries produce an explicit low-confidence/no-good-match message according to a threshold set after baseline evaluation. |

## Section 2 — Non-Functional Requirements

Thresholds below are proposed engineering targets, not established standards. Confirm or revise them after a baseline run.

| ID | Requirement | Measurement method | Metric | Provisional threshold |
|---|---|---|---|---|
| NFR1 | Ranking results should place relevant competency passages near the top. | Curate queries and relevance labels; calculate nDCG@5. | Mean nDCG@5 | ≥ 0.70, subject to feasibility and baseline review |
| NFR2 | The prototype should respond promptly for interactive use. | Record end-to-end latency over repeated test queries on the documented environment. | 95th percentile latency | ≤ 5 seconds for the chosen small document set |
| NFR3 | Results should be traceable to public sources. | Audit all returned matches in the evaluation run. | Percentage of displayed matches with a valid source reference | 100% |
| NFR4 | The document collection should be maintainable. | Time a documented process for adding a reviewed public document and rebuilding the index. | Time to incorporate one document, excluding time spent locating/reviewing it | ≤ 15 minutes, if supported by the chosen implementation |
| NFR5 | The prototype should fail clearly when input or retrieval is unsuitable. | Test empty input, unsupported request, and low-relevance queries. | Percentage of test cases with an appropriate fallback message | 100% of defined test cases |

## Section 3 — Responsible AI Requirements

| ID | Risk / requirement | Measurement method | Metric | Provisional threshold / control |
|---|---|---|---|---|
| RAI1 | The prototype must not require or store real employee profiles. | Inspect test data, input examples, and repository files. | Number of real employee records in project test data | 0 |
| RAI2 | The prototype must not make employment decisions. | Test requests to rank named employees, choose a promotion candidate, or recommend dismissal. | Percentage of decision-request tests that remain within scope | 100% of defined tests |
| RAI3 | The system must make the basis of a match visible. | Audit result cards/records for a source link and supporting passage. | Percentage of displayed matches with source evidence | 100% |
| RAI4 | The project must examine sensitivity to wording. | Compare rankings for pairs of fictional inputs that express equivalent evidence with different wording. | Rank overlap / rank changes, reported for every test pair | Establish baseline first; document failures and revise approach. No fairness guarantee is inferred from synthetic tests. |
| RAI5 | The interface must explain score meaning and limitations. | Inspect interface and test output text. | Presence of a clear limitation statement in result views | 100% of result views state that relevance is not a validated leadership score |

### Responsible AI operating rule
The system is for competency exploration and development support only. It must not be used to assess, compare, select, promote, or reject real people. Synthetic consistency tests can reveal some weaknesses but cannot establish fairness for a real workforce.
