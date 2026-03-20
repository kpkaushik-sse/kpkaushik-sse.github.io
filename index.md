---
layout: default
title: Home
---

# Build Real AI Agents — From First Principles to Production

**Structured, hands-on learning for the era of autonomous AI.**

LearnHub is a free, self-paced platform for engineers who want to go beyond prompting and actually build agentic AI systems — systems that reason, plan, use tools, and complete complex tasks autonomously.

[Start the Agentic AI course &rarr;](/courses/agentic-ai-engineering/)

---

## What You Will Learn

| Phase                   | Topics                                                  | Duration    |
| ----------------------- | ------------------------------------------------------- | ----------- |
| **1 — Foundations**     | Agentic concepts, ReAct, ReWOO, design patterns, ethics | Weeks 1–3   |
| **2 — Core Frameworks** | LangChain, LCEL, LangGraph, Agentic RAG, LlamaIndex     | Weeks 4–7   |
| **3 — Advanced Agents** | Phidata, CrewAI, multi-agent systems, Autogen           | Weeks 8–10  |
| **4 — Ops & Cloud**     | AgentOps, Langfuse, Langsmith, Langflow, AWS/Azure/GCP  | Weeks 11–12 |

[View the full 12-week plan &rarr;](/courses/agentic-ai-engineering/)

---

## Key Concepts Covered

- **AI Agents** — autonomous loops of perception, reasoning, and action
- **ReAct pattern** — interleaving reasoning traces with tool calls
- **LangGraph** — stateful, graph-based agent orchestration with persistent memory
- **Agentic RAG** — retrieval pipelines driven by an agent, not a static chain
- **Multi-agent systems** — specialized agents collaborating via CrewAI and Autogen
- **Observability** — tracing and evaluating agent runs with Langfuse and Langsmith
- **Cloud deployment** — running agents on AWS Bedrock, Azure OpenAI, and GCP Vertex AI

---

## Latest Posts

{% for post in site.posts limit:5 %}

- **[{{ post.title }}]({{ post.url | relative_url }})** — <small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% endfor %}

[All posts &rarr;](/blog/)

---

## How It Works

1. **Follow the 12-week plan** — modules are sequenced so each one builds on the last.
2. **Do the labs** — 20+ hands-on projects, not just theory.
3. **Build your capstone** — a multi-agent RAG system with observability, deployed to cloud.
4. **Explore the blog** — deeper dives, concept explainers, and framework comparisons.

---

[About LearnHub &rarr;](/about/)
