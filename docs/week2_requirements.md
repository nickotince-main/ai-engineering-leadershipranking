# Week 2 Requirements Specification — LeadRanking (Leadership Competency Evidence Ranking Assistant)

**Status:** V1 proposal. Requirements and thresholds are provisional until a test set and baseline results are available.

---

## Section 0 — Project Framing & Application Scope Checkpoint

| | |
|---|---|
| **Problem Evidence** | Public leadership competency frameworks provide structured descriptions of competencies and behaviours. Related research exists on leadership-potential assessment, ranking systems, and explainable matching. The project investigates whether a small retrieval-and-ranking application can make relevant public competency passages easier to locate and verify. This evidence does **not** establish that all organisations have the same problem or that the proposed tool is a valid measure of leadership potential — that limitation stays explicit. |
| **Existing Approaches** | 1) Manual consultation of leadership frameworks — authoritative, but users must locate and compare passages themselves. 2) Leadership assessment instruments / structured assessment processes — validated procedures, but this prototype does not reproduce or replace them. 3) General text search / lexical retrieval — simple, interpretable baseline, but may miss passages when query wording differs from framework wording. 4) Semantic similarity / embedding-based retrieval — may match related wording, but can return plausible yet irrelevant passages. 5) Learning-to-rank methods — a possible later option, but require suitable relevance labels and data; not assumed feasible for V1. |
| **Project / Engineering Gap** | Can a small, source-grounded prototype rank relevant competency passages from selected public frameworks, show traceable supporting evidence, and provide sufficiently relevant and consistent results for non-decisional competency exploration? This is an engineering question to test, not a claim that no similar product or study exists. |
| **Objective O1** | Design an AI-assisted system that retrieves and ranks leadership competency passages from selected public frameworks using fictional behavioural evidence. |
| **Objective O2** | Implement and compare a lexical retrieval baseline with a semantic-similarity approach, where feasible. |
| **Objective O3** | Evaluate ranking relevance, source traceability, response time, wording consistency, and scope-control behaviour. |
| **Intended Users** | Learning and development practitioners; HR practitioners using public frameworks for development discussions; individuals exploring leadership competencies for personal development. |
| **Supported Tasks** | Select a role/category or competency area from the supported scope; enter fictional, non-identifying behavioural evidence; retrieve and rank related competency passages from the selected documents; view the matching source excerpt and source link; review potential development areas as reflection prompts. |
| **Information / Knowledge Domain** | A small, curated collection of public leadership competency documents (University of Minnesota, Government of Canada, U.S. OPM frameworks). |
| **Operating Context** | Intended for demonstration and evaluation in a student project environment, not production HR use. |
| **Important Constraints** | One-semester student project; public documents only, subject to source terms and copyright; no employee-level promotion labels or validated leadership outcome data are assumed to exist; fictional, non-identifying input only; limited number of documents and manually curated evaluation queries; the three frameworks originate from different institutional contexts and should not be assumed equivalent. The supplementary IBM HR Attrition dataset (`data/ibm_hr_attrition_reference.csv`) may be used only as a reference when authoring fictional evidence examples — it must never be loaded as ranking input or used to compare/score individual records. |
| **Explicit Out-of-Scope Tasks** | Predicting actual leadership success, promotion, or job performance; ranking real employees or candidates; recommending who to hire, promote, dismiss, reward, or include in a succession plan; replacing validated assessment instruments or qualified human judgement; processing confidential HR records or sensitive personal data; training a supervised model on invented labels and presenting it as validated. |
| **Evaluation Focus** | Primary focus: ranking relevance and source traceability. Secondary focus: end-to-end response time, consistency under equivalent paraphrases, and adherence to the non-decision-making boundary. |

---

## Section 1 — Functional Requirements (FR)

