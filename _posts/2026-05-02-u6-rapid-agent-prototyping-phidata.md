---
layout: default
title: "Unit 6 — Rapid Agent Prototyping with Phidata"
date: 2026-05-02
categories: [agentic-ai, specialized-agents]
permalink: /blog/2026/05/02/u6-rapid-agent-prototyping-phidata/
description: "Build production-ready AI agents in minutes with Phidata — structured outputs, built-in tools, vector knowledge bases, session memory, and a real-time monitoring dashboard."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 6</span>
</nav>

<div class="mod-hero">
  <h1>Unit 6 — Rapid Agent Prototyping with Phidata</h1>
  <p class="mod-hero-sub">LangChain and LangGraph give you full control — but that control comes with boilerplate. Phidata takes the opposite approach: opinionated defaults, batteries-included tools, and production features out of the box. In this unit you'll go from zero to a deployed agent in under 50 lines of code.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Module C · Collaborative & Specialized Agents</span>
    <span class="mod-pill time">⏱ ~8 hrs across 5 days (Week 8)</span>
    <span class="mod-pill hands">🛠 1 hands-on project</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/04/25/u5-retrieval-augmented-agent-pipelines/" style="color:var(--gum);">Unit 5 — RAG Pipelines</a>. You'll use vector knowledge bases extensively in Phidata, and understanding RAG fundamentals makes the setup intuitive.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Create a Phidata Agent with an LLM, tools, and structured output in under 10 lines</li>
    <li>Use built-in tool kits: web search (DuckDuckGo), finance (YFinance), file I/O, and shell commands</li>
    <li>Attach a vector knowledge base (PgVector, Qdrant, LanceDB) for RAG directly on the agent</li>
    <li>Add session memory with PostgreSQL so agents remember conversations across restarts</li>
    <li>Enforce structured output using Pydantic response models</li>
    <li>Build an agent team where a lead agent delegates to specialist sub-agents</li>
    <li>Deploy the agent as a FastAPI web app with Phidata's built-in playground UI</li>
    <li>Monitor agent runs using Phidata's dashboard: traces, token usage, and tool call logs</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">Phidata Agent Framework</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Knowledge Bases & Memory</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Agent Teams & Deployment</span>
</div>

<div class="day-tabs" role="tablist">
  <button class="day-tab active" onclick="switchDay(1)" role="tab">Day 1</button>
  <button class="day-tab" onclick="switchDay(2)" role="tab">Day 2</button>
  <button class="day-tab" onclick="switchDay(3)" role="tab">Day 3</button>
  <button class="day-tab" onclick="switchDay(4)" role="tab">Day 4</button>
  <button class="day-tab" onclick="switchDay(5)" role="tab">Day 5</button>
</div>

<!-- DAY 1 -->
<div id="day1" class="day-panel active">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>Phidata fundamentals — your first agent in 10 lines</h4><p>Two topics · ~1.5 hours · Cover: Why Phidata + Agent basics with tools</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>Why Phidata — The Fastest Path to a Working Agent</h2><span class="topic-time">30 min</span></div>
<div class="topic-body">
<p>You've spent four units building agents from scratch with LangChain and LangGraph. You understand the internals: prompts, parsers, state graphs, conditional edges, checkpointers. Now imagine a framework that wraps all of that into a single class: <code>Agent</code>. That's Phidata.</p>
<p>Phidata is an opinionated framework designed for one thing: getting agents to production as fast as possible. It trades flexibility for speed — you don't design the state graph, you declare what the agent should do, and Phidata handles the ReAct loop, tool execution, memory, and even deployment.</p>

