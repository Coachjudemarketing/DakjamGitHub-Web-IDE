# DakJam Human Company Operating Structure

## Purpose

This handbook defines the human organization that must exist before equivalent agent roles are automated. The objective is a small, accountable company that can build, deploy, sell, operate, secure, and continuously improve DakJam enterprise systems with humans remaining responsible for consequential decisions.

## Operating principle

**Automate the work, not the accountability.**

Every automated role has:

- a named owner
- a defined scope
- measurable outputs
- approval boundaries
- escalation rules
- audit requirements
- a human fallback

No agent gets authority merely because it has a job title.

---

# 1. Executive structure

```text
Founder / CEO
│
├── Chief Product & Technology Officer
│   ├── Architecture
│   ├── Engineering
│   ├── AI / Agent Systems
│   └── QA / Release
│
├── Chief Operating Officer
│   ├── Customer Operations
│   ├── Implementation
│   ├── Support
│   └── Process Excellence
│
├── Chief Revenue Officer
│   ├── Sales
│   ├── Marketing
│   ├── Partnerships
│   └── Customer Success
│
├── Security & Trust Lead
│   ├── Security
│   ├── Privacy
│   ├── Compliance
│   └── Incident Response
│
└── Finance & Administration Lead
    ├── Finance
    ├── Contracts
    ├── Procurement
    └── People / Administration
```

For an early-stage company, one human may hold multiple positions. The positions remain separate because their responsibilities and approval boundaries are different.

---

# 2. Short position handbook

| Position | Primary responsibility | Core outputs | Must escalate |
|---|---|---|---|
| Founder / CEO | Vision, capital, final company decisions | Strategy, priorities, major approvals | Legal, financial, reputational, existential risk |
| CTO / Product Technology | Technical direction and product quality | Architecture, roadmap, technical standards | Security exceptions, major outages, irreversible architecture |
| Principal Architect | System architecture | ADRs, reference architectures, integration design | Cross-system conflicts, unsafe designs |
| Engineering Lead | Delivery | Working software, estimates, reviews | Blockers, quality failures, production risk |
| AI/Agent Lead | Agent architecture and evaluation | Model registry, routing, prompts, evaluations | Unsafe autonomy, poor evaluation, provider failure |
| QA/Release Lead | Release confidence | Test plans, CI gates, release reports | Failed critical tests, regression |
| COO | Operating system of company | SOPs, SLAs, workflows, capacity | Repeated operational failures |
| Implementation Lead | Customer deployment | Discovery, configuration, launch plan | Customer data/security concerns |
| Customer Success Lead | Customer outcomes | Adoption, QBRs, success metrics | Churn risk, unresolved escalations |
| Support Lead | Incident and user support | Tickets, incident reports, knowledge base | Security incidents, SLA breach |
| CRO | Revenue system | Pipeline, forecast, sales process | Material commitments or pricing exceptions |
| Sales Lead | New customer acquisition | Qualified pipeline, proposals, closed business | Contract/legal exceptions |
| Marketing Lead | Demand generation | Positioning, campaigns, content, attribution | Brand/reputation risk |
| Partnerships Lead | Strategic integrations | Partner pipeline, agreements, integrations | Data-sharing or commercial exceptions |
| Security & Trust Lead | Security and privacy | Threat model, controls, incident response | Any suspected breach |
| Compliance/Privacy Lead | Regulatory and contractual controls | Policies, reviews, data maps | Regulatory uncertainty |
| Finance Lead | Financial control | Cash flow, billing, budgets, reporting | Fraud, material variance, unusual transactions |
| People/Admin Lead | Hiring and organizational health | Hiring, onboarding, policies | Employment/legal issues |
```

---

# 3. Company-wide rules

### Rule 1 — One source of truth

Code, architecture, product requirements, deployment definitions, and operational runbooks have canonical locations. Duplicates must identify their owner and relationship to the canonical source.

### Rule 2 — Nothing is "done" until it runs

A feature is complete only when it passes the applicable build, test, health, integration, deployment, and user-verification gates.

### Rule 3 — Evidence before certainty

The company distinguishes facts, verified evidence, assumptions, forecasts, and opinions.

### Rule 4 — No silent autonomy

Agents may recommend, draft, analyze, test, and execute within explicit permissions. They may not expand their own permissions.

### Rule 5 — Human ownership

Every automated workflow has a human owner responsible for its outcome.

### Rule 6 — Production is earned

A system moves from development → staging → pilot → production only after passing defined gates.

### Rule 7 — Least privilege

Systems receive only the credentials, data, tools, and actions required for their job.

### Rule 8 — Reversible first

Prefer actions that can be tested, rolled back, or quarantined before irreversible actions.

---

# 4. Daily operating rhythm

## Daily

- Review production health.
- Review incidents and failed automations.
- Review critical customer issues.
- Review revenue/pipeline movement.
- Review agent evaluation regressions.
- Review deployment changes.

## Weekly

- Product/engineering review.
- Agent/model performance review.
- Customer outcomes review.
- Security review.
- Cash/revenue review.
- Priorities and capacity review.

## Monthly

- Financial close.
- Security/control review.
- Product roadmap review.
- Customer retention analysis.
- Model/provider benchmark refresh.
- Automation ROI review.

---

# 5. Enterprise deployment lifecycle

```text
Prospect
  ↓
