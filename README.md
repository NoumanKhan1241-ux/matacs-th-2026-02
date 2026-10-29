
# MATACS Associate Software Developer Assessment

**Candidate:** Muhammad Nouman Khan  
**Assessment Reference:** MATACS-TH-2026-02  

## Overview

This assessment explores the design of an AI-assisted system for reviewing and ranking commercial solar installation proposals. The objective is to make proposal evaluation consistent, explainable, and auditable while keeping mandatory compliance checks and final procurement decisions under human control.

The proposed system combines AI-assisted information extraction with deterministic application logic for eligibility checks, weighted scoring, and ranking.

## Repository Structure

- `README.md` — Project overview, setup instructions, and implementation notes.
- `WRITEUP.md` — Design approach, scoring methodology, risks, and safeguards.
- `PROMPTS.md` — Prompts used during the assessment and proposed extraction workflow.
- `ranking.json` — Proposal ranking and explanations.
- `diagram/workflow.png` — Workflow diagram.
- `prototype/run.py` — Python offline prototype.
- `prototype/extraction_prompt.txt` — Proposed proposal-extraction prompt.
- `prototype/samples/` — Sample proposal text files A–E.
- `prototype/outputs/` — Generated proposal results and ranking.
- `prototype/reviews.json` — Saved human-review decisions.
- `prototype/requirements.txt` — Prototype dependency information.

## Design Approach

The proposed system uses AI to extract relevant information from contractor proposals into a consistent structure. Extracted information would include pricing, experience, completion timelines, warranties, licensing, insurance, WSIB clearance, and team details.

Deterministic application logic would then validate mandatory requirements, calculate weighted scores, and produce a ranking. Missing or conflicting information would be flagged for clarification rather than guessed. Instructions embedded within proposal documents would be treated as untrusted content and would not be allowed to influence the evaluation rules.

A human reviewer would verify important evidence, review flagged proposals, and make the final procurement decision.

## Optional Prototype

I developed an offline Python prototype to demonstrate key parts of the proposed workflow.

### Features

- Reads and inspects sample proposals A–E.
- Performs basic keyword and text checks.
- Identifies missing information and suspicious embedded instructions.
- Demonstrates eligibility checks and human-review logging.
- Calculates weighted scores using configured demonstration data.
- Generates JSON outputs for individual proposals and the ranking.

### Technology

- Python 3
- Python standard library
- JSON for structured outputs

### How to Run

From the repository root, run:

```bash
python prototype/run.py
```

The script reads sample files from `prototype/samples/` and writes generated results to `prototype/outputs/`. Human-review decisions are stored in `prototype/reviews.json`.

No external Python packages or API key are required for the current offline version.

### Current Limitation: API Credit Availability

The prototype is temporarily operating offline because of API credit limitations encountered during development. It does not currently perform live AI-powered extraction.

Instead, it uses basic keyword and text checks against the sample files, while scoring inputs are simulated demonstration data. Consequently, its output should not be treated as independently verified proposal information or as the result of a live AI model.

The extraction prompt and proposed JSON schema demonstrate how AI-assisted extraction could be integrated when API access is available. A future implementation would validate model responses, retain supporting evidence, and pass verified information to the deterministic eligibility and scoring logic.

## Use of AI Tools

I used ChatGPT to help organize my design approach, develop and refine prompts, consider risks, and improve the documentation and prototype logic. I reviewed the suggestions against the assessment requirements rather than accepting them automatically.

The prototype was implemented as an offline demonstration after API credit limitations prevented live model-based extraction. This limitation is disclosed explicitly, and the current scoring inputs are simulated rather than AI-extracted.

## Important Limitations

This submission demonstrates a proposed design and an offline proof of concept, not a production-ready procurement platform. The prototype does not independently verify contractor licences, WSIB clearance, insurance coverage, or experience claims. These details would require appropriate evidence and human verification before a real procurement decision.

The system is intended to support transparent evaluation and human judgment, not replace them.