<h3>Phidata vs. LangChain — when to use which</h3>
<table class="cmp-table">
  <thead><tr><th>Aspect</th><th>LangChain/LangGraph</th><th>Phidata</th></tr></thead>
  <tbody>
    <tr><td><strong>Philosophy</strong></td><td>Composable primitives — build anything</td><td>Opinionated defaults — get to production fast</td></tr>
    <tr><td><strong>Agent setup</strong></td><td>Define state, nodes, edges, compile graph</td><td>Instantiate Agent() with model, tools, instructions</td></tr>
    <tr><td><strong>Tool creation</strong></td><td>@tool decorator + manual wiring</td><td>Built-in tool kits (DuckDuckGo, YFinance, etc)</td></tr>
    <tr><td><strong>Memory</strong></td><td>Checkpointer + thread_id + manual config</td><td>session_id parameter, auto-stored in PostgreSQL</td></tr>
    <tr><td><strong>Knowledge</strong></td><td>Build RAG pipeline manually</td><td>Pass knowledge_base parameter to Agent()</td></tr>
    <tr><td><strong>Deployment</strong></td><td>You build the FastAPI/Flask app</td><td>Built-in serve() with playground UI</td></tr>
    <tr><td><strong>Best for</strong></td><td>Custom workflows, complex routing, multi-agent orchestration</td><td>Quick prototypes, standard agent patterns, demos</td></tr>
  </tbody>
</table>

<div class="insight-box"><strong>Not either/or:</strong> Many production systems use Phidata for rapid prototyping and initial deployment, then migrate critical agents to LangGraph when they need custom workflows. Knowing both is a superpower.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Install Phidata: <code>pip install phidata openai</code></li>
  <li>Read the Phidata docs overview page and note the three core concepts: Agent, Tool, Knowledge.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>Your First Phidata Agent — 10 Lines to ReAct</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>Here's the minimum viable agent — a web-searching assistant in 10 lines:</p>

<div class="arch-diagram">
  <div class="title">PHIDATA — HELLO WORLD AGENT</div>
  <div><span class="purple">from</span> phi.agent <span class="purple">import</span> Agent</div>
  <div><span class="purple">from</span> phi.model.openai <span class="purple">import</span> OpenAIChat</div>
  <div><span class="purple">from</span> phi.tools.duckduckgo <span class="purple">import</span> DuckDuckGo</div>
  <div></div>
  <div>agent = Agent(</div>
  <div>    model=OpenAIChat(id=<span class="green">"gpt-4o-mini"</span>),</div>
  <div>    tools=[DuckDuckGo()],</div>
  <div>    instructions=[<span class="green">"Always cite your sources with URLs."</span>],</div>
  <div>    show_tool_calls=<span class="yellow">True</span>,</div>
  <div>    markdown=<span class="yellow">True</span>,</div>
  <div>)</div>
  <div></div>
  <div>agent.print_response(<span class="green">"What are the latest AI agent frameworks released in 2026?"</span>)</div>
</div>

<p>That's it. The agent runs a full ReAct loop internally: it reads the query, decides to search the web, parses the results, and generates a cited response. No state schema, no graph, no conditional edges — Phidata handles all of that.</p>

