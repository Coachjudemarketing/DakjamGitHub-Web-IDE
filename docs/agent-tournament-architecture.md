# DakJam Swarm Intelligence Engine

## Purpose

An internal multi-model decision layer that runs structured agent tournaments before presenting a concise decision brief to a human.

## Pipeline

1. **Problem Intake** — normalize the question, objective, constraints, assumptions, unknowns, and success criteria.
2. **Independent Proposals** — agents solve independently to reduce groupthink.
3. **Cross Examination** — agents challenge competing proposals.
4. **Evidence Challenge** — claims are classified as verified, supported, assumed, or speculative.
5. **Adversarial Testing** — deliberately try to break the leading proposals.
6. **Rubric Scoring** — score correctness, evidence, feasibility, security, cost, scalability, novelty, and robustness using configurable weights.
7. **Lead Judge** — select the strongest proposal while accounting for uncertainty and confidence.
8. **Validation Gate** — require configured tests/parameters to pass before a result can be promoted.
9. **Human Decision Brief** — expose only the decision, confidence, reasons, disagreements, unknowns, evidence, and recommended next action.
10. **Outcome Tracking** — compare predictions with real-world outcomes and feed results back into future tournaments.

## Internal components

- `orchestrator`: creates tournaments and coordinates agents.
- `arena`: manages rounds, turns, and isolation boundaries.
- `agents`: role-specific model adapters.
- `rubrics`: configurable scoring definitions and weights.
- `evaluation`: deterministic and model-assisted evaluation.
- `adversary`: failure-mode and counterexample generation.
- `validator`: test and parameter gates.
- `judge`: confidence-aware winner selection.
- `memory`: tournament history, evidence, decisions, and outcomes.
- `briefing`: human-facing summaries.
- `telemetry`: cost, latency, model performance, and audit events.

## Default roles

| Role | Responsibility |
|---|---|
| Strategist | Generate the strongest solution |
| Skeptic | Attack assumptions and arguments |
| Researcher | Gather and evaluate evidence |
| Engineer | Test implementation feasibility |
| Risk Agent | Identify failure modes |
| Business Agent | Test economics and adoption |
| Safety Agent | Test safety, privacy, and policy boundaries |
| Futurist | Explore second- and third-order effects |
| Tester | Create adversarial test cases |
| Lead Judge | Score and select the result |

## Default rubric

| Criterion | Weight |
|---|---:|
| Correctness | 25 |
| Evidence | 15 |
| Feasibility | 20 |
| Security | 15 |
| Cost | 10 |
| Scalability | 5 |
| Novelty | 5 |
| Robustness | 5 |

Weights must be configurable and validated to total 100.

## Confidence-aware selection

A raw score is not sufficient. The judge should report both score and confidence, preserve close calls, and surface material disagreements instead of hiding uncertainty.

## Human gate

No high-impact action should be automatically executed merely because an agent won a tournament. The validator must confirm required parameters and tests, and configurable approval policies determine whether the system may proceed automatically or must ask the human.

## Internal UI principle

The orchestration layer may remain out of the normal application UI. It should still produce auditable structured records for authorized administrators: tournament ID, agents/models used, rubric version, evidence references, test results, scores, confidence, winner, and final decision brief.

## Suggested tournament record

```json
{
  "tournament_id": "uuid",
  "problem": {},
  "rounds": [],
  "evidence": [],
  "tests": [],
  "rubric_version": "v1",
  "scores": [],
  "winner": {},
  "confidence": 0,
  "validation": {"passed": false, "gates": []},
  "human_decision": null,
  "outcome": null
}
```

## Design rule

Treat the swarm as a decision-support and validation system, not as an authority. The human remains the final authority for consequential decisions unless an explicitly configured low-risk automation policy says otherwise.
