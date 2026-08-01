# DakJam Multi-Model Routing Blueprint

Date: 2026-07-31

## Goal

Build a private, provider-agnostic DakJam intelligence layer that selects model groups by task, runs independent research and adversarial debate in parallel, scores outputs with a stable rubric, and sends only validated decision briefs to the human.

This is a routing blueprint, not a claim that any one leaderboard is permanently best. Frontier models change quickly, so DakJam should continuously benchmark its own workloads and update routing from measured results.

## Current research snapshot

- OpenAI GPT-5.5 is reported by Artificial Analysis as the April 2026 Intelligence Index leader and strong on terminal/agentic tasks, with a higher token price than GPT-5.4 but improved token efficiency. Source: Artificial Analysis, Apr 23 2026.
- Anthropic Claude Opus 4.8 took the Intelligence Index lead in May 2026 and showed strong agentic knowledge work, scientific reasoning, terminal use, and lower hallucination rates on the cited evaluation set. Source: Artificial Analysis, May 28 2026.
- Google Gemini 3.1 Pro is positioned by Google for complex tasks and is available through Gemini API, Vertex AI, Gemini, and NotebookLM. Independent ConfidenceBench results reported Gemini 3.1 Pro Preview among the best-calibrated models tested.
- xAI Grok 4.5 is reported by Artificial Analysis as #4 on its Intelligence Index, with strong agentic knowledge work and coding, and coding-agent performance roughly on par with GPT-5.5 in the cited harness.
- Kimi K3 is reported by Artificial Analysis as #3 on its Intelligence Index as of July 17 2026, with especially strong agentic workflow and long-horizon knowledge-work results.
- DeepSeek-V4 provides an important cost/open-weight branch. Official DeepSeek documentation reports V4-Pro and V4-Flash, 1M context, thinking/non-thinking modes, tool calls, and OpenAI/Anthropic-compatible APIs.
- Qwen remains strategically valuable as an open-weight/agentic branch. Qwen reports strong agent capabilities across its newer Qwen3.6/Qwen3.7 families.

## Strategic conclusion

Do not create a single permanent "best model". Create **model cells**: interchangeable groups optimized for a task family. A tournament can replace one or two participants without changing the rest of the system.

## Recommended model cells

| Use case | Primary | Challenger | Specialist | Judge | Cheap/scale fallback |
|---|---|---|---|---|---|
| General strategic decisions | GPT-5.5 | Claude Opus 4.8 | Gemini 3.1 Pro | Claude/GPT cross-judge | DeepSeek-V4-Flash |
| Deep research | Gemini 3.1 Pro | GPT-5.5 | Claude Opus 4.8 | Gemini/GPT cross-judge | DeepSeek-V4-Pro |
| Software architecture | Claude Opus 4.8 | GPT-5.5 | Grok 4.5 | GPT/Claude cross-judge | Qwen/DeepSeek |
| Coding implementation | GPT-5.5 | Claude Opus 4.8 | Grok 4.5 | GPT/Claude | DeepSeek-V4 |
| Adversarial critique | Grok 4.5 | Claude Opus 4.8 | GPT-5.5 | Gemini/GPT | DeepSeek-V4-Pro |
| Long-context synthesis | Gemini 3.1 Pro | Kimi K3 | Claude Opus 4.8 | GPT/Claude | DeepSeek-V4 |
| Agentic workflow planning | Claude Opus 4.8 | Kimi K3 | GPT-5.5 | GPT/Claude | Qwen/DeepSeek |
| Multimodal analysis | Gemini 3.1 Pro | Qwen3.7-Plus | GPT-5.5 | Claude/GPT | Qwen open-weight |
| Cost-sensitive exploration | DeepSeek-V4-Flash | Qwen | Kimi | GPT/Claude | local/open-weight |
| Forecasting / futures | GPT-5.5 | Gemini 3.1 Pro | Claude Opus 4.8 | independent jury | DeepSeek/Qwen |

These are starting hypotheses. DakJam should promote/demote models based on its own evaluation corpus rather than treating this table as static truth.

## Tournament topology

### Standard 5-seat tournament

1. **Generator** — creates an independent solution.
2. **Researcher** — searches for evidence and counterevidence.
3. **Skeptic** — attacks the solution and assumptions.
4. **Builder/Tester** — checks feasibility and creates tests.
5. **Judge** — scores all artifacts against a fixed rubric.

Run seats concurrently whenever dependencies permit.

### 7-seat high-stakes tournament

Add:

- **Contrarian** — intentionally argues for the strongest alternative.
- **Verifier** — checks citations, calculations, and test evidence.

### 11-seat frontier tournament

Add multiple independent generators and judges. Rotate model assignments to reduce provider-specific bias.

## Research protocol

For research-heavy questions, the orchestrator creates a query tree rather than one giant prompt:

```text
Question
├── definitions
├── current state
├── primary sources
├── opposing evidence
├── historical evidence
├── quantitative evidence
├── implementation evidence
├── edge cases
├── failure modes
└── unknowns
```

