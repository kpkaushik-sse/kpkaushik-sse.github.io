---
layout: post
title: "M1 — Agentic AI Essentials"
date: 2026-03-21
categories: [agentic-ai, foundations]
permalink: /blog/2026/03/21/m1-agentic-ai-essentials/
description: "What makes an AI system 'agentic'? This module covers the core concepts, vocabulary, design philosophy, and ethics of autonomous AI agents."
---

**Module 1 · Phase 1: Foundations · Week 1 · ~8 hrs · 2 labs**

---

## What You Will Learn

By the end of this module you will be able to:

- Define what an AI agent is and explain how it differs from a standard LLM call
- Describe the four foundational agentic design patterns
- Recognise real-world agentic use cases and evaluate their feasibility
- Explain the key ethical risks of autonomous AI systems and the mitigations used in practice

---

## 1. What Is an AI Agent?

A **large language model (LLM)** on its own takes input and produces output in one step. An **AI agent** wraps an LLM in a loop that lets it:

1. **Observe** — receive a goal or updated state from the environment
2. **Think** — reason about what to do next
3. **Act** — call a tool, write to memory, or produce an output
4. **Repeat** — feed the result back and continue until the goal is reached

```
┌─────────────────────────────────────────┐
│              Agent Loop                 │
│                                         │
│  Goal ──► Reason ──► Act ──► Observe   │
│              ▲                  │       │
│              └──────────────────┘       │
└─────────────────────────────────────────┘
```

This loop — often called the **Sense → Think → Act** cycle — is what makes a system _agentic_ rather than just generative.

### Key distinctions

|              | LLM (single call) | AI Agent                         |
| ------------ | ----------------- | -------------------------------- |
| **Turns**    | One               | Many (loop)                      |
| **Memory**   | None (stateless)  | Short-term & long-term           |
| **Tools**    | None              | Web search, code exec, APIs, DBs |
| **Goal**     | Answer a question | Complete a multi-step task       |
| **Autonomy** | Zero              | Partial → Full                   |

---

## 2. Core Vocabulary

You will see these terms throughout every module — get them solid now.

| Term             | Definition                                                                    |
| ---------------- | ----------------------------------------------------------------------------- |
| **LLM**          | The reasoning engine inside an agent (e.g. GPT-4o, Claude 3, Gemini)          |
| **Agent**        | An autonomous system that uses an LLM to reason and act in a loop             |
| **Tool**         | Any external function an agent can call (search, calculator, code runner, DB) |
| **Action**       | The result of a reasoning step — calling a tool or producing a final answer   |
| **Observation**  | The output returned to the agent after an action                              |
| **Memory**       | Context the agent can read/write — in-context (short) or vector store (long)  |
| **Orchestrator** | The code/framework that runs the agent loop (LangGraph, CrewAI, Autogen…)     |
| **Environment**  | Everything external to the agent that it can observe and affect               |

---

## 3. The Four Foundational Design Patterns

Andrew Ng's framing of agentic design patterns is the best mental model to start with. Memorise these — they reappear in every framework you will use.

### Pattern 1 — Reflection

The agent reviews and critiques its own output before returning it to the user.

```
Generate output
     │
     ▼
Critique output   ◄──┐
     │               │
     ▼               │
Good enough? ──No────┘
     │
    Yes
     ▼
Return to user
```

> **Example:** An agent writes a Python function, then re-reads it to check for bugs and style issues before returning it.

---

### Pattern 2 — Tool Use

The agent can call external tools to get information it does not have in its weights.

```
User goal
    │
    ▼
Plan which tools to call
    │
    ▼
Call tool(s) → Get observation
    │
    ▼
Reason over results → Final answer
```

> **Example:** "What is the weather in London?" → agent calls a weather API → reads the JSON → answers the user.

---

### Pattern 3 — Planning

The agent decomposes a complex goal into a series of sub-tasks and executes them in order (or in parallel).

```
Complex goal
      │
      ▼
Decompose into sub-tasks
  [T1] [T2] [T3]
      │
      ▼
Execute each sub-task
      │
      ▼
Synthesise final result
```

> **Example:** "Write a competitive analysis report" → agent breaks this into: search competitors, summarise each, compare features, draft report.

---

### Pattern 4 — Multi-Agent Collaboration

Multiple specialised agents work together, each owning a part of the task. An orchestrator agent coordinates them.

```
Orchestrator Agent
   ├── Research Agent  →  gathers information
   ├── Writer Agent    →  drafts content
   └── Critic Agent    →  reviews and scores
```

