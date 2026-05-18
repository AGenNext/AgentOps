# Agent Analytics Contract

Agent-Analytics owns reusable analytics contracts for AGenNext agentic systems.

## Responsibility

Agent-Analytics collects and analyzes signals from:

- objectives
- A2A handoffs
- agent work loops
- model routing
- evaluations
- skills
- product usage
- billing and metering
- customer feedback
- release readiness

## Boundary

```text
Agent-Objective
  → defines goals and completion criteria

Agent-Team
  → emits agent activity and A2A handoff events

Model-Router
  → emits model choice, cost, latency, and routing events

Agent-Eval
  → emits quality, reliability, assurance, and completion scores

Agent-Knowledge
  → emits product usage, artifact, search, and enterprise workflow events

Agent-Analytics
  → aggregates, analyzes, and reports signals
```

## Core Event Categories

```text
objective.created
objective.started
objective.blocked
objective.completed
objective.cancelled

a2a.handoff.created
a2a.handoff.accepted
a2a.handoff.rejected
a2a.handoff.blocked
a2a.handoff.completed

agent.task.started
agent.task.completed
agent.task.failed
agent.task.retried

model.route.requested
model.route.selected
model.route.rejected
model.route.escalated
model.call.completed
model.call.failed

eval.started
eval.completed
eval.failed
eval.regression_detected

artifact.generated
artifact.evaluated
artifact.approved
artifact.rejected
artifact.stale

billing.usage_recorded
billing.quota_exceeded

customer.feedback.created
customer.feedback.triaged
```

## Required Analytics Dimensions

Every event should include where applicable:

```yaml
event_id: string
event_type: string
occurred_at: datetime
tenant_id: string | null
workspace_id: string | null
objective_id: string | null
task_id: string | null
agent_id: string | null
handoff_id: string | null
model_id: string | null
provider_id: string | null
artifact_id: string | null
environment: dev | test | staging | prod
status: string
cost_usd: number | null
latency_ms: integer | null
risk_level: low | medium | high | critical | null
metadata: object
```

## Core Metrics

### Objective Metrics

- objective completion rate
- time to objective completion
- blocker rate
- stop condition rate
- human escalation rate

### Agent Metrics

- task completion rate by agent
- blocker rate by agent
- A2A rejection rate
- handoff latency
- rework cycles per task

### Model Metrics

- model selection frequency
- cost per task
- latency per task
- success rate by model
- evaluation score by model
- policy escalation rate

### Evaluation Metrics

- CLEAR score
- cost
- latency
- efficacy
- assurance
- reliability
- regression rate

### Product Metrics

- activated users
- artifact acceptance rate
- search success rate
- regeneration rate
- stale artifact rate
- feedback-to-roadmap conversion rate

### Business Metrics

- qualified leads
- demo requests
- paid pilots
- conversion rate
- revenue
- usage by plan

## Analytics Loop

```text
events emitted
  → analytics collected
  → metrics computed
  → insights generated
  → objectives/roadmap updated
  → agents adapt behavior
  → repeat
```

## Final Rule

If the system cannot measure it, it cannot reliably improve it.
