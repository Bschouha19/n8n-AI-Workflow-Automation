# n8n Automation Engineering Course Index
### Master Automation Engineering — From Event-Driven Fundamentals to Production AI-Native Systems, Volume 5

---

> **Prerequisites:** [Volume 1 — AI Engineering](https://github.com/Bschouha19/AI-Engineering-Handbook), [Volume 2 — MCP Engineering](https://github.com/Bschouha19/MCP-Engineering) (Chapter 12's own "n8n and MCP" chapter depends directly on this), [Volume 3 — RAG Deep Dive](https://github.com/Bschouha19/RAG-Deep-Dive), and [Volume 4 — AI Agent Engineering](https://github.com/Bschouha19/AI-Agent-Engineering) (reasoning loops, memory, orchestration, human oversight, and evaluation are all reused, not re-taught).
>
> **Assumed knowledge:** Everything from Volumes 1–4. Basic HTTP/REST and JSON are assumed; no prior n8n experience is assumed.

> **What you will build by the end:** A production-grade, AI-native automation platform for Aperture Cloud — event-driven triggers, reliable and modular workflows, an MCP-connected AI agent with retrieval and human-approval gates, deployed, scaled, observed, and governed like real production software, not a demo.

---

## Progress

**7 of 20 chapters complete — Module 1 fully complete, Module 2 underway.** Chapters 01–04 shipped 2026-07-11. Chapters 05–07 shipped 2026-07-12 — see [ROADMAP.md](./ROADMAP.md) for the kickoff research log.

---

## Design Philosophy — Why This Course Is Structured This Way

This course teaches **automation engineering**, not n8n's menu system. Every chapter follows the same discipline this series has used since Volume 1: explain *why* a problem exists and how it's solved in general, before showing *how* n8n solves it specifically. A reader who finishes this course should be able to reason about Temporal, Airflow, Zapier, or a hand-rolled event bus just as confidently as about n8n — n8n is the concrete teaching vehicle, not the ceiling of what's taught.

**The Architecture-First Thread.** Every chapter's Core Concepts section teaches the underlying engineering idea (idempotency, orchestration vs. choreography, dead-letter handling, RBAC) before it teaches which n8n node implements it. Technology Comparison sections throughout keep n8n honestly positioned against real alternatives — Zapier and Make for non-technical simplicity, Windmill/Temporal for code-first durable execution, Airflow for batch data pipelines — rather than treating n8n as the only tool that exists.

**The Autonomy Thread (continued from Volume 4).** Modules 1–2 use safe, reversible Aperture Cloud scenarios — internal notifications, data syncing, reporting. From Module 3 onward, once AI agents enter the canvas, workflows are permitted genuinely consequential real-world capability (sending real communications, writing to real systems, autonomous decision-making) — the exact same escalation discipline Volume 4 used, continued rather than restarted.

**Real production issues, every chapter, not just the security chapter.** Following Volume 4's discipline exactly: every chapter includes at least one realistic, named production issue. See the table below for the planned anchor per topic — several are grounded in real, current, verified incidents (the Ni8mare RCE, CVE-2026-25049), the rest in realistic Aperture Cloud scenarios consistent with this series' citation discipline.

| Topic | Planned production issue |
|---|---|
| Event-driven thinking | Duplicate webhook deliveries processed twice — no idempotency key, a customer gets charged twice |
| Data transformation | Malformed upstream API response silently corrupts downstream records for days before anyone notices |
| Reliability | A non-idempotent retry after a timeout creates duplicate side effects (double-sent email, double-charged invoice) |
| Workflow design patterns | A fan-out workflow with no rate limiting takes down a partner's API |
| Modular design | A 120-node monolithic workflow becomes unmaintainable and undebuggable |
| AI-native automation | An unbounded AI Agent loop burns an API budget in hours — the same class of failure as Volume 4 Chapter 01/11, now with no engineer watching a terminal |
| MCP integration | An unauthenticated MCP Server Trigger exposes internal workflow capability to any caller |
| Deployment | A queue-mode misconfiguration silently drops executions under load |
| Scaling | Worker starvation under real traffic — executions queue for hours with no alert |
| Observability | A workflow has been failing silently for a week; nobody knew because no one was watching |
| Governance | Credential sprawl — the same API key pasted into a dozen workflows, unrotatable without breaking all of them |
| Security | The real Ni8mare-class unauthenticated RCE pattern (CVE-2026-21858) — how it happened, how to prevent it |

---

## Course Structure

### MODULE 1 — AUTOMATION ENGINEERING FOUNDATIONS
*Go past "drag and drop nodes" into the actual engineering discipline of automation systems.*

| # | Chapter | File | Status | Key Skills |
|---|---------|------|--------|-----------|
| 01 | Automation Architecture — Orchestration, Choreography, and the Trigger-Action Model | chapters/chapter-01-automation-architecture.md | ✅ Complete | Sync vs. async, orchestration vs. choreography, idempotency, delivery semantics, when NOT to use a visual platform (vs. Temporal/Airflow) |
| 02 | Event-Driven Thinking and n8n's Trigger Model | chapters/chapter-02-event-driven-thinking.md | ✅ Complete | Events vs. polling, ordering, deduplication, idempotent handlers, n8n's full trigger taxonomy |
| 03 | The n8n Data Model and Expressions | chapters/chapter-03-data-model-expressions.md | ✅ Complete | Items, `json`/`binary`, `$json`/`$input`/`$node`, IF/Switch/Merge/Filter |
| 04 | Connecting to the World — APIs, Webhooks, and Credentials | chapters/chapter-04-connecting-to-the-world.md | ✅ Complete | HTTP Request node, Credentials Manager, webhook authentication, OAuth2/API key patterns |

**Module 1 Learning Goal:** Understand automation as an engineering discipline — not a drag-and-drop skill — and be able to build and connect a real, working, authenticated integration.

**Module 1 Project:** An event-driven workflow (webhook-triggered) that calls a real external API, handles the response correctly, and is authenticated end to end.

---

### MODULE 2 — WORKFLOW DESIGN PATTERNS AND RELIABILITY ENGINEERING
*Master the patterns and reliability discipline that separate a production workflow from a demo.*

| # | Chapter | File | Status | Key Skills |
|---|---------|------|--------|-----------|
| 05 | Data Transformation and Validation at Scale | chapters/chapter-05-data-transformation.md | ✅ Complete | Schema mapping, malformed/missing data handling, batch processing, pagination |
| 06 | Workflow Design Patterns | chapters/chapter-06-workflow-design-patterns.md | ✅ Complete | Fan-out/fan-in, saga/compensating transactions, pipeline, request-reply, competing consumers |
| 07 | Reliability and Error Recovery | chapters/chapter-07-reliability-error-recovery.md | ✅ Complete | Retry/backoff, circuit breakers (extends Vol4 Ch03), dead-letter thinking, Error Trigger/Workflow |
| 08 | Modular Workflow Design and Workflows as Code | chapters/chapter-08-modular-workflow-design.md | 🔜 Next | Sub-workflows, one-workflow-per-task, composition, versioning workflows like software |

**Module 2 Learning Goal:** Design workflows using named, reusable patterns, and build in the reliability and modularity that separates production automation from a fragile demo.

**Module 2 Project:** A modular, sub-workflow-based system with explicit error handling and a documented retry/backoff strategy for at least one flaky external dependency.

---

### MODULE 3 — AI-NATIVE AUTOMATION
*Where this course's real center of gravity lives — n8n as an agent-orchestration platform, not just an integration tool.*

| # | Chapter | File | Status | Key Skills |
|---|---------|------|--------|-----------|
| 09 | The AI Agent Node — LangChain Inside the Canvas | chapters/chapter-09-ai-agent-node.md | 🔜 | Model/Memory/Chain node families, bounded agent loops (extends Vol4 Ch01) |
| 10 | Retrieval and Memory in n8n | chapters/chapter-10-retrieval-memory.md | 🔜 | Vector Store nodes, visual RAG pipelines (extends Vol3, Vol4 Ch04/11) |
| 11 | Tool-Calling and Multi-Agent Orchestration | chapters/chapter-11-tool-calling-multi-agent.md | 🔜 | Tools Agent, sub-workflows as agent tools, human-in-the-loop gates (extends Vol4 Ch05/08) |
| 12 | n8n and MCP — Bridging Visual Automation and the Agent Ecosystem | chapters/chapter-12-n8n-and-mcp.md | 🔜 | MCP Server Trigger, MCP Client Tool, n8n's native MCP server (extends Vol2, Vol4 Ch09) |
| 13 | The AI Workflow Builder and Evaluating AI Workflows | chapters/chapter-13-ai-workflow-builder-evaluation.md | 🔜 | Prompt-to-automation, n8n Evaluations, trajectory thinking (extends Vol4 Ch12) |

**Module 3 Learning Goal:** Build genuinely agentic automation — not just AI-flavored integrations — with the same bounded-autonomy discipline Volume 4 established, now expressed visually.

**Module 3 Project:** An MCP-connected AI agent workflow with retrieval, at least one tool exposed via a sub-workflow, and a human-approval gate for its one consequential action.

---

### MODULE 4 — PRODUCTION ENGINEERING
*Take a workflow from "works on my instance" to deployed, scaled, observed, and governed — four distinct disciplines, not one settings menu.*

| # | Chapter | File | Status | Key Skills |
|---|---------|------|--------|-----------|
| 14 | Custom Code Nodes — JavaScript and Python | chapters/chapter-14-custom-code-nodes.md | 🔜 | The Code node, npm/pip packages, performance tradeoffs, community nodes |
| 15 | Deployment Architecture | chapters/chapter-15-deployment-architecture.md | 🔜 | Docker/Compose, environments, CI/CD, self-hosted vs. Cloud decision framework |
| 16 | Scaling n8n in Production | chapters/chapter-16-scaling-n8n.md | 🔜 | Queue mode, Redis, worker containers, capacity planning, AI-workflow cost at scale |
| 17 | Observability — Knowing When Automation Breaks | chapters/chapter-17-observability.md | 🔜 | Execution logs, monitoring, alerting, debugging a silently-failing production workflow |
| 18 | Governance and Compliance | chapters/chapter-18-governance-compliance.md | 🔜 | RBAC/projects, Git-based source control and environments, audit logs, SOC2/SSO |

**Module 4 Learning Goal:** Operate n8n the way you'd operate any other piece of production infrastructure — deployed deliberately, scaled with headroom, observed continuously, and governed with real, auditable access control.

**Module 4 Project:** A queue-mode, multi-worker n8n deployment with RBAC-scoped projects, Git-based environments, an alerting pipeline for silent failures, and an audit trail proving who changed what.

---

### MODULE 5 — SECURITY AND CAPSTONE
*Where the stakes are real, and everything gets assembled into one system.*

| # | Chapter | File | Status | Key Skills |
|---|---------|------|--------|-----------|
| 19 | Securing n8n in Production | chapters/chapter-19-securing-n8n.md | 🔜 | Real CVE case studies, credential hygiene, webhook auth, prompt-injection risk in AI Agent workflows |
| 20 | Capstone — Aperture Cloud's Production Automation Platform | chapters/chapter-20-capstone.md | 🔜 | Everything: event-driven, reliable, MCP-connected AI agent, RAG, human approval, deployed, scaled, observed, governed |

**Capstone System:** A production automation platform for Aperture Cloud — event-driven triggers feeding reliable, modular sub-workflows; an MCP-connected AI agent with retrieval and a human-approval gate for its one consequential capability; deployed in queue mode, observed with real alerting, and governed with RBAC and Git-based environments. Explicitly designed so a reader can substitute their own company's automation needs with no conceptual gap.

---

## Chapter Dependency Map

```
Ch 01 (Automation Architecture)
  └─► Ch 02 (Event-Driven Thinking)
        └─► Ch 03 (Data Model & Expressions)
              └─► Ch 04 (Connecting to the World)
                    └─► Ch 05 (Data Transformation at Scale)
                          └─► Ch 06 (Workflow Design Patterns)
                                └─► Ch 07 (Reliability & Error Recovery)
                                      └─► Ch 08 (Modular Design & Workflows as Code)
                                            └─► Ch 09 (AI Agent Node)
                                                  └─► Ch 10 (Retrieval & Memory)
                                                        └─► Ch 11 (Tool-Calling & Multi-Agent)
                                                              └─► Ch 12 (n8n and MCP)
                                                                    └─► Ch 13 (AI Workflow Builder & Evaluation)
                                                                          └─► Ch 14 (Custom Code Nodes)
                                                                                └─► Ch 15 (Deployment Architecture)
                                                                                      └─► Ch 16 (Scaling)
                                                                                            └─► Ch 17 (Observability)
                                                                                                  └─► Ch 18 (Governance & Compliance)
                                                                                                        └─► Ch 19 (Security)
                                                                                                              └─► Ch 20 (Capstone)
```

---

## Cross-Volume Reference Map

| Volume 5 Topic | Earlier Volume Connection |
|---|---|
| Ch 01 (Automation Architecture) | Vol 4 Ch 01 — the "bounded reasoning loop" concept has a direct parallel in bounded, idempotent workflow execution |
| Ch 02 (Event-Driven Thinking) | Vol 4 Ch 06 — A2A's synchronous request/response contrasted against genuinely event-driven, decoupled communication |
| Ch 05 (Data Transformation) | Vol 3 — chunking/preprocessing discipline, applied to workflow data instead of documents |
| Ch 06 (Workflow Design Patterns) | Vol 4 Ch 05 — fallback hierarchies and topology choices have direct workflow-pattern analogues |
| Ch 07 (Reliability & Error Recovery) | Vol 4 Ch 01, 03, 08 — bounded loops, circuit breakers, and TTL-expiry are the same discipline in a new surface |
| Ch 09 (AI Agent Node) | Vol 4 Ch 01–03 — the reasoning loop, tool use, and bounded autonomy, now built visually |
| Ch 10 (Retrieval & Memory) | Vol 3 (RAG), Vol 4 Ch 04, 11 — memory systems and bounded agentic RAG, reused directly |
| Ch 11 (Tool-Calling & Multi-Agent) | Vol 4 Ch 05, 08 — orchestration topologies and human-in-the-loop gating |
| Ch 12 (n8n and MCP) | **Vol 2 (MCP Engineering)** directly — this chapter is the concrete payoff of Volume 2's entire subject; Vol 4 Ch 09's SDK+MCP pattern |
| Ch 13 (AI Workflow Builder & Evaluation) | Vol 4 Ch 12 — trajectory vs. outcome evaluation, applied to visual workflows |
| Ch 16 (Scaling) | Vol 4 Ch 14 — fleet-level governance, same discipline at the infrastructure layer |
| Ch 17 (Observability) | Vol 4 Ch 14 — fleet-level tracing and observability, same discipline applied to workflow executions instead of agent trajectories |
| Ch 18 (Governance & Compliance) | Vol 4 Ch 13 — identity, access control, and audit, applied to workflow/credential ownership instead of agent identity |
| Ch 19 (Security) | Vol 4 Ch 13, Vol 2 (MCP security), Vol 1 (AI Security) |

---

## Learning Path Options

### Standard Path (recommended)
Read all 20 chapters in order. Takes approximately 9–11 weeks part-time.

### No-Code Practitioner Path
Ch 01 → 02 → 03 → 04 → 05 → 07 → 08 → 09 → 10 → 13
Skips: named design-pattern theory (Ch06), custom code (Ch14), and deep production-ops chapters (Ch15–18) — for a reader who wants to build real, reliable AI-augmented automations without becoming an infrastructure operator.

### Platform Engineer / SRE Path
Ch 01 → 02 → 06 → 07 → 08 → 14 → 15 → 16 → 17 → 18 → 19
Focus: running n8n as production infrastructure at scale — deployment, scaling, observability, governance, and security in full — skipping the AI-native module entirely.

### AI Automation Specialist Path
Ch 01 → 02 → 03 → 04 → 09 → 10 → 11 → 12 → 13 → 19
Focus: the AI-native module in full, with just enough foundation and security to build responsibly — skips deep production-ops depth.

---

*Last updated: 2026-07-11 — 0 of 20 chapters complete. Curriculum design phase, kickoff research complete, awaiting approval before Chapter 01.*
