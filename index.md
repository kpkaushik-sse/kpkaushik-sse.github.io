---
layout: default
title: Home
---

# Build Autonomous AI Agents — From Fundamentals to Deployment

**Structured, project-driven learning for the age of autonomous AI.**

LearnHub is a free, self-paced platform for engineers who want to move beyond simple prompting and actually construct AI agent systems — systems that reason, plan, invoke tools, and accomplish complex tasks on their own.

[Start the Autonomous AI track &rarr;](/courses/agentic-ai-engineering/)

---

## What You Will Learn

| Track                          | Topics                                                      | Duration    |
| ------------------------------ | ----------------------------------------------------------- | ----------- |
| **A — Groundwork**             | Agent concepts, ReAct loops, reasoning strategies, ethics   | Weeks 1–3   |
| **B — Orchestration Toolkits** | LangChain, LCEL, LangGraph, retrieval pipelines, LlamaIndex | Weeks 4–7   |
| **C — Collaborative Agents**   | Phidata, CrewAI, agent teams, Autogen                       | Weeks 8–10  |
| **D — Production & Cloud**     | Telemetry, Langfuse, Langsmith, Langflow, AWS/Azure/GCP     | Weeks 11–12 |

[View the full 12-week track &rarr;](/courses/agentic-ai-engineering/)

---

## Core Topics

- **AI Agents** — autonomous loops of perception, reasoning, and action
- **ReAct pattern** — interleaving reasoning traces with tool invocations
- **LangGraph** — graph-based agent orchestration with persistent state
- **Retrieval-augmented agents** — agent-driven retrieval pipelines, not static chains
- **Agent teams** — specialized agents collaborating via CrewAI and Autogen
- **Telemetry** — tracing and evaluating agent runs with Langfuse and Langsmith
- **Cloud deployment** — running agents on AWS Bedrock, Azure OpenAI, and GCP Vertex AI

---

## Latest Posts

{% for post in site.posts limit:5 %}

- **[{{ post.title }}]({{ post.url | relative_url }})** — <small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% endfor %}

[All posts &rarr;](/blog/)

---

## How It Works

1. **Follow the 12-week track** — units are sequenced so each builds on the last.
2. **Complete the projects** — 20+ practice exercises, not just theory.
3. **Build your capstone** — a coordinated agent pipeline with retrieval, tracing, and cloud deployment.
4. **Read the blog** — deeper explorations, concept breakdowns, and framework comparisons.

---

[About LearnHub &rarr;](/about/)