<h3>Built-in tool kits</h3>
<div class="blocks-grid">
  <div class="block-card"><h4>🔍 DuckDuckGo</h4><p>Web search + news search. No API key needed. Returns titles, URLs, and snippets.</p></div>
  <div class="block-card"><h4>📈 YFinance</h4><p>Stock prices, company info, analyst recommendations, historical data. Free.</p></div>
  <div class="block-card"><h4>📁 FileTools</h4><p>Read, write, and list files on the local filesystem. Use with caution in production.</p></div>
  <div class="block-card"><h4>🐍 PythonTools</h4><p>Execute arbitrary Python code. The agent can write and run code to solve problems.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">FINANCE AGENT — STRUCTURED OUTPUT</div>
  <div><span class="purple">from</span> phi.agent <span class="purple">import</span> Agent</div>
  <div><span class="purple">from</span> phi.model.openai <span class="purple">import</span> OpenAIChat</div>
  <div><span class="purple">from</span> phi.tools.yfinance <span class="purple">import</span> YFinanceTools</div>
  <div><span class="purple">from</span> pydantic <span class="purple">import</span> BaseModel</div>
  <div></div>
  <div><span class="blue">class</span> <span class="yellow">StockReport</span>(BaseModel):</div>
  <div>    ticker: str</div>
  <div>    price: float</div>
  <div>    recommendation: str</div>
  <div>    reasoning: str</div>
  <div></div>
  <div>agent = Agent(</div>
  <div>    model=OpenAIChat(id=<span class="green">"gpt-4o-mini"</span>),</div>
  <div>    tools=[YFinanceTools(stock_price=<span class="yellow">True</span>, analyst_recommendations=<span class="yellow">True</span>)],</div>
  <div>    <span class="highlight">response_model=StockReport</span>,  <span class="dim"># enforces structured output</span></div>
  <div>)</div>
  <div></div>
  <div>result = agent.run(<span class="green">"Analyse NVDA stock"</span>)</div>
  <div>print(result.content)  <span class="dim"># → StockReport(ticker="NVDA", price=...)</span></div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build the web-searching agent and ask it 3 different questions. Observe the tool calls in the output.</li>
  <li>Build the finance agent with structured output. Analyse 3 different stocks.</li>
  <li>Create a custom Pydantic model for a weather report and build an agent that returns structured weather data.</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Knowledge bases & memory — RAG and persistence the Phidata way</h4><p>Two topics · ~1.5 hours · Cover: Vector knowledge bases + Session memory</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Vector Knowledge Bases</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>In Unit 5 you built RAG pipelines manually: load → chunk → embed → store → retrieve → generate. In Phidata, you pass a <code>knowledge_base</code> parameter to the Agent and it handles the entire pipeline. The agent automatically searches the knowledge base before responding.</p>