Each branch can run parallel searches. Results are deduplicated, source-ranked, contradiction-checked, and attached to claims.

Deep research should be treated as a **research capability**, not as a model identity. OpenAI documents that deep research can plan multi-step investigations, search/evaluate sources, use uploaded files and connected apps, and produce cited reports. DakJam should implement the same conceptual separation: planner → retrieval → evidence evaluation → synthesis.

## Boundary-pushing research policy

"Push the boundary" should mean **maximize legitimate information retrieval and hypothesis testing**, not bypass access controls, authentication, paywalls, robots restrictions, private data boundaries, or safety controls.

Allowed research expansion:

- more independent queries
- alternate terminology
- primary-source searches
- contradictory-source searches
- historical comparisons
- technical documentation
- academic literature
- public repositories
- public filings and public datasets
- user-supplied/private authorized sources
- repeated verification of important claims

The orchestrator should stop when the marginal information gain falls below a configurable threshold or when the evidence budget is exhausted.

## Shared research memory

Create a common evidence object so every agent can work from the same verified material without blindly copying another agent's conclusion.

```json
{
  "claim_id": "uuid",
  "claim": "...",
  "source_refs": [],
  "source_quality": 0,
  "independent_support": 0,
  "contradictions": [],
  "last_verified": "timestamp",
  "confidence": 0
}
```

Agents may challenge claims, but should not silently rewrite the shared evidence ledger.

## Scoring

Use a configurable 100-point rubric:

| Criterion | Default weight |
|---|---:|
| Correctness | 20 |
| Evidence quality | 15 |
| Reasoning quality | 15 |
| Feasibility | 15 |
| Robustness | 10 |
| Security/safety | 10 |
| Cost/efficiency | 5 |
| Novelty/option value | 5 |
| Clarity/actionability | 5 |

For research questions, shift weight toward evidence and source quality. For implementation, shift weight toward tests, correctness, and maintainability.

## Judge design

Never rely on one model to judge itself. Use cross-provider judging when possible.

Preferred pattern:

```text
Model A proposes
Model B proposes
Model C proposes
       ↓
Evidence ledger
       ↓
Model D critiques
Model E critiques
       ↓
Independent judges
       ↓
Score aggregation
       ↓
Confidence + disagreement analysis
       ↓
Lead orchestrator
```

A disagreement should be preserved as a first-class result. Consensus is not automatically truth.

## Model performance memory

DakJam should maintain a rolling scorecard by task family:

| Metric | Meaning |
|---|---|
| Accuracy | Correctness on known-answer tests |
| Citation precision | Fraction of cited claims actually supported |
| Citation recall | Relevant evidence found |
| Calibration | Whether confidence tracks correctness |
| Adversarial resistance | Performance under hostile critique |
| Tool reliability | Successful tool use |
| Code success | Tests/builds passing |
| Cost | Cost per successful task |
| Latency | End-to-end completion time |
| Judge agreement | Stability across independent judges |

The router should use these measured values to select participants.

## Dynamic substitution

A tournament cell should be represented by capabilities, not hard-coded model names:

```json
{
  "cell": "software_architecture",
  "seats": [
    {"role":"generator","capabilities":["reasoning","coding"]},
    {"role":"skeptic","capabilities":["adversarial_reasoning"]},
    {"role":"researcher","capabilities":["web","citations"]},
    {"role":"tester","capabilities":["coding","tools"]},
    {"role":"judge","capabilities":["evaluation","calibration"]}
  ]
}
```

The router resolves each seat to the best currently validated model. This means changing one or two models does not require changing application logic.

## Human output

The swarm should not dump the entire debate into the normal user experience. Produce:

- decision
- confidence
- winning proposal
- strongest alternative
- evidence summary
- major disagreement
- failed tests
- unresolved unknowns
- recommended next action
- human approval requirement

Store the full trace privately for authorized audit/research use.

## Continuous improvement loop

```text
Task
 → Tournament
 → Decision
 → Real-world outcome
 → Outcome scoring
 → Model/task scorecard
 → Router update
 → Better tournament
```

This is the key mechanism for turning a collection of models into a DakJam-specific decision system.

## Initial implementation phases

### Phase 1 — Routing foundation
- provider-neutral adapter interface
- model registry
- capability registry
- task taxonomy
- tournament configuration
- rubric engine

### Phase 2 — Research engine
- query planner
- parallel search workers
- source/evidence ledger
- contradiction detector
- citation verifier

### Phase 3 — Arena
- agent roles
- debate rounds
- adversarial testing
- cross-provider judging
- confidence aggregation

### Phase 4 — Evaluation
- DakJam benchmark corpus
- golden tasks
- regression suite
- model scorecards
- automatic routing updates

### Phase 5 — Private production
- policy engine
- secrets isolation
- tenant/data boundaries
- audit logs
- human approval gates
- cost/latency budgets

## Non-negotiable architecture rule

DakJam owns the **protocol, memory, evaluation, routing, rubrics, and decision process**. Model vendors provide replaceable intelligence modules. No vendor-specific model should become a single point of failure or the definition of intelligence for the platform.
