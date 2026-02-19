# PicoHive

## The AI-Native Operating System for Startups

---

### The Problem

Every early-stage company dies from the same thing: they need expensive humans to build product before they know whether the product is worth building. The human capital cost problem forces founders to raise money to hire people to figure out if they need more money to hire more people.

**PicoHive breaks this loop.**

---

### The Vision

PicoHive is a multi-tenant platform that lets founders deploy specialized AI agents — a developer, a product manager, a growth lead, a sales rep — that behave like persistent employees with names, memories, budgets, and escalation protocols. They coordinate through an orchestrator, execute real work through tools and integrations, and produce tangible artifacts: code pushed to GitHub, emails sent, slides built, sites deployed.

This is not a chatbot with memory. This is an operating system for running a company with AI employees.

---

### Core Philosophy

> **Agents are employees, not sessions.** They persist across time, accumulate memory, and have careers.

> **The orchestrator is the CEO, not a router.** It holds strategy, delegates with context, and owns outcomes.

> **Everything is logged immutably.** Every action, decision, and token spent creates a learning signal.

> **Security by isolation.** Agents never hold API keys. A proxy layer mediates all external calls.

> **Budget is a first-class primitive.** Token spend, tool calls, and time are metered and gated.

> **Self-improvement is systematic.** Agent performance compounds over time through structured feedback loops.

---

### The Architecture

PicoHive is structured as a layered system where each layer has a single responsibility and communicates through well-defined interfaces:

```
┌─────────────────────────────────────────────────────────────┐
│  CLIENT LAYER                                               │
│  Web Dashboard · Mobile (Telegram) · API Access             │
├─────────────────────────────────────────────────────────────┤
│  PRODUCT LAYER                                              │
│  Auth & Multi-Tenancy · Billing · Artifact Viewer · Approval│
├─────────────────────────────────────────────────────────────┤
│  ORCHESTRATOR                                               │
│  Task Graph Engine · Delegation Protocol · Heartbeat (30s)  │
├─────────────────────────────────────────────────────────────┤
│  AGENT RUNTIME                                              │
│  Soul + Identity Files · Think → Plan → Act · Handoffs      │
├─────────────────────────────────────────────────────────────┤
│  MEMORY LAYER                                               │
│  Core · Working · Episodic · Semantic (Vector)              │
├─────────────────────────────────────────────────────────────┤
│  TOOL LAYER                                                 │
│  Browser · Shell · GitHub · Email · Calendar · Deploy       │
├─────────────────────────────────────────────────────────────┤
│  INFRASTRUCTURE                                             │
│  BullMQ Queues · Supabase · Redis · S3 · Key Proxy          │
└─────────────────────────────────────────────────────────────┘
```

---

### How It Works

**1. Set a Goal**

A founder sets a goal. The Global Context Engine persists this as the northstar — the mission, ICP, and current sprint objective that every agent knows.

**2. Orchestrator Decomposes**

The Orchestrator's heartbeat picks up the goal, decomposes it into a task graph, and delegates tasks to specialized agents via the queue system.

**3. Agents Execute**

Each agent receives a task with full context (company DNA, its own memory, team capabilities), thinks, plans, and acts through tools.

**4. Artifacts Emerge**

Real work is produced: code committed, emails sent, sites deployed. Artifacts are surfaced to the founder in real-time.

**5. The System Learns**

Every action feeds back into memory. Agents improve. The company's HIVE instance becomes uniquely tailored and harder to replace.

---

### The Agent Model

Every agent in PicoHive is built on three foundational concepts:

#### Soul File (`soul.md`)
The behavioral constitution — what the agent can do, how it thinks, and what is outside its scope. This is not a system prompt that gets overwritten; it's the permanent base layer of every interaction.

#### Identity File (`identity.md`)
Who the agent is as an entity: name, personality, how it behaves under pressure, what it cares about. This creates agents that feel like people, not functions.

#### The Execution Loop
```
Think → Plan → Act
```
On every task: read full context, build situational understanding, decompose into steps, select tools, execute sequentially, emit results.

---

### Memory Architecture

What separates a persistent agent from a stateless API call:

| Tier | Purpose | Storage |
|------|---------|---------|
| **Core Memory** | Always in context. Agent identity, company DNA, current priorities. | Postgres |
| **Working Memory** | Task-scoped. Loaded on pickup, cleared on completion. | Redis (TTL) |
| **Episodic Memory** | Session and task history. What was asked, what was done, what happened. | Postgres |
| **Semantic Memory** | Domain knowledge and learned facts. Retrieved via similarity search. | pgvector |

Memory compaction runs nightly — raw episodes become summaries, summaries feed back into core memory as learned lessons.

---

### Security Model

Agents are powerful: they browse the web, send emails, push code, deploy servers. Security is structural, not additive.

**Key Proxy Service**: Agents never hold API keys. All external calls go through a proxy that validates permissions, logs actions, and returns only results.

**Multi-Tenant Isolation**: Every query is scoped to `organization_id`. Row-level security in the database. Middleware enforcement, not convention.

**Approval Gates**: High-stakes actions (spending above threshold, external communications, production deploys) require human sign-off.

**Immutable Audit Trail**: Every action — every agent decision, every tool call, every approval — is logged permanently.

---

### Budget Engine

Budget is a first-class primitive. Every token spent, every tool call made, is metered and attributed.

- **Org Pool**: Total tokens + dollar budget for billing period
- **Agent Allocation**: Per-agent slice, dynamically adjusted by Orchestrator
- **Task Budget**: Per-task estimate, hard cap prevents runaway tasks
- **Milestones**: Defined checkpoints with token rewards for achievement

When agents hit milestones, the org earns more runway. Productive agents are rewarded with greater operational latitude.

---

### Self-Improvement Loops

Agents that improve systematically are compounding assets.

**Feedback Ingestion**: Explicit user ratings, implicit signals (completion rate, retry frequency), and outcome signals (did the email get replies? did the code pass tests?).

**Confidence Scoring**: Per-agent, per-domain performance tracking. High-confidence tasks go direct; low-confidence gets oversight.

**Soul File Evolution**: The system proposes updates based on learnings. Humans approve. Agents get better at their jobs over time.

---

### Build Roadmap

| Phase | Focus | Timeline |
|-------|-------|----------|
| **Phase 1** | Foundation & Single Agent | Weeks 1–4 |
| **Phase 2** | Orchestrator & Multi-Agent | Weeks 5–9 |
| **Phase 3** | Memory & Self-Improvement | Weeks 10–14 |
| **Phase 4** | Full Tool Suite & MCP | Weeks 15–19 |
| **Phase 5** | Mobile & Growth Features | Weeks 20–24 |
| **Phase 6** | Scale & Enterprise | Weeks 25+ |

---

### The Core Technical Contract

An agent must be able to:

1. **Remember** what it has done across sessions
2. **Receive** delegated tasks and hand off tasks outside its scope
3. **Execute** real-world actions through tools
4. **Produce** persistent artifacts
5. **Operate** within a defined budget
6. **Improve** its own performance over time from feedback

Every architectural decision serves one of these six requirements.

---

### Why This Matters

The companies that win will deploy capability, not headcount.

PicoHive is not about replacing humans — it's about giving founders the leverage to build before they hire, to test before they commit, to scale intelligence instead of scaling headcount.

This is the AI-native operating system for the next generation of companies.

---

<p align="center">
  <strong>PicoHive</strong><br>
  <em>AI-Native Operating System</em><br><br>
  Version 1.0 · February 2026
</p>