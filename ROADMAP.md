# n8n Automation Engineering — Roadmap

This file tracks research passes, known open questions, and possible future additions. Every research pass records what was confirmed, from which source, and what could not be verified — following this series' established discipline (see Volume 4's `ROADMAP.md` for the pattern this file continues).

---

## Kickoff Research Summary — completed 2026-07-11

Curriculum-level research run before any chapter existed, to ground the 20-chapter structure in `COURSE_INDEX.md` in verified, current facts rather than training-data recall. This is **not** a substitute for each chapter's own dedicated Step 3 research pass — it confirms the *shape* of the course is right; exact node names, current version numbers, and current pricing must be re-verified at the moment each chapter is actually drafted, per `CLAUDE.md`.

### n8n — version, licensing, pricing

- **Current version confirmed**: n8n 2.0 shipped January 2026 with native LangChain support; latest stable observed during this research was in the `2.29.x`–`2.30.x` range (specific patch versions drift fast — re-confirm via `github.com/n8n-io/n8n/releases` at draft time, don't cite a specific patch version as "current" without a fresh check).
- **Licensing**: the Sustainable Use License — n8n's own "fair-code" term — source-available, restricts commercial resale of the source itself, but allows free internal business use, modification, and non-commercial redistribution.
- **Pricing (confirmed current, re-verify before citing in a chapter)**: Cloud Starter $20/mo, Cloud Pro $50/mo, self-hosted Business $800/mo (all annual billing), free self-hosted Community Edition (unlimited users/workflows), Enterprise custom-priced, a Startup Program at $400/mo for companies with <20 employees and <$5M funding including unlimited executions and enterprise features.
- **Execution-based pricing** (not per-task like Zapier) is a genuine architectural differentiator worth teaching explicitly in Chapter 01/15 — a 20-step workflow costs the same as a 2-step workflow.
- **GitHub**: confirmed ~196,000 stars at research time — a real, current adoption signal worth citing, re-verify the exact count before publishing.

### AI-native capabilities

- **AI Agent node**: wraps LangChain primitives (tools, memory, output parsers) directly inside the visual canvas. Confirmed current node families: **Model Nodes** (OpenAI, Anthropic, Ollama for local models), **Memory Nodes** (Window Buffer — last N messages; Summary Memory — rolling summary; external Redis/Postgres-backed memory for long-running agents), **Chain Nodes** (pre-built logic: Summarize, QA with Documents, Structured Output Parser), **Vector Store Nodes** (Pinecone, Qdrant, Supabase, specifically for RAG).
- **Tools Agent**: implements LangChain's tool-calling interface. Tools passed to an AI Agent node can themselves be n8n sub-workflows or HTTP requests — a direct, concrete parallel to Volume 4 Chapter 09's subagent-as-tool pattern, now expressed visually.
- **70+ AI nodes** confirmed as of this research pass — re-verify the exact count before citing.
- **2026 roadmap signals** (lower confidence, directional only): more prebuilt AI-task templates, faster multi-agent orchestration, better monitoring dashboards for memory/reasoning/tool execution in real time. Treat as roadmap intent, not shipped fact, until independently re-confirmed at draft time.

### MCP integration — directly relevant to Chapter 12 and to Volume 2

- **n8n ships a native instance-level MCP server**, confirmed in **Public Preview since April 2026** — lets Claude Desktop, ChatGPT, Cursor, or any MCP-compatible client build, test, and publish workflows directly inside an n8n instance. Available on Cloud, Enterprise, and self-hosted Community Edition (a specific minimum version was cited in one secondary source as v2.18.4+ — re-verify this exact version gate directly against `docs.n8n.io` before citing it in the chapter).
- **Two core nodes, confirmed current**: **MCP Server Trigger** (n8n acts as an MCP server, exposing its own tools/workflows to MCP clients) and **MCP Client Tool** (n8n consumes an external MCP server's tools as agent tools, with no per-tool wiring required — n8n introspects the external server's tool schema automatically).
- **Transport**: streamable-http confirmed as the 2026 default; older external MCP servers may still use SSE — worth a compatibility note in Chapter 12.
- **First-class MCP client support** confirmed added "late 2025" per multiple sources — re-verify exact date at draft time.

### Comparison landscape

- **Zapier**: linear/guided trigger-then-action UX, most accessible for non-technical users, 8,000+ integrations, per-task pricing (every action is a billable task, unlike n8n's per-execution model). Zapier Agents confirmed shipped in 2026 for autonomous task execution.
- **Make** (formerly Integromat): canvas-based visual interface, more sophisticated branching/conditional logic than Zapier, 2,000+ integrations. "Maia AI" and Make AI Agents confirmed shipped in 2026.
- **Windmill**: open-source, developer-team-oriented, native Python/TypeScript/Go/SQL script support — the closest "pro-code" competitor to n8n's Code node capability.
- **Temporal**: code-first durable-execution SDK (Go, Java, TypeScript, Python, .NET) — the right tool when a business process must survive infrastructure failure over a long horizon (seconds to months). Not a drag-and-drop competitor to n8n; a different category entirely.
- **Apache Airflow**: code-first DAG orchestration in Python, the de facto standard for batch data pipelines at real data-engineering scale (minutes-to-hours repeat runs, Kubernetes/Celery executors).
- **The decision heuristic that recurred across multiple independent current sources, worth treating as this course's own recurring decision question**: *will this workflow be maintained by an engineer, or a business user?*

### Custom code, deployment, and scaling

- **Code node**: JavaScript is native/default and available on both Cloud and self-hosted. **Python and arbitrary npm/pip package installation are self-hosted-only** — a real, important constraint to state explicitly, not gloss over, in Chapter 14.
- **Task runners**: confirmed enabled by default as of n8n 2.0, executing Code node JavaScript/Python in an isolated environment; external mode (`N8N_RUNNERS_MODE=external`) runs a sidecar runner container per n8n process.
- **Memory footprint of the Code node**: confirmed current, concrete, citable detail — a Code node duplicates its payload in memory (once before processing, once after), so a 100MB payload can temporarily consume ~300MB. Worth an explicit Common Mistake in Chapter 14.
- **Self-hosted deployment**: Docker Compose confirmed as n8n's own recommended path (isolates n8n + database, one-command upgrades, automatic dependency management) over bare-metal or plain Docker.
- **Queue mode / scaling**: main process pushes jobs to a Redis queue; separate worker containers pull and execute, enabling horizontal scaling by adding workers. Confirmed current capacity guidance: queue mode with 1 worker for 1,000–10,000 executions/day; add more workers and dedicated webhook processors above 10,000/day. Treat these thresholds as directional, re-verify before citing as a hard rule in Chapter 16.

### Enterprise governance

- **RBAC**: confirmed current two-tier model — Account Types at the instance level (Owner, Admin, Member) and Role Types at the project level (Project Admin, Project Editor, Project Viewer), with custom roles/granular scopes on Enterprise. Available on all plans except Community Edition.
- **Source control and environments**: Git-based, confirmed current — linking an n8n instance to a Git repository lets each instance represent an environment (dev/staging/production) via branches, with workflow diffs for comparing environments before promoting. Confirmed Business/Enterprise-only.
- **Enterprise bundle**: SOC 2 compliance, SSO/SAML/LDAP, external secrets store integration, log streaming, Git-based environments, queue-mode scaling, SLA support, invoice billing, audit logs tracking logins and workflow changes with timestamps.

### Production best practices (confirmed current, multi-source consistent)

- **n8n fails silently by default** — a workflow with no configured Error Workflow simply stops with no alert when a node fails. This is a real, current, teachable surprise worth leading Chapter 07 with, not burying.
- **Error Trigger + dedicated Error Workflow** is the confirmed current standard pattern — one workflow whose only job is receiving failures from other workflows and alerting/logging.
- **"One workflow per discrete, describable task"** confirmed cited across multiple current sources as the single most impactful modularity practice — monolithic 50+-node workflows are a named anti-pattern.
- **Credentials**: exported workflows carry any inline secrets with them — the Credentials Manager (never inline API keys/tokens) is confirmed current, non-negotiable guidance.
- **Webhooks default to no authentication** — confirmed current, real, production-relevant gotcha: fine for local testing, a real gap if shipped to production unauthenticated.

### AI Workflow Builder and evaluation

- **AI Workflow Builder**: natural-language-to-workflow generation, confirmed shipped as an npm package (`@n8n/ai-workflow-builder`) and as a beta-labeled in-product feature per n8n's own community announcement. Generates nodes/logic/configuration from a plain-English description, refinable through chat.
- **n8n Evaluations**: confirmed current feature for testing AI workflow quality — supports exact-match scoring (workflows with a defined expected output) and **LLM-as-judge scoring** (nuanced quality criteria evaluated by a separate model) — a direct, concrete parallel to Volume 4 Chapter 12's LLM-as-judge content, now applied to visual workflows. Confirmed current pattern: integrate into CI/CD so a score below threshold blocks deployment.
- **Data pinning/mocking**: confirmed current n8n feature (`docs.n8n.io/data/data-pinning`) letting a workflow be tested against fixed sample data without re-triggering the live event — belongs in Chapter 08 (Workflows as Code) as a testing practice.

### Security — real, current, named incidents

- **"Ni8mare" (CVE-2026-21858)**: confirmed current, real, maximum-severity unauthenticated remote-code-execution vulnerability affecting self-hosted n8n instances running versions prior to 1.121.0. Multi-source confirmed (Cybersecurity Dive, Talos Intelligence, Dataminr intel brief) — clears this course's citation bar as a primary Chapter 19 case study.
- **CVE-2026-25049**: confirmed current, real — authenticated users with workflow-modification permissions can craft expressions that trigger unintended system command execution on the host machine. A distinct mechanism from the RCE above (authenticated-but-overprivileged vs. fully unauthenticated) — worth presenting as two structurally different vulnerability classes, the same discipline Volume 4 applied to its own excessive-agency incidents.
- **Threat-actor abuse**: Talos Intelligence ("The n8n n8mare") documents an increase, October 2025 through March 2026, in threat actors weaponizing n8n for phishing campaigns — malware delivery and device fingerprinting. Confirmed current, real, named-source reporting.
- **One unverified, lower-confidence statistic found**: a claim that "n8n has 57 security advisories, the most among tracked agentic projects" appeared in one secondary source. Flag explicitly and re-verify against a primary advisory database (e.g., n8n's own GitHub Security Advisories page, or the National Vulnerability Database) before citing this specific number in Chapter 19 — it has the shape of a citable fact but was not independently cross-confirmed during this pass.

### Core data model (confirmed directly from `docs.n8n.io`)

- Data passed between nodes is an array of JSON objects called **items**, each wrapped as `{ json: {...}, binary: {...} }` — the `binary` key is optional and most items don't use it.
- **Expression shorthands, confirmed current**: `$json` is shorthand for `$input.item.json` (current item's JSON data); `$binary` is shorthand for `$input.item.binary`; `$input.item` accesses the current item being processed; `$input.all()` accesses every input item for the current node.
- The Code node automatically wraps data in the expected `{ json: {...} }` / array structure if a script's return value is missing it.

---

## Not Fully Resolved / Flag for Re-Verification at Draft Time

- Exact current n8n patch version — cite whatever `github.com/n8n-io/n8n/releases` shows at the moment Chapter 01 is actually drafted, not the range observed during kickoff research.
- The exact minimum self-hosted version gate for the native MCP server (v2.18.4+ was cited in one secondary source only) — re-verify directly against `docs.n8n.io` before Chapter 12.
- The "57 security advisories" statistic — re-verify against a primary advisory source before Chapter 19, or drop it if it can't be independently confirmed.
- Queue-mode capacity thresholds (1,000–10,000 executions/day → 1 worker; above that → more workers) — directional guidance from secondary sources, re-confirm against n8n's own scaling documentation before treating as a hard rule in Chapter 16.
- 2026 AI Agent Builder roadmap items (prebuilt templates, faster multi-agent orchestration, real-time monitoring dashboards) — roadmap intent only, confirm shipped status before citing as current capability.

---

## Known Open Questions

- ~~Repository not yet created on GitHub~~ — resolved 2026-07-11: remote is `git@github.com:Bschouha19/n8n-AI-Workflow-Automation.git`, kickoff commit pushed to `main`.
- ~~Volume 4's own `README.md` series table still lists Volume 5 as "🔜 Planned" with no repository link~~ — resolved 2026-07-11, updated in that repository.

## Possible Future Additions (Not Yet Scoped)

- A reference doc comparing n8n's AI Agent node against building the equivalent directly with the Claude Agent SDK (Volume 4) or LangGraph (Volume 4) — when does the visual/managed tradeoff make sense vs. hand-rolling it — once Chapters 09–13 are far enough along to know precisely what that comparison should say.
- Coverage of n8n's own hosted AI features (if n8n ships a first-party hosted model/embedding offering beyond routing to external providers) — flagged as a "watch for it" item, not yet confirmed to exist.

---

*Last updated: 2026-07-11 — Chapters 01 (Automation Architecture) and 02 (Event-Driven Thinking and n8n's Trigger Model) researched, drafted, verified, and shipped. Chapter 01's dedicated research pass (n8n v2.29.10 confirmed current; GitHub stars 196k holds up; n8n pricing is EUR-denominated and geo-priced, not the USD figure this kickoff summary cached; Zapier/Make integration counts refreshed to 9,000+/3,000+; Make switched to credit-based billing in Aug 2025; Temporal now has 7 SDKs) superseded the corresponding figures above — see chapter-01-automation-architecture.md's Technology Comparison and Cost Considerations sections for the current numbers. Chapter 02's research pass confirmed n8n's complete current core trigger taxonomy (15 core trigger nodes, now organized into six practical categories including a distinct "invocation-by-another-workflow" category for Execute Sub-workflow Trigger — see chapter-02-event-driven-thinking.md), the Airtable Trigger's Trigger Field polling/deduplication mechanism, Schedule Trigger's multi-rule support, and Error Workflow firing conditions — all directly against docs.n8n.io. Chapter 03 next.*
