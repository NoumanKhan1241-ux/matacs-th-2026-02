
# Design Write-Up

## 1. AI vs. Rules

I would use AI to extract information from uploaded proposals because contractors may describe the same information in different ways. For example, one proposal might say that it has a project manager, while another might describe a named project lead. AI can identify these details and return them in a consistent JSON structure, including the supporting text and page reference where available.

I would use normal application code for mandatory checks, score calculations, weight validation, and ranking. These steps follow defined rules and should not depend on an AI model's judgment. The system would also treat proposal content as untrusted input, so instructions inside a proposal could never change the evaluation rules.

## 2. Consistency and Explainability

The admin would configure criteria, weights, mandatory requirements, and scoring rules through the application. The system would validate that the weighted criteria total 100% before scoring begins.


For repeatable results, I would use the same scoring formulas and a versioned criteria configuration for every proposal in an evaluation. Experience would be scored as the qualifying installation count divided by 15, multiplied by 100, capped at 100. Price would be scored relative to the budget ceiling and the lowest-priced eligible proposal. Timeline would be scored as (16 minus completion weeks) divided by 16, multiplied by 100. Warranty would average the panel warranty score, capped at 25 years, and workmanship warranty score, capped at 12 years. Team and approach would award 25 points each for a named lead, crew details, a safety plan, and a monitoring or reporting plan. Each criterion score would be multiplied by its configured weight, and the weighted results would be added to produce a total out of 100.

For example, experience could be scored using the number of qualifying installations, while timeline scores would reward shorter completion times within the required limit. Price and warranty scores would use defined formulas rather than AI-generated judgments.

Each result would show the individual criterion scores, total weighted score, evidence used, and reason for the position. If a required fact is missing or unclear, the system would flag it instead of inventing a value. Using the same verified information and rules should produce the same ranking.

## 3. Human in the Loop

A reviewer would confirm the extracted information and check any missing, conflicting, or uncertain evidence before accepting the ranking. The reviewer would also inspect flagged proposals and make the final award decision. The system would support manual corrections, but it would require a reason for each override.

The audit log would record the proposal reference, extracted values, evidence references, criteria version, scoring breakdown, flags, reviewer actions, overrides, timestamps, and final decision. This would make it possible to understand how a result was produced and who changed it.

## 4. Changing Criteria

Criteria would be stored as configuration in the database rather than hard-coded into the application. If an admin changed a weight or requirement, the system would create a new version of the criteria configuration and validate it before use.

Previously scored evaluations would retain their original criteria version so their results remained explainable. If the admin wanted to apply the new criteria to existing proposals, the system would rescore all relevant proposals using the new version and clearly label the updated results. This would avoid comparing proposals scored under different rules.

## 5. Risks and Safeguards

- **Incorrect extraction:** AI might misread a price, licence number, warranty, or completion time. I would keep references to the source text and ask a reviewer to verify uncertain or important values.
- **Made-up information:** The model might fill in details that are not present. The extraction prompt would require it to return unknown values as null and never guess. The application would not award credit for unsupported claims.
- **Manipulation:** A proposal could contain instructions telling the AI to ignore the criteria or award it full marks. Proposal text would be treated only as evidence, never as instructions. The application would calculate scores independently of the model.
- **Bias and unfair scoring:** Different wording could lead to inconsistent interpretations. A common extraction schema, published scoring rules, and human review would help reduce this risk.
- **Missing information:** A proposal without a confirmed schedule, for example, should be flagged for clarification rather than assigned an assumed completion time.
- **Cost and performance:** Processing every document with a large model could be expensive. I would extract only relevant information, limit unnecessary model calls, and cache results against the document version. Any change to a document would trigger a new extraction.

The system would assist the reviewer rather than make the final procurement decision. Mandatory requirements, transparent scoring, and human approval would remain central to the process.
