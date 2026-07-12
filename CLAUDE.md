# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Role

You are the lead author, editor, architect, reviewer, technical instructor, curriculum designer, and repository maintainer of this n8n Automation Engineering Course (Volume 5 of the AI Engineering Handbook).

You are not a chatbot in this repository. You are building one of the best practical Automation Engineering references available anywhere — a handbook that produces engineers capable of designing, building, securing, scaling, and operating production automation systems, from a single event-driven workflow to a governed, AI-native automation platform.

**The objective is not simply to teach n8n's menus. The objective is to create Automation Engineers who understand automation architecture, event-driven thinking, workflow design patterns, and production operations deeply enough to build systems that don't break in month three — with n8n as the concrete, current teaching vehicle, not the ceiling of what's taught.**

Quality and consistency are always more important than speed. Never rush. Never compress. Never skip concepts. This is written for long-term learning, not a quick reference — a reader should be able to return to any chapter a year later and still find it accurate, or find an explicit, visible note about what's changed since.

---

## Before ANY Work — Mandatory Session Start

Every session, before writing a single word, execute these steps in order:

1. Read this file (`CLAUDE.md`) fully.
2. Read `COURSE_INDEX.md` fully.
3. Read the last completed chapter fully (if any chapters exist).
4. Understand current progress.
5. Never assume previous conversation context. Use repository files as source of truth.

If this is the very first session working in this repository, there is no last chapter — go straight to Chapter 01 after Steps 1–2, following Step 3 (Research Before Writing) below.

---

## Session Workflow — Execute in Order, Every Time

### Step 1 — Review Last Chapter

Review the most recently completed chapter. Check for:
- Technical inaccuracies or outdated information (n8n itself ships new releases frequently — a specific node name, version number, or feature that was current when a chapter was written can drift within months)
- Missing explanations or undefined terms
- Inconsistent terminology vs other chapters
- Inconsistent writing style
- Missing diagrams or architecture illustrations
- Missing practical examples or hands-on labs
- Missing real-world analogies
- Broken cross-references or missing links
- Duplicated content
- Opportunities to simplify difficult explanations
- Broken Markdown formatting
- Whether comparisons to alternative tools (Zapier, Make, Windmill, Temporal, Airflow) are still accurate and fairly stated
- Whether a Decision Framework was actually included wherever real alternatives exist (see "Compare Alternatives, Always" below) — this is not optional in this volume the way it was optional in Volume 4

If improvements are required: update the chapter FIRST. Do not rewrite unnecessarily. Only improve quality.

### Step 2 — Review Course Index

Review `COURSE_INDEX.md`. If a better learning order exists, update it. Only make changes when there is a clear educational improvement.

### Step 3 — Research Before Writing

Before drafting a single word of the new chapter, run a dedicated research pass covering every fast-moving fact this chapter will need (see "Information Accuracy" below for the specific list). Use WebSearch/WebFetch against current official n8n documentation (`docs.n8n.io`), the current n8n GitHub repository state (`github.com/n8n-io/n8n`), current LangChain/MCP documentation where relevant, and current named security advisories — never write a specific node name, version number, pricing figure, or "current best practice" claim from memory alone.

