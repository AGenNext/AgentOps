# Cloud agent analytics boundary

Agent-Analytics owns metrics, insights, and analytical views across AGenNext agent activity.

## Decision

Agent-Analytics consumes execution, trace, deployment, security, cost, capacity, and runtime data to produce insights.

It does not execute workflows, deploy systems, or own trace schemas.

## Boundary

| Component | Responsibility |
|---|---|
| Agent-Analytics | Metrics, insights, trends, reporting, recommendations |
| Agent-Traces | Trace/audit/timeline contracts and raw event records |
| Agent-Runs | Human debugging/replay UX for individual runs |
| Agent-Dashboard | Operator overview and control surface |
| Agent-Runtime | Executes workflows and emits events |
| Agent-Security | Security scans and pre-deploy gates |
| Agent-deploy | CI/CD and deployment events |
| Agent-FinOps | Cloud cost and financial optimization |

## Agent-Analytics owns

- execution success/failure rates
- workflow duration metrics
- deployment frequency metrics
- failure trend analysis
- security gate pass/fail trends
- infrastructure capacity trends
- runtime usage analytics
- agent performance analytics
- SLA/SLO reporting
- recommendation signals

## Agent-Analytics does not own

- runtime execution
- trace schema authority
- deployment automation
- vulnerability scanning
- cloud provider operations
- user-facing chat UX

## Cloud agent analytics

For the Cloud Architect Agent, Agent-Analytics should report:

- Kimsufi/k8smicro deployment success rate
- average bootstrap duration
- most common failed step
- security gate failures
- Kubernetes rollout failures
- OVH/Kimsufi incident history
- capacity and resource utilization trends
- remediation effectiveness

## Data flow

```txt
Agent-Runtime / Agent-deploy / Agent-Security / AgentKube
  ↓ emit events
Agent-Traces
  ↓ raw timeline/event data
Agent-Analytics
  ↓ aggregated insights
Agent-Dashboard / Agent-Runs / reports
```
