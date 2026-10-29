# MATACS Associate Software Developer Assessment

**Candidate:** Muhammad Nouman Khan

**Assessment Reference:** MATACS-TH-2026-02

## Overview

This assessment explores how I would design an AI assisted system for reviewing and ranking contractor proposals. My main focus is to make the process reliable, explainable and easy for a human reviewer to understand.

## Files

- [Design Write Up](WRITEUP.md)
- [AI Prompts](PROMPTS.md)
- [Proposal Ranking](ranking.json)
- [Process Flow Diagram](diagram/workflow.png)

## Design Approach

My approach is to use AI for extracting information from proposal documents and understanding qualitative details. I would use normal application logic to check mandatory requirements, calculate scores and produce the ranking. A human reviewer would check uncertain results and make the final decision.

## Use of AI Tools

I used ChatGPT to help organize my ideas, explore possible risks and review my proposed scoring approach. I did not accept every suggestion without considering the assessment requirements. For example, I chose to flag Proposal D for clarification instead of assuming a completion time that was not provided in the proposal.


## Prototype

I developed an offline Python prototype to demonstrate how proposal-review automation could work. It inspects sample proposal files, performs basic keyword and text checks, identifies missing information, detects suspicious embedded instructions, and generates JSON outputs for review.

### Features

- **Proposal inspection:** Reads the five sample proposals (A–E).
- **Basic text checks:** Looks for information related to licensing, WSIB, insurance, pricing, timelines, and warranties.
- **Risk identification:** Flags suspicious embedded instructions so they cannot influence the scoring process.
- **Human review:** Records a review decision and reason for Proposal C before allowing it to be considered for ranking.
- **Eligibility checks:** Flags missing or inconsistent information and identifies proposals that do not meet the configured requirements.
- **Scoring and ranking:** Calculates weighted scores for eligible proposals with complete scoring inputs.
- **JSON outputs:** Saves individual proposal results, a generated ranking, and human-review decisions.

### Technology

- Python 3
- Python standard library (`json`, `re`, `pathlib`, and `datetime`)
- JSON for structured outputs

### How to Run

From the repository root, execute:

```bash
python prototype/run.py
```

The prototype reads sample files from `prototype/samples/` and saves generated results in `prototype/outputs/`. Human-review decisions are stored in `prototype/reviews.json`.

### Current Limitations

This is an offline proof of concept, not a production-ready AI extraction system. It uses keyword-based text checks and simulated scoring inputs; it does not call a live AI model or independently verify contractor credentials, insurance, WSIB clearance, or supporting evidence. The human-review step demonstrates an approval workflow but does not replace a formal procurement review. The results should therefore be treated as illustrative rather than as verified procurement recommendations.