<div class="arch-diagram">
  <div class="title">PHIDATA RAG — KNOWLEDGE BASE</div>
  <div><span class="purple">from</span> phi.agent <span class="purple">import</span> Agent</div>
  <div><span class="purple">from</span> phi.knowledge.pdf <span class="purple">import</span> PDFKnowledgeBase</div>
  <div><span class="purple">from</span> phi.vectordb.lancedb <span class="purple">import</span> LanceDb</div>
  <div></div>
  <div><span class="dim"># Create a knowledge base from PDF files</span></div>
  <div>kb = PDFKnowledgeBase(</div>
  <div>    path=<span class="green">"./company_docs"</span>,</div>
  <div>    vector_db=LanceDb(table_name=<span class="green">"company_kb"</span>, uri=<span class="green">"./lancedb"</span>),</div>
  <div>)</div>
  <div></div>
  <div>agent = Agent(</div>
  <div>    knowledge=kb,</div>
  <div>    search_knowledge=<span class="yellow">True</span>,  <span class="dim"># always search before answering</span></div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># First run: load and index the PDFs</span></div>
  <div>agent.knowledge.load(recreate=<span class="yellow">False</span>)</div>
  <div></div>
  <div>agent.print_response(<span class="green">"What is our refund policy?"</span>)</div>
</div>

<h3>Supported knowledge sources</h3>
<table class="cmp-table">
  <thead><tr><th>Source</th><th>Class</th><th>Use Case</th></tr></thead>
  <tbody>
    <tr><td><strong>PDF files</strong></td><td>PDFKnowledgeBase</td><td>Company documents, reports, manuals</td></tr>
    <tr><td><strong>URLs</strong></td><td>WebsiteKnowledgeBase</td><td>Documentation sites, help centres</td></tr>
    <tr><td><strong>Text files</strong></td><td>TextKnowledgeBase</td><td>Plain text, markdown, code files</td></tr>
    <tr><td><strong>JSON</strong></td><td>JSONKnowledgeBase</td><td>API responses, structured data exports</td></tr>
    <tr><td><strong>Combined</strong></td><td>CombinedKnowledgeBase</td><td>Mix multiple sources into one searchable index</td></tr>
  </tbody>
</table>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Create a PDFKnowledgeBase from 2–3 documents. Load it and verify the chunks are indexed.</li>
  <li>Ask the agent a question only the documents can answer. Verify it retrieves and cites the correct source.</li>
  <li>Use CombinedKnowledgeBase to merge PDFs and a website into a single searchable index.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">4</div><h2>Session Memory — Agents That Remember</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>By default, each <code>agent.run()</code> call is stateless. For multi-turn conversations, Phidata provides session-based memory backed by a database. Each session_id gets its own conversation history, persisted across restarts.</p>

<div class="arch-diagram">
  <div class="title">SESSION MEMORY WITH POSTGRESQL</div>
  <div><span class="purple">from</span> phi.agent <span class="purple">import</span> Agent</div>
  <div><span class="purple">from</span> phi.storage.agent.postgres <span class="purple">import</span> PgAgentStorage</div>
  <div></div>
  <div>agent = Agent(</div>
  <div>    storage=PgAgentStorage(</div>
  <div>        table_name=<span class="green">"agent_sessions"</span>,</div>
  <div>        db_url=<span class="green">"postgresql://user:pass@localhost:5432/agents"</span>,</div>
  <div>    ),</div>
  <div>    add_history_to_messages=<span class="yellow">True</span>,</div>
  <div>    num_history_responses=<span class="yellow">5</span>,  <span class="dim"># include last 5 turns</span></div>
  <div>    session_id=<span class="green">"user-123-session-abc"</span>,</div>
  <div>)</div>
  <div></div>
  <div>agent.print_response(<span class="green">"My name is Kaushik."</span>)</div>
  <div>agent.print_response(<span class="green">"What's my name?"</span>)  <span class="dim"># → "Your name is Kaushik."</span></div>
</div>

<div class="insight-box"><strong>Memory strategies:</strong> <code>num_history_responses=5</code> includes the last 5 exchanges in context. For long conversations, use Phidata's built-in summarisation: <code>create_user_memories=True</code> extracts key facts (name, preferences) from the conversation into a durable memory store, similar to how ChatGPT remembers user preferences.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Set up memory with SQLite (for simplicity): <code>SqlAgentStorage</code>. Have a 5-turn conversation and verify the agent remembers earlier turns.</li>
  <li>Kill the Python process, restart it with the same session_id, and verify the conversation resumes.</li>
  <li>Enable <code>create_user_memories=True</code> and observe what facts the agent extracts and stores.</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>Agent teams — lead agent delegates to specialists</h4><p>One topic · ~1.5 hours · Cover: Multi-agent teams with Phidata</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">5</div><h2>Agent Teams — Delegation & Specialisation</h2><span class="topic-time">75 min</span></div>
<div class="topic-body">
<p>A single agent can't be great at everything. Want financial analysis AND web research AND code execution? Instead of one overloaded agent, build a <strong>team</strong>: a lead agent that understands the request and delegates to specialist sub-agents.</p>

<div class="arch-diagram">
  <div class="title">AGENT TEAM ARCHITECTURE</div>
  <div><span class="green">User Query</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  <span class="dim">▼</span></div>
  <div><span class="highlight">Lead Agent</span> <span class="dim">— understands intent, decides which specialist to call</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  <span class="dim">├──▶</span> <span class="blue">Research Agent</span> <span class="dim">(DuckDuckGo, web scraping)</span></div>
  <div>  <span class="dim">├──▶</span> <span class="purple">Finance Agent</span> <span class="dim">(YFinance, stock analysis)</span></div>
  <div>  <span class="dim">└──▶</span> <span class="orange">Code Agent</span> <span class="dim">(PythonTools, data processing)</span></div>
  <div></div>
  <div><span class="dim">Each specialist has its own tools, instructions, and output format.</span></div>
  <div><span class="dim">The lead synthesises specialist outputs into a coherent response.</span></div>
</div>

<div class="arch-diagram">
  <div class="title">PHIDATA AGENT TEAM</div>
  <div><span class="purple">from</span> phi.agent <span class="purple">import</span> Agent</div>
  <div></div>
  <div><span class="dim"># Specialist agents</span></div>
  <div>researcher = Agent(</div>
  <div>    name=<span class="green">"Researcher"</span>,</div>
  <div>    role=<span class="green">"Search the web for information"</span>,</div>
  <div>    tools=[DuckDuckGo()],</div>
  <div>)</div>
  <div></div>
  <div>analyst = Agent(</div>
  <div>    name=<span class="green">"Analyst"</span>,</div>
  <div>    role=<span class="green">"Analyse financial data and stocks"</span>,</div>
  <div>    tools=[YFinanceTools(stock_price=<span class="yellow">True</span>, analyst_recommendations=<span class="yellow">True</span>)],</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># Lead agent — delegates to specialists</span></div>
  <div>team = Agent(</div>
  <div>    <span class="highlight">team=[researcher, analyst]</span>,</div>
  <div>    instructions=[<span class="green">"Delegate research to the Researcher. Delegate finance to the Analyst."</span>],</div>
  <div>    show_tool_calls=<span class="yellow">True</span>,</div>
  <div>)</div>
  <div></div>
  <div>team.print_response(<span class="green">"What's the latest news about NVDA and its current stock price?"</span>)</div>
</div>

<div class="insight-box"><strong>When to use teams vs. a single agent:</strong> Use a single agent when one set of tools covers the entire task. Use teams when (a) different tasks need different expertise, (b) you want to isolate tool access (the researcher can't access finance tools), or (c) you want specialists to have different model configurations (cheaper model for research, smarter model for analysis).</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build a three-agent team: researcher (web search), analyst (finance), coder (Python execution).</li>
  <li>Ask a question that requires two specialists: "What's AAPL's current P/E ratio and how does it compare to the industry average?" The analyst should get the P/E; the researcher should find industry averages.</li>
  <li>Give each specialist a different model: researcher uses gpt-4o-mini (cheap), analyst uses gpt-4o (precise). Observe cost differences.</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Deployment & monitoring — serve your agent as a web app</h4><p>Two topics · ~1.5 hours · Cover: FastAPI deployment + Phidata monitoring dashboard</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">6</div><h2>Deploying Agents with Phidata Playground</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">
<p>Phidata includes a built-in web playground and a <code>serve()</code> function that wraps your agent in a FastAPI application with a chat UI. This means you can go from a Python script to a shareable web app with one function call.</p>

<div class="arch-diagram">
  <div class="title">SERVE YOUR AGENT</div>
  <div><span class="purple">from</span> phi.playground <span class="purple">import</span> Playground, serve_playground_app</div>
  <div></div>
  <div>app = Playground(agents=[agent]).get_app()</div>
  <div></div>
  <div><span class="dim"># Run with: uvicorn app:app --reload</span></div>
  <div><span class="dim"># Opens a chat UI at localhost:7777</span></div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Serve your finance agent as a playground app. Open the UI in a browser and have a conversation.</li>
  <li>Add session memory so conversations persist across page reloads.</li>
  <li>Deploy to a cloud VM (or Docker) and share the URL with a colleague for testing.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">7</div><h2>Monitoring — Traces, Tokens & Tool Logs</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>Phidata provides a monitoring dashboard (phidata.app) that captures every agent run: prompts sent to the LLM, tool calls made, tokens consumed, latency per step, and errors. This is similar to LangSmith but integrated directly into the Phidata ecosystem.</p>

<div class="blocks-grid">
  <div class="block-card"><h4>📊 Run traces</h4><p>See the full execution flow: user message → LLM call → tool call → tool response → LLM call → final response. Click any step to see the full payload.</p></div>
  <div class="block-card"><h4>💰 Token tracking</h4><p>Input tokens, output tokens, total cost per run. Aggregated per agent, per session, and per day.</p></div>
  <div class="block-card"><h4>🔧 Tool call logs</h4><p>Every tool invocation: which tool, what arguments, what it returned, how long it took. Essential for debugging tool failures.</p></div>
  <div class="block-card"><h4>⚠️ Error tracking</h4><p>Exceptions, API timeouts, rate limits. Grouped by type with stack traces. Set up alerts for critical errors.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">ENABLE MONITORING</div>
  <div>agent = Agent(</div>
  <div>    model=OpenAIChat(id=<span class="green">"gpt-4o-mini"</span>),</div>
  <div>    tools=[DuckDuckGo()],</div>
  <div>    <span class="highlight">monitoring=True</span>,  <span class="dim"># sends traces to phidata.app</span></div>
  <div>)</div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Enable monitoring on your agent and run 5 queries.</li>
  <li>Open phidata.app and inspect the traces. Find the most expensive run and the fastest run.</li>
  <li>Identify which tool call took the longest. How would you optimise it?</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Project — Automated Insights Dashboard</h4><p>One project · ~2.5 hours · Combine all Phidata concepts</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">P</div><h2>Project — Automated Insights Dashboard</h2><span class="topic-time">2.5 hrs</span></div>
<div class="topic-body">
<p>Build an agent-powered dashboard that takes a company name, fetches real-time stock data and news, searches your internal knowledge base for company notes, and produces a structured insights report — all via an agent team served through the Phidata playground.</p>

<div class="lab-box"><h4>✏️ Phase 1 — Agent Specialists (40 min)</h4><ol>
  <li>Create a finance_agent with YFinanceTools (stock price, financials, analyst recommendations).</li>
  <li>Create a news_agent with DuckDuckGo (latest news, press releases).</li>
  <li>Create a knowledge_agent with a PDFKnowledgeBase containing sample company reports.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 2 — Team & Structured Output (40 min)</h4><ol>
  <li>Create a lead agent that delegates to all three specialists.</li>
  <li>Define a Pydantic <code>InsightReport</code> model: company, ticker, current_price, price_change_30d, key_news (list), internal_notes (list), recommendation, reasoning.</li>
  <li>Set <code>response_model=InsightReport</code> on the lead agent.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 3 — Memory & Deployment (40 min)</h4><ol>
  <li>Add session memory so users can ask follow-up questions ("What about MSFT?").</li>
  <li>Serve the team via Phidata Playground with a chat UI.</li>
  <li>Enable monitoring and run 10 queries. Review the traces on phidata.app.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 4 — Polish (30 min)</h4><ol>
  <li>Add error handling: what if YFinance returns no data for a private company?</li>
  <li>Test with 5 different companies (public and private). Verify graceful fallback.</li>
  <li>Export a cost report: total tokens and estimated cost across all 10 queries.</li>
</ol></div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 6 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Phidata philosophy</strong> — opinionated defaults, batteries-included, fast to production</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agent class</strong> — model, tools, instructions, response_model in one constructor</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Built-in tools</strong> — DuckDuckGo, YFinance, PythonTools, FileTools</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Knowledge bases</strong> — PDF, web, text, JSON with automatic RAG pipeline</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Session memory</strong> — PostgreSQL/SQLite, num_history_responses, user memories</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Structured output</strong> — response_model with Pydantic for typed agent responses</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agent teams</strong> — lead agent delegates to specialists</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Deployment</strong> — Playground UI, FastAPI, serve() function</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Monitoring</strong> — traces, token tracking, tool logs on phidata.app</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Phidata vs. LangChain</strong> — speed vs. flexibility trade-off</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>When would you choose Phidata over LangGraph? When would LangGraph be the better choice?</li>
  <li>Explain how Phidata's knowledge_base parameter differs from building a RAG pipeline manually with LangChain.</li>
  <li>Design an agent team for a travel booking application. What specialists would you create?</li>
  <li>How does session memory in Phidata compare to LangGraph's checkpointer approach?</li>
  <li>You need to deploy an agent that handles 100 concurrent users. What infrastructure would you set up?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/04/25/u5-retrieval-augmented-agent-pipelines/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 5</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/09/u7-coordinated-agent-teams-crewai/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 7 →</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