| ID | Requirement |
|---|---|
| FR1 | The system shall allow a user to select a supported role/category or competency area. (Verification: test each supported option and confirm the selected scope is applied.) |
| FR2 | The system shall accept fictional, non-identifying behavioural evidence as input. (Verification: valid fictional input is accepted; empty or out-of-scope input is handled with a helpful message.) |
| FR3 | The system shall retrieve and rank competency passages from the curated public document collection. (Verification: for each evaluation query, the system returns a ranked list up to the configured result limit.) |
| FR4 | Each displayed match shall include a source document reference and link, and where feasible the supporting passage. (Verification: audit displayed matches and confirm the source points to the document the passage was extracted from.) |
| FR5 | The system shall present results as competency-exploration or development prompts, not as a judgement of a person's potential. (Verification: output wording describes text relevance and avoids validated-sounding personal scores or employment recommendations.) |
| FR6 | The system shall respond safely to requests to rank real employees or decide promotion/rejection. (Verification: in test cases, the system declines the employment-decision task and restates the tool's intended scope.) |
| FR7 | The system shall indicate when no sufficiently relevant match is found, rather than always forcing a confident result. (Verification: low-relevance test queries produce an explicit low-confidence/no-good-match message, per a threshold set after baseline evaluation.) |

## Section 2 — Non-Functional Requirements (NFR)

| ID | Quality Dimension | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Relevance / Correctness | Ranking results should place relevant competency passages near the top. | Curate queries and relevance labels; calculate nDCG@5. | Mean nDCG@5 | ≥ 0.70 (provisional, subject to baseline review) |
| NFR2 | Performance | The prototype should respond promptly for interactive use. | Record end-to-end latency over repeated test queries on the documented environment. | 95th percentile latency | ≤ 5 seconds for the chosen small document set |
| NFR3 | Traceability / Transparency | Results should be traceable to public sources. | Audit all returned matches in the evaluation run. | % of displayed matches with a valid source reference | 100% |
| NFR4 | Maintainability | The document collection should be maintainable. | Time a documented process for adding a reviewed public document and rebuilding the index. | Time to incorporate one document (excluding review time) | ≤ 15 minutes, if supported by the chosen implementation |
| NFR5 | Reliability | The prototype should fail clearly when input or retrieval is unsuitable. | Test empty input, unsupported request, and low-relevance queries. | % of test cases with an appropriate fallback message | 100% of defined test cases |

## Section 3 — Responsible AI Requirements (RAI)

| ID | Linked Risk (Topic 1) | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Privacy | The prototype must not require or store real employee profiles. | Inspect test data, input examples, and repository files. | Number of real employee records in project test data | 0 |
| RAI2 | Unfair employment use | The prototype must not make employment decisions. | Test requests to rank named employees, choose a promotion candidate, or recommend dismissal. | % of decision-request tests that remain within scope | 100% of defined tests |
| RAI3 | Misinterpretation / overreliance | The system must make the basis of a match visible. | Audit result cards/records for a source link and supporting passage. | % of displayed matches with source evidence | 100% |
| RAI4 | Bias and inconsistent ranking | The project must examine sensitivity to wording. | Compare rankings for pairs of fictional inputs expressing equivalent evidence with different wording. | Rank overlap / rank changes, reported per test pair | Baseline first; document failures and set tolerance after. No fairness guarantee inferred from synthetic tests. |
| RAI5 | Misinterpretation / overreliance | The interface must explain score meaning and limitations. | Inspect interface and test output text. | % of result views with a clear limitation statement | 100% of result views state that relevance is not a validated leadership score |

---

### Reflection

**Which Responsible AI requirement in your project will be the most difficult to measure or enforce technically? Why?**

RAI4 (wording-sensitivity / consistency) is likely the hardest to enforce technically. Unlike RAI1–RAI3, which can be checked with a clear pass/fail audit (does a record exist? does a source link appear?), RAI4 has no fixed threshold yet — "equivalent evidence" is itself a judgement call, and paraphrase pairs can differ in subtle ways that legitimately should change relevant results versus ways that shouldn't. Establishing a defensible baseline and tolerance will require building the paraphrase test set first and reviewing real failure cases before any numeric target can be trusted, rather than setting a threshold upfront.