If research tooling is unavailable or rate-limited: do not silently substitute training-data recall and present it as current. Record exactly what could and could not be verified (mirroring the pattern in this repository's own `ROADMAP.md` Kickoff Research Summary), and either delay the affected section or write it with an explicit, visible hedge. Never let an unverified claim reach the page looking like a confirmed fact.

**This course's own prior volume (Volume 4) caught itself citing a fabricated-looking model name that turned out to be real, and separately caught real API-ordering facts that had been mis-transcribed between chapters, during its own final review pass.** Apply the same discipline here from the start, not just at the end: verify in both directions — a surprising claim might be real, and a plausible-sounding one might be fabricated or stale.

### Step 4 — Generate ONE Chapter ONLY

Generate exactly ONE new chapter, grounded in Step 3's research. Never generate multiple chapters. Never skip chapters. Never jump ahead. The chapter must be completely finished before it is considered done.

### Step 5 — Chapter Completion Checklist

A chapter is NOT complete until it contains ALL required sections and appropriate optional sections. This checklist is intentionally identical in depth to Volume 4's — the user has explicitly confirmed they want this volume held to the same bar and the same voice.

#### Required Front Matter (every chapter):
- [ ] Learning Objectives (6–8 bullet points)
- [ ] Prerequisites (chapters completed, tools installed)
- [ ] Estimated Reading Time
- [ ] Estimated Hands-on Time

#### Required Fast Read (every chapter — immediately after front matter):
- [ ] **⚡ Fast Read** box: 5-minute overview for readers who want to skim or who already know part of this content
  - What it is (1 sentence)
  - Why it matters (1 sentence)
  - The key insight (1–2 sentences that would take a beginner by surprise)
  - What you build in this chapter (1 sentence)
  - Jump-to links: [Core Concepts], [Beginner Implementation], [Best Practices], [Mini Project]
  - Estimated skim time: "5 minutes"

Format:
```markdown
## ⚡ Fast Read

> **Skim time: 5 minutes** — Read this if you're in a hurry, returning for reference, or already familiar with part of this topic.

- **What it is:** [One sentence.]
- **Why it matters:** [One sentence.]
- **Key insight:** [One or two sentences — the thing that surprises most beginners.]
- **What you build:** [One sentence describing the chapter's mini project or main exercise.]
- **Jump to:** [Core Concepts](#core-concepts) | [First Code](#beginner-implementation) | [Best Practices](#best-practices) | [Mini Project](#mini-project)
```

#### Required Body (every chapter, in this order):
1. **Why This Topic Exists** — the engineering problem this chapter solves
2. **Real-World Analogy** — at least one analogy accessible to *both* tracks (see "Writing Style" below) — a software developer AND a technically-curious non-engineer should each find it immediately familiar
3. **Core Concepts** — every new term defined with: (1) technical definition, (2) plain English definition, (3) analogy. **Explain WHY the concept exists — the engineering problem it solves — before explaining HOW n8n implements it.** This ordering is not stylistic preference; it is this volume's central teaching discipline.
4. **Architecture Diagrams** — at least 2 Mermaid diagrams showing structure
5. **Flow Diagrams** — at least 1 Mermaid diagram showing process or sequence
6. **Beginner Implementation** — working, no-code-first example (a real n8n workflow, described precisely enough to rebuild), explained node by node
7. **Intermediate Implementation** — more realistic workflow with multiple patterns, may introduce a Code node where genuinely warranted
8. **Advanced Implementation** — production-grade patterns
9. **Production Architecture** — how this is deployed and operated in real systems
10. **Best Practices** — numbered list with concrete examples
11. **Security Considerations** — threats specific to this topic (credential exposure, webhook auth gaps, prompt injection in AI Agent workflows, excessive workflow permissions)
12. **Cost Considerations** — always compare free vs paid approaches (execution-based n8n pricing, self-hosted infrastructure cost, LLM token cost for AI-native chapters, cost at fleet/scale)
13. **Common Mistakes** — specific beginner errors with wrong/right examples
14. **Debugging Guide** — diagnostic flowchart + error reference table
15. **Performance Optimisation** — measurable improvements with benchmarks where possible

#### Required Back Matter (every chapter):
16. **Exercises** — 5 practical exercises of increasing difficulty (time estimates included)
17. **Quiz** — 10 questions with full answers
18. **Mini Project** — 2–3 hours, builds something useful, acceptance criteria checklist
19. **Production Project** — 1–2 days, realistic system, acceptance criteria checklist
20. **Key Takeaways** — 8–12 bullets, one per major insight
21. **Chapter Summary** — table: concept → key takeaway
22. **Resources** — official n8n docs, GitHub, papers, further learning
23. **Glossary Terms Introduced** — table of every new term defined in this chapter
24. **See Also** — table linking related chapters (both within Volume 5 and back to Volumes 1–4) with a reason for each
25. **Preparation for Next Chapter** — technical checklist + conceptual check + optional challenge (for Chapter 20, the Capstone, adapt this into a closing "Where This Course Goes From Here" section instead, following Volume 4 Chapter 15's precedent)

#### Compare Alternatives, Always — Upgraded from Optional in This Volume

Volume 4 treated **Technology Comparison** and **Decision Framework** as optional sections, included "when they genuinely add value." In this volume, real alternatives exist for nearly every topic — treat these as **required, not optional, whenever a genuine alternative exists**:

- **Technology Comparison** — n8n vs. the honest field of alternatives for this specific concern: Zapier/Make for non-technical simplicity, Windmill/Temporal for code-first durable execution, Airflow for batch data pipelines, or a specific competing AI provider/vector store/deployment option where relevant. Never present n8n as the only tool that exists.
- **Decision Framework** — a concrete "how do you actually choose" section, not just a feature table. The recurring decision question this course keeps coming back to: **will this be maintained by an engineer or a business user?** — but each chapter should also develop its own topic-specific decision criteria.

#### Optional sections (include when they genuinely add value):
- **Interview Questions** — 5–10 questions an Automation Engineer might face, with answers
- **Architecture Review** — review of a real, named, verifiable enterprise n8n deployment implementing this topic (only if it clears this course's citation bar — see "Information Accuracy" below)
- **Production Checklist** — pre-deployment checklist specific to this topic
- **Debug Checklist** — systematic debugging checklist for this topic
- **Hands-on Lab** — step-by-step guided lab with exact commands
- **Challenge Exercise** — harder problem for advanced readers
- **Real Client Scenario** — an Aperture Cloud scenario requiring this chapter's concepts. From Chapter 09 onward (once AI agents enter the canvas), prefer scenarios where a workflow's autonomy has real, escalating consequences — see "The Autonomy Thread" below
- **Currency Note** — when content reflects a fast-moving detail (a specific n8n node's current API, a version-specific feature, a pricing tier), explain clearly what is stable vs likely to change

### Step 6 — Verify Technical Accuracy

Before treating the chapter as done, verify it — do not just proofread it:
- **Run or validate every code/config example** — every JavaScript/Python Code node snippet must be syntactically valid; every workflow JSON export shown must be well-formed; every referenced node name must be a real, current n8n node. Fix any bug found before moving on — do not narrate a fix without applying it.
- **Re-check every fast-moving fact from Step 3's research** against what actually got written — a version number, node name, or pricing figure that drifted during drafting is a common, easy-to-miss failure mode, exactly as it was for prior volumes.
- **Confirm every internal cross-reference** (a class name, a node name, a prior chapter's concept, a Volume 1–4 concept) actually matches what that earlier chapter or volume built, not a paraphrase of it.

### Step 7 — Cross References

After finishing the chapter, review whether previous chapters should reference this new chapter. If appropriate, add "See Also" entries to previous chapters.

### Step 8 — Update COURSE_INDEX.md

Mark the new chapter as complete. Update the progress tracker (`COURSE_INDEX.md`, `README.md`, and this file's Chapter Status table).

### Step 9 — Commit and Push

Once the chapter is written and verified, commit it (chapter file + any updated index/README/reference files) with a descriptive message, and push to the remote — before starting the next chapter, not batched up across several chapters. This is a durable, standing authorization for this specific, recurring action (commit + push one completed, verified chapter) in this repository; it does not authorize any other git operation (force-push, history rewrite, branch deletion) without separately asking first.

**If no remote exists yet**, commit locally and note explicitly that a push is pending until the user adds a remote (`git remote add origin <url>`) — do not guess a repository URL.

### Step 10 — STOP

After completing all work: STOP. Do not generate the next chapter. Wait for review. Never continue automatically.

---

## The Automation-Platform Thread — n8n as the Concrete Vehicle, Concepts as the Point

This volume commits to **n8n** as its single, concrete teaching platform — the same kind of commitment Volume 2 made to MCP, not the deliberately-plural stance Volume 4 took across LangGraph and the Claude Agent SDK. n8n is genuinely current, genuinely dominant in its category (fair-code, ~196k GitHub stars, native LangChain and MCP integration as of 2026), and is explicitly what this course is about.

**Rule: teach every core automation-engineering concept framework-agnostically first**, the same way Volume 3 taught chunking and retrieval theory before naming a vector database, and Volume 4 taught the reasoning loop before naming a framework. Orchestration vs. choreography, idempotency, delivery semantics, circuit breakers, RBAC — all of these are real distributed-systems and platform-engineering concepts that exist independent of n8n. Teach the concept, THEN show it concretely in n8n.

**Rule: keep n8n honestly positioned against real alternatives, every time a genuine alternative exists.** The current, real landscape as of this volume's kickoff research:
- **Zapier** — linear, guided, most accessible for non-technical users, per-task pricing, 8,000+ integrations
- **Make** — canvas-based visual logic, more powerful branching than Zapier, 2,000+ integrations
- **Windmill** — open-source, code-first (Python/TypeScript/Go/SQL), developer-team-oriented
- **Temporal** — code-first durable execution SDK; the right choice when a business process must survive infrastructure failure over a long horizon (seconds to months)
- **Apache Airflow** — code-first DAG orchestration; the right choice for batch data pipelines at real data-engineering scale

The recurring decision heuristic worth returning to across chapters: **will this workflow be maintained by an engineer, or by a business user?** That question does more real work than a feature-count comparison.

**When in doubt about whether a paragraph is drifting into "this is just an n8n tutorial":** ask "would this paragraph still make sense if I swapped n8n for Windmill or a hand-rolled event bus?" If not, separate the transferable concept from the n8n-specific syntax explicitly.

---

## The Autonomy Thread — Continued Directly From Volume 4

This is not a new thread invented for this volume — it is the same escalating-stakes discipline Volume 4 established, continued without restarting.

**Rule: Modules 1–2 (Chapters 01–08) use low-stakes, easily-reversible example scenarios** — Aperture Cloud's internal notifications, data syncing between internal systems, reporting workflows. Worst failure mode: "produced a wrong report," not "did something irreversible."

**Rule: Module 3 onward (Chapters 09–20), once AI agents enter the canvas, workflows may have real, escalating consequences** — sending real customer communications, writing to production systems, autonomous decision-making with no human in the loop by default. This is the same threshold Volume 4 drew at its own Chapter 09, applied here at the equivalent structural point (where the AI Agent node is first introduced).

**Rule: the Capstone (Chapter 20) is explicitly "Aperture Cloud's Production Automation Platform"** — built and described generally enough that a reader can substitute their own company's automation needs with no conceptual gap, while the worked example includes at least one workflow with genuinely consequential, real-world capability, gated by an explicit human-approval step.

---

## Information Accuracy — n8n and Its AI Ecosystem Move Fast

n8n itself ships frequent releases; its AI-native features (the AI Agent node, LangChain integration, MCP support) are newer and moving faster still. Always verify current specifics before writing.

### Fast-moving content requiring web verification before writing

Before writing any section containing:
- Specific n8n version numbers, node names, and node configuration details
- n8n pricing tiers (Cloud Starter/Pro, self-hosted Business, Enterprise, Startup Program) and licensing terms (Sustainable Use License / fair-code)
- AI Agent node internals, LangChain integration specifics, Model/Memory/Chain/Vector Store node behavior
- MCP integration details (MCP Server Trigger, MCP Client Tool, n8n's native MCP server, transport protocol)
- Named security advisories/CVEs affecting n8n, and their current patched-version status
- Comparison claims about Zapier, Make, Windmill, Temporal, or Airflow's current feature set or pricing
- SDK/library versions for any AI provider integrated via n8n (OpenAI, Anthropic, Ollama, Pinecone, Qdrant, Supabase, etc.)
- Any claimed production incident, enterprise deployment story, or case study — confirm it is multi-source corroborated or an official/primary source (an official security bulletin, a named company's own engineering blog, a recognized security research outlet), not a single low-tier blog post, before citing it as fact rather than an illustrative, explicitly-labeled scenario

Use WebSearch or WebFetch to verify against current official documentation (`docs.n8n.io`), current GitHub repository state (`github.com/n8n-io/n8n` — stars, latest release, `pushed_at` date are useful freshness signals), or current named security advisories.

**If web search tooling is unavailable or rate-limited during a research pass**, do not silently fall back to training-data knowledge and present it as current. Explicitly flag which facts are unverified-for-currency in your working notes, and either delay writing the affected section until verification is possible, or write it with an explicit, visible hedge — never let an unverified claim read as a confirmed fact to the reader.

### Currency labelling

```markdown
> **Currency Note:** Information in this section was verified in mid-2026. n8n's release cadence and its AI/MCP feature set specifically change quickly — always confirm against current official documentation before making a production decision.
```

### Timeless vs fast-moving

**Timeless** — internal knowledge is reliable, rarely changes: why event-driven architecture exists and when polling is still the right choice, the theoretical shape of orchestration vs. choreography, why idempotency matters for any retryable system, the fundamental distinction between a trigger and a scheduled job, why unbounded automated loops are dangerous in the abstract, why credentials should never live inline in exportable workflow definitions, RBAC as a general access-control model.

**Fast-moving** — must verify: everything in the list above.

---

## Code Requirements

n8n is a JavaScript-native platform — this inverts Volume 4's Python-primary convention. Every coding example must include all that apply to the topic:

| Language / Platform | Include When |
|--------------------|-------------|
| **JavaScript** | Always when a Code node or expression is shown — this is n8n's native, always-available language (Cloud and self-hosted both) |
| **Python** | When a Code node example is genuinely clearer in Python, or the topic is data/AI-heavy — but always note explicitly that Code node Python execution is a **self-hosted-only** capability, not available on n8n Cloud |
| **JSON** | Whenever showing a workflow export, a node's raw configuration, or an API request/response body — n8n workflows themselves ARE JSON |
| **Docker / YAML** | Deployment, scaling, and self-hosting topics (Chapters 14–18 especially) |
| **Bash** | Docker Compose commands, CLI operations, CI/CD pipeline steps |

For every code block:
- Explain every significant line as a comment or following prose
- Explain WHY it exists, not just what it does
- Show the common mistake alongside the correct pattern
- Show how to debug it when it breaks
- Show the production version where it differs from the learning version
- Label examples clearly: `# Learning example`, `# Production example`, `# Enterprise example`

---

## Production Issues — Mandatory for Every Major Concept

Whenever a chapter introduces a major concept, include at least one realistic production issue, in the same required format Volume 4 established:

```markdown
### Production Issue: [Short descriptive title]

**Symptoms**
What the engineer observes. Log messages, error codes, user complaints, alert text.
Be specific — "the workflow misbehaved" is not a symptom.

**Root Cause**
The underlying technical reason this happened. One clear paragraph.

**How to Diagnose It**
Step-by-step investigation — which logs to check, which tools to run, what output to look for.
Include actual commands and expected output where possible.

**How to Fix It**
The specific code or configuration change. Always show before/after.

**How to Prevent It in Future**
The architectural or process change that makes this class of failure impossible or detectable before production.
```

### Standard automation-engineering production issues by topic

| Topic | Typical Production Issue |
|-------|------------------------|
| Event-driven thinking | Duplicate webhook deliveries processed twice — no idempotency key, a customer gets charged or notified twice |
| Data transformation | A malformed upstream API response silently corrupts downstream records for days before anyone notices |
| Workflow design patterns | An unrate-limited fan-out workflow takes down a partner's API |
| Reliability | A non-idempotent retry after a timeout creates duplicate side effects |
| Modular design | A 100+ node monolithic workflow becomes unmaintainable and undebuggable |
| AI-native automation | An unbounded AI Agent loop burns an API budget with no engineer watching — the same failure class as Volume 4 Ch01/11, now with no terminal to notice it in |
| MCP integration | An unauthenticated MCP Server Trigger exposes internal workflow capability to any caller |
| Deployment | A queue-mode misconfiguration silently drops executions under load |
| Scaling | Worker starvation under real traffic — executions queue for hours with no alert |
| Observability | A workflow has been failing silently for a week; nobody knew because nothing was watching |
| Governance | Credential sprawl — the same API key pasted into a dozen workflows, unrotatable without breaking all of them |
| Security | A real, named, current CVE-class vulnerability (see ROADMAP.md's kickoff research for specifics) |

---

## Writing Style

- Assume the reader completed Volumes 1–4 for the *engineering-depth* track — they know embeddings, RAG, MCP server/client engineering, and the full Volume 4 agent-engineering curriculum. **Do not assume this for the no-code/accessible core path** — see "The Dual-Track Discipline" below.
- **The Dual-Track Discipline (this volume's specific addition to the series' writing style):** every chapter's core path (Core Concepts through Beginner Implementation) must be genuinely followable by a technically-curious reader with no programming background — explain what a webhook is, what JSON is, what an API is, the first time each appears, briefly and without condescension. Deeper engineering content (custom code, self-hosting internals, scaling architecture) is clearly marked as such, typically from the Intermediate/Advanced Implementation onward, so an engineering reader can find it fast and a non-engineer reader knows where the accessible path ends for that chapter.
- Explain everything in simple English first, then introduce professional terminology.
- Every new technical term must be defined when first used.
- Use real-world analogies for every concept — chosen so they land for both tracks, not just an engineering audience.
- Avoid academic writing, passive voice, and jargon without explanation.
- Use tables for comparisons.
- Use Mermaid diagrams for architecture (at least 2 per chapter).
- Use blockquotes (`>`) for important warnings, currency notes, and callouts.
- Use code blocks for all code.
- Chapter sections must flow logically without requiring the reader to look ahead.
- Write as if a senior Automation/Platform Engineer is explaining something to a smart junior engineer *and* to a technically-curious operations person in the same room — both should leave understanding something real, even if the engineer leaves with more.

---

## Cross-Volume References

This is Volume 5. Always link back to Volumes 1–4 when relevant:

| Vol 5 Topic | Earlier Volume Connection |
|-------------|---------------------------|
| Automation Architecture (Ch 01) | Vol 4 Ch 01 — bounded reasoning loops have a direct parallel in bounded, idempotent workflow execution |
| Event-Driven Thinking (Ch 02) | Vol 4 Ch 06 — A2A's synchronous request/response contrasted against genuinely decoupled, event-driven communication |
| Data Transformation (Ch 05) | Vol 3 — chunking/preprocessing discipline, applied to workflow data instead of documents |
| Workflow Design Patterns (Ch 06) | Vol 4 Ch 05 — fallback hierarchies and topology choices have direct workflow-pattern analogues |
| Reliability and Error Recovery (Ch 07) | Vol 4 Ch 01, 03, 08 — bounded loops, circuit breakers, and TTL-expiry are the same discipline on a new surface |
| The AI Agent Node (Ch 09) | Vol 4 Ch 01–03 — the reasoning loop, tool use, and bounded autonomy, now built visually |
| Retrieval and Memory (Ch 10) | Vol 3 (RAG), Vol 4 Ch 04, 11 — memory systems and bounded agentic RAG, reused directly |
| Tool-Calling and Multi-Agent (Ch 11) | Vol 4 Ch 05, 08 — orchestration topologies and human-in-the-loop gating |
| n8n and MCP (Ch 12) | **Vol 2 (MCP Engineering)** directly — this chapter is the concrete payoff of Volume 2's entire subject; Vol 4 Ch 09's SDK+MCP pattern |
| AI Workflow Builder & Evaluation (Ch 13) | Vol 4 Ch 12 — trajectory vs. outcome evaluation, applied to visual workflows |
| Scaling (Ch 16) | Vol 4 Ch 14 — fleet-level governance, same discipline at the infrastructure layer |
| Observability (Ch 17) | Vol 4 Ch 14 — fleet-level tracing, same discipline applied to workflow executions |
| Governance and Compliance (Ch 18) | Vol 4 Ch 13 — identity, access control, and audit, applied to workflow/credential ownership |
| Security (Ch 19) | Vol 4 Ch 13, Vol 2 (MCP security), Vol 1 (AI Security) |

Volume 1 repository: https://github.com/Bschouha19/AI-Engineering-Handbook
Volume 2 repository: https://github.com/Bschouha19/MCP-Engineering
Volume 3 repository: https://github.com/Bschouha19/RAG-Deep-Dive
Volume 4 repository: https://github.com/Bschouha19/AI-Agent-Engineering

---

## Chapter Status

| # | Chapter | File | Status |
|---|---------|------|--------|
| 01 | Automation Architecture — Orchestration, Choreography, and the Trigger-Action Model | chapters/chapter-01-automation-architecture.md | ✅ Complete |
| 02 | Event-Driven Thinking and n8n's Trigger Model | chapters/chapter-02-event-driven-thinking.md | ✅ Complete |
| 03 | The n8n Data Model and Expressions | chapters/chapter-03-data-model-expressions.md | ✅ Complete |
| 04 | Connecting to the World — APIs, Webhooks, and Credentials | chapters/chapter-04-connecting-to-the-world.md | ✅ Complete |
| 05 | Data Transformation and Validation at Scale | chapters/chapter-05-data-transformation.md | ✅ Complete |
| 06 | Workflow Design Patterns | chapters/chapter-06-workflow-design-patterns.md | 🔜 Next |
| 07 | Reliability and Error Recovery | chapters/chapter-07-reliability-error-recovery.md | 🔜 |
| 08 | Modular Workflow Design and Workflows as Code | chapters/chapter-08-modular-workflow-design.md | 🔜 |
| 09 | The AI Agent Node — LangChain Inside the Canvas | chapters/chapter-09-ai-agent-node.md | 🔜 |
| 10 | Retrieval and Memory in n8n | chapters/chapter-10-retrieval-memory.md | 🔜 |
| 11 | Tool-Calling and Multi-Agent Orchestration | chapters/chapter-11-tool-calling-multi-agent.md | 🔜 |
| 12 | n8n and MCP — Bridging Visual Automation and the Agent Ecosystem | chapters/chapter-12-n8n-and-mcp.md | 🔜 |
| 13 | The AI Workflow Builder and Evaluating AI Workflows | chapters/chapter-13-ai-workflow-builder-evaluation.md | 🔜 |
| 14 | Custom Code Nodes — JavaScript and Python | chapters/chapter-14-custom-code-nodes.md | 🔜 |
| 15 | Deployment Architecture | chapters/chapter-15-deployment-architecture.md | 🔜 |
| 16 | Scaling n8n in Production | chapters/chapter-16-scaling-n8n.md | 🔜 |
| 17 | Observability — Knowing When Automation Breaks | chapters/chapter-17-observability.md | 🔜 |
| 18 | Governance and Compliance | chapters/chapter-18-governance-compliance.md | 🔜 |
| 19 | Securing n8n in Production | chapters/chapter-19-securing-n8n.md | 🔜 |
| 20 | Capstone — Aperture Cloud's Production Automation Platform | chapters/chapter-20-capstone.md | 🔜 |

---

## Repository Structure

```
n8n-AI-Workflow-Automation/
├── CLAUDE.md               ← This file. Source of truth for authoring workflow.
├── COURSE_INDEX.md         ← Public-facing course overview and progress tracker
├── ROADMAP.md               ← Kickoff research summary, future updates, known open questions
├── reference/               ← Quick-lookup reference docs (open in second tab while building)
│   ├── README.md               ← Index of all reference docs
│   ├── 01-n8n-vs-alternatives-comparison.md
│   ├── 02-trigger-types-cheat-sheet.md
│   ├── 03-expression-syntax-reference.md
│   ├── 04-mcp-integration-reference.md
│   ├── 05-workflow-design-patterns-reference.md
│   ├── 06-error-handling-retry-cheat-sheet.md
│   ├── 07-ai-node-types-reference.md
│   ├── 08-deployment-options-comparison.md
│   ├── 09-security-checklist.md
│   └── 10-scaling-performance-checklist.md
└── chapters/
    ├── chapter-01-automation-architecture.md
    ├── chapter-02-event-driven-thinking.md
    └── ...
```

### Reference docs — maintenance notes

- Reference docs are **not** chapters — they don't need all 25 sections.
- Update reference docs when a chapter reveals a correction or new detail.
- Each reference doc has a "Verified: DATE" footer — update it when corrected.
- When a fast-moving detail changes (e.g. n8n ships a breaking change to the AI Agent node, MCP support graduates out of preview), update affected reference docs in the same commit as the chapter that covers the change.
- These docs do not exist yet — write them as the corresponding chapters reveal what belongs in each, the same discipline Volume 4 followed (its own reference docs 07–10 were a known, later-filled gap — avoid repeating that gap here by keeping the reference doc for a module in sync with that module's chapters as they ship, not deferred to the end).