Discovery
  ↓
Use-case definition
  ↓
Security/privacy review
  ↓
Sandbox
  ↓
Synthetic or approved test data
  ↓
Agent tournament / evaluation
  ↓
Human acceptance
  ↓
Pilot
  ↓
Production gates
  ↓
Enterprise deployment
  ↓
Monitoring
  ↓
Outcome measurement
  ↓
Continuous improvement
```

---

# 6. Human-to-agent transition

An agent can inherit a role only after the human version has:

1. documented the responsibilities;
2. defined inputs and outputs;
3. defined decision boundaries;
4. defined escalation conditions;
5. produced representative examples;
6. established measurable KPIs;
7. created test cases;
8. established an audit trail;
9. passed a shadow-mode evaluation;
10. received human approval for its permitted automation scope.

## Agent role template

```yaml
role: ""
mission: ""
human_owner: ""
inputs: []
outputs: []
tools_allowed: []
data_allowed: []
actions_allowed: []
actions_forbidden: []
kpis: []
quality_gates: []
escalate_when: []
approval_required_for: []
model_requirements: []
backup_models: []
audit_events: []
rollback_plan: ""
```

---

# 7. DakJam agent-company structure

Once the human organization is validated, agent equivalents can be introduced by department.

```text
DAKJAM HUMAN COMPANY
        │
        ▼
ROLE DEFINITIONS
        │
        ▼
PROCESS DOCUMENTATION
        │
        ▼
AGENT SPECIFICATION
        │
        ▼
SHADOW MODE
        │
        ▼
TOURNAMENT / EVALUATION
        │
        ▼
LIMITED AUTOMATION
        │
        ▼
HUMAN-ON-THE-LOOP
        │
        ▼
MEASURED AUTONOMY
```

Agents should be treated as **software workers**, not employees or legal persons. Human leaders remain accountable for the company and its customers.

---

# 8. Initial agent departments

### Executive Intelligence

- Strategy Analyst
- Chief-of-Staff Agent
- Research Agent
- Decision Analyst

### Product & Engineering

- Product Analyst
- Architect Agent
- Developer Agent
- Code Reviewer
- QA Agent
- Release Agent
- DevOps Agent

### AI Systems

- Model Router
- Research Agent
- Debate Agents
- Adversarial Agent
- Evaluation Agent
- Judge Agent
- Memory Curator

### Revenue

- Market Research Agent
- Lead Research Agent
- Sales Development Agent
- Proposal Agent
- CRM Agent
- Customer Success Agent

### Operations

- Workflow Analyst
- Implementation Agent
- Support Agent
- Knowledge Agent
- Reporting Agent

### Security & Trust

- Security Monitor
- Policy Agent
- Compliance Assistant
- Incident Triage Agent

Agents in these departments must inherit the human role's documented permissions rather than receiving broad access by default.

---

# 9. Enterprise readiness gates

A DakJam company/application should not enter productive enterprise deployment until:

| Gate | Required |
|---|---|
| Requirements defined | Yes |
| Owner assigned | Yes |
| Architecture reviewed | Yes |
| Security review | Yes |
| Data boundaries defined | Yes |
| Secrets managed correctly | Yes |
| Automated tests | Yes |
| Agent evaluation | Yes |
| Adversarial tests | Yes |
| Rollback plan | Yes |
| Monitoring | Yes |
| Health checks | Yes |
| Customer acceptance | Yes |
| Human escalation | Yes |
| Audit trail | Yes |
| Incident process | Yes |

---

# 10. The human review checkpoint

Before converting a human role into an automated agent role, the Founder/CEO and responsible functional owner review:

- What the role does.
- What the role must never do.
- What information it can access.
- What tools it can use.
- What decisions it can make.
- What actions require approval.
- What happens when it is uncertain.
- How performance is measured.
- How it is stopped.
- How its actions are audited.

**Approval phrase:** `WORD — APPROVED FOR AGENTIZATION`

Until that approval, the role remains human-operated or shadow-only.