> **Example:** A code-generation system where one agent writes code, a second runs tests, and a third suggests fixes.

---

## 4. Real-World Agentic Use Cases

### High-value applications today

| Domain                   | Agent task                                       | Tools used                                 |
| ------------------------ | ------------------------------------------------ | ------------------------------------------ |
| **Software engineering** | Write, test, and debug code autonomously         | Code executor, file system, GitHub API     |
| **Research & analysis**  | Gather, synthesise, and summarise sources        | Web search, PDF reader, vector DB          |
| **Customer support**     | Resolve tickets end-to-end without human         | CRM API, knowledge base, email tool        |
| **Data analysis**        | Clean, analyse, and visualise data from a prompt | Python REPL, SQL, charting libraries       |
| **Finance**              | Monitor markets, generate and explain signals    | Market data API, calculator, report writer |
| **DevOps**               | Investigate incidents, propose and apply fixes   | Log search, shell, alerting API            |

### Lab 1 — Analyse Use Cases

Pick **two** use cases from the table above. For each one, write a one-page analysis covering:

1. What is the goal the agent is trying to achieve?
2. What tools would it need?
3. What could go wrong? (hallucination, tool failure, runaway actions)
4. How would you limit the blast radius if the agent makes a mistake?

---

## 5. Ethics & Safety of Autonomous Agents

Agentic systems introduce risks that do not exist with single LLM calls. Because the agent acts in the world — calling APIs, writing files, sending emails — mistakes can have real consequences.

### Key risks

| Risk                        | Description                                                              | Mitigation                                     |
| --------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------- |
| **Hallucinated tool calls** | Agent invents an API or parameters                                       | Strict tool schemas, output validation         |
| **Goal mis-specification**  | Agent achieves the stated goal but not the intended one                  | Clear, constrained goal definitions            |
| **Prompt injection**        | Malicious content in tool output hijacks the agent                       | Sanitise observations, use system-level guards |
| **Runaway actions**         | Agent takes far more (or more destructive) actions than expected         | Human-in-the-loop checkpoints, action budgets  |
| **Data leakage**            | Agent sends private data to external tools                               | Tool-level permission scoping, audit logs      |
| **Bias amplification**      | Agent applies biased reasoning across many autonomous decisions at scale | Diverse eval sets, red-teaming                 |

### Responsible agent design principles

- **Minimal footprint** — request only the permissions the task actually needs
- **Prefer reversible actions** — delete → trash, not permanent delete
- **Human-in-the-loop** — for consequential actions, require explicit approval
- **Audit trail** — log every action and observation for post-hoc review
- **Fail safe** — when uncertain, stop and ask rather than guess

### Lab 2 — Ethics Audit

Take one of the use cases from Lab 1. Map out:

1. Every tool the agent would need and what that tool has access to
2. At least three things that could go wrong
3. A safeguard for each risk

---

## 6. The Agentic AI Landscape — Tools Overview

You do not need to know these deeply yet — you will build with each one in later modules. This is your map.

| Layer                        | Tools                                                          |
| ---------------------------- | -------------------------------------------------------------- |
| **LLMs (reasoning engines)** | OpenAI GPT-4o, Anthropic Claude 3, Google Gemini, Mistral      |
| **Agent frameworks**         | LangChain, LangGraph, LlamaIndex, CrewAI, Autogen, Phidata     |
| **Memory / Vector stores**   | Chroma, Pinecone, Weaviate, pgvector                           |
| **Tool integrations**        | Tavily (web search), E2B (code sandbox), Browserbase (browser) |
| **Observability**            | Langsmith, Langfuse                                            |
| **No/low-code**              | Langflow, Relevance AI, Wordware                               |
| **Cloud**                    | AWS Bedrock, Azure OpenAI, GCP Vertex AI                       |

---

## 7. Module Summary

| Concept    | What to remember                                         |
| ---------- | -------------------------------------------------------- |
| Agent loop | Observe → Think → Act → repeat                           |
| vs LLM     | Agents are stateful, tool-using, multi-turn              |
| 4 patterns | Reflection, Tool Use, Planning, Multi-Agent              |
| Ethics     | Minimal footprint, reversible actions, HITL, audit trail |

---

## Check Your Understanding

Before moving to M2, you should be able to answer:

1. What is the difference between a chatbot and an AI agent?
2. Name and describe the four agentic design patterns.
3. What is prompt injection in an agentic context and how do you defend against it?
4. What does "minimal footprint" mean and why does it matter?

---

[← Back to Agentic AI Engineering course](/courses/agentic-ai-engineering/)
