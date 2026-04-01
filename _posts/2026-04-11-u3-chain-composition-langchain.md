---
layout: default
title: "Unit 3 — Chain Composition with LangChain"
date: 2026-04-11
categories: [agentic-ai, orchestration]
permalink: /blog/2026/04/11/u3-chain-composition-langchain/
description: "Master LangChain and LCEL — build composable chains, connect LLMs to tools, manage prompt templates, parse structured outputs, and create your first autonomous agent."
---

<style>
/* ───────────────────────────────────────────────
   MODULE PAGE — LMS-style interactive layout
   ─────────────────────────────────────────────── */
.mod-page { max-width: 820px; margin: 0 auto; padding: 0 0 48px; }

/* ── Breadcrumb ── */
.mod-breadcrumb { display: flex; align-items: center; gap: 6px; font-size: 13px; color: var(--gray-500); margin-bottom: 20px; }
.mod-breadcrumb a { color: var(--gum); text-decoration: none; }
.mod-breadcrumb a:hover { color: var(--earth); }

/* ── Hero ── */
.mod-hero { margin-bottom: 32px; }
.mod-hero h1 { font-size: 32px; font-weight: 700; line-height: 1.2; margin-bottom: 8px; border: none; }
.mod-hero-sub { font-size: 16px; color: var(--gray-500); line-height: 1.6; margin-bottom: 16px; }
.mod-hero-meta { display: flex; flex-wrap: wrap; gap: 12px; }
.mod-pill { display: inline-flex; align-items: center; gap: 5px; padding: 4px 12px; border-radius: 20px; font-size: 12px; font-weight: 500; }
.mod-pill.track   { background: rgba(84,100,20,0.1);  color: var(--gum); }
.mod-pill.time    { background: rgba(172,100,46,0.1);  color: var(--earth); }
.mod-pill.hands   { background: rgba(224,248,46,0.15); color: var(--gum-dark); }

/* ── Objectives card ── */
.obj-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-md); padding: 20px 24px; margin-bottom: 32px; }
.obj-card h3 { font-size: 15px; font-weight: 600; margin-bottom: 10px; border: none; display: flex; align-items: center; gap: 6px; }
.obj-card ul { list-style: none; padding: 0; }
.obj-card li { position: relative; padding-left: 22px; margin-bottom: 6px; font-size: 14px; line-height: 1.6; }
.obj-card li::before { content: "✓"; position: absolute; left: 0; color: var(--gum); font-weight: 700; }

/* ── Day tabs ── */
.day-tabs { display: flex; gap: 4px; margin-bottom: 0; border-bottom: 2px solid var(--gray-200); overflow-x: auto; }
.day-tab { padding: 10px 20px; font-size: 14px; font-weight: 500; cursor: pointer; border: none; background: none; color: var(--gray-500); border-bottom: 2px solid transparent; margin-bottom: -2px; transition: all var(--transition); white-space: nowrap; }
.day-tab:hover { color: var(--gray-700); }
.day-tab.active { color: var(--gum); border-bottom-color: var(--gum); }
.day-panel { display: none; padding-top: 24px; }
.day-panel.active { display: block; }

/* ── Topic section ── */
.topic-section { margin-bottom: 36px; }
.topic-header { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
.topic-num { width: 36px; height: 36px; border-radius: 50%; background: var(--gum); color: var(--white); display: flex; align-items: center; justify-content: center; font-size: 15px; font-weight: 700; flex-shrink: 0; }
.topic-header h2 { font-size: 22px; font-weight: 600; margin: 0; border: none; padding: 0; }
.topic-time { font-size: 12px; color: var(--gray-500); margin-left: auto; white-space: nowrap; background: var(--gray-100); padding: 3px 10px; border-radius: 12px; }

.topic-body { padding-left: 48px; }
.topic-body p { margin-bottom: 14px; font-size: 15px; line-height: 1.8; }
.topic-body h3 { font-size: 17px; font-weight: 600; margin: 24px 0 10px; border: none; padding: 0; }

/* ── Insight box ── */
.insight-box { background: linear-gradient(135deg, rgba(84,100,20,0.06), rgba(235,252,211,0.4)); border-left: 3px solid var(--gum); border-radius: 0 var(--radius-sm) var(--radius-sm) 0; padding: 14px 18px; margin: 16px 0; font-size: 14px; line-height: 1.7; }
.insight-box strong { color: var(--gum-dark); }

/* ── Building blocks / module grid ── */
.blocks-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; margin: 16px 0; }
@media (max-width: 560px) { .blocks-grid { grid-template-columns: 1fr; } }
.block-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-sm); padding: 14px 16px; }
.block-card h4 { font-size: 14px; font-weight: 600; margin-bottom: 4px; display: flex; align-items: center; gap: 6px; }
.block-card p { font-size: 13px; color: var(--gray-700); line-height: 1.55; margin: 0; }

/* ── Three-column module grid ── */
.blocks-grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin: 16px 0; }
@media (max-width: 640px) { .blocks-grid-3 { grid-template-columns: 1fr; } }

/* ── Comparison table ── */
.cmp-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 13.5px; }
.cmp-table th { text-align: left; padding: 10px 12px; background: var(--gray-100); font-weight: 600; font-size: 12px; text-transform: uppercase; letter-spacing: 0.4px; }
.cmp-table td { padding: 10px 12px; border-bottom: 1px solid var(--gray-200); }
.cmp-table tr:last-child td { border-bottom: none; }
.cmp-table tr:hover td { background: rgba(84,100,20,0.03); }

/* ── Themed framework table ── */
.fw-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 13.5px; }
.fw-table th { text-align: left; padding: 10px 12px; background: var(--gum); color: var(--white); font-weight: 600; font-size: 12px; text-transform: uppercase; letter-spacing: 0.4px; }
.fw-table td { padding: 10px 12px; border-bottom: 1px solid var(--gray-200); }

/* ── Pattern cards ── */
.pattern-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-md); padding: 20px 22px; margin-bottom: 16px; }
.pattern-card h4 { font-size: 17px; font-weight: 600; margin-bottom: 6px; display: flex; align-items: center; gap: 8px; }
.pattern-card .pattern-tag { display: inline-block; font-size: 10px; font-weight: 600; padding: 2px 8px; border-radius: 12px; text-transform: uppercase; letter-spacing: 0.5px; }
.pattern-card p { font-size: 14px; color: var(--gray-700); line-height: 1.7; margin-bottom: 10px; }

/* ── Step-flow cards (dark) ── */
.step-flow { display: flex; flex-direction: column; gap: 12px; margin: 20px 0; }
.step-card { background: var(--gray-900); border-radius: var(--radius-md); padding: 20px 22px; color: var(--white); display: flex; gap: 16px; }
.step-num { width: 38px; height: 38px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 16px; font-weight: 700; flex-shrink: 0; }
.step-num.perceive { background: #6366f1; color: white; }
.step-num.plan     { background: #8b5cf6; color: white; }
.step-num.act      { background: var(--gum); color: white; }
.step-num.learn    { background: var(--earth); color: white; }
.step-body { flex: 1; }
.step-label { font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 2px; }
.step-label.perceive { color: #a5b4fc; }
.step-label.plan     { color: #c4b5fd; }
.step-label.act      { color: #d9f99d; }
.step-label.learn    { color: #fed7aa; }
.step-title { font-size: 17px; font-weight: 600; margin-bottom: 6px; }
.step-desc { font-size: 13.5px; line-height: 1.65; color: #d1d5db; }
.step-tools { display: flex; gap: 8px; margin-top: 10px; flex-wrap: wrap; }
.tool-badge { padding: 4px 10px; border-radius: 4px; font-size: 11px; font-weight: 600; }
.tool-badge.green { background: rgba(16,185,129,0.2); color: #6ee7b7; }
.tool-badge.red   { background: rgba(239,68,68,0.2);  color: #fca5a5; }
.tool-badge.blue  { background: rgba(96,165,250,0.2); color: #93c5fd; }
.tool-badge.amber { background: rgba(245,158,11,0.2); color: #fcd34d; }
.tool-badge.purple { background: rgba(139,92,246,0.2); color: #c4b5fd; }

/* ── Schedule cards ── */
.sched-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-md); padding: 16px 20px; margin-bottom: 12px; display: flex; gap: 14px; align-items: flex-start; }
.sched-time { font-size: 12px; font-weight: 600; color: var(--gum); white-space: nowrap; min-width: 90px; padding-top: 2px; }
.sched-body h4 { font-size: 15px; font-weight: 600; margin-bottom: 4px; }
.sched-body p { font-size: 13px; color: var(--gray-700); line-height: 1.5; margin: 0; }

/* ── Lab box ── */
.lab-box { background: linear-gradient(135deg, rgba(172,100,46,0.06), rgba(172,100,46,0.02)); border: 1px solid rgba(172,100,46,0.2); border-radius: var(--radius-md); padding: 20px 22px; margin: 20px 0; }
.lab-box h4 { font-size: 15px; font-weight: 600; color: var(--earth); margin-bottom: 8px; display: flex; align-items: center; gap: 6px; }
.lab-box ol, .lab-box ul { padding-left: 20px; }
.lab-box li { font-size: 14px; line-height: 1.7; margin-bottom: 4px; }

/* ── Day progress bar ── */
.day-progress { background: var(--gray-200); border-radius: 6px; height: 6px; margin-bottom: 20px; overflow: hidden; }
.day-progress-fill { height: 100%; background: var(--gum); border-radius: 6px; transition: width 0.4s ease; }

/* ── Section divider ── */
.section-divider { border: none; height: 1px; background: var(--gray-200); margin: 36px 0; }

/* ── Summary checklist ── */
.summary-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin: 16px 0; }
@media (max-width: 560px) { .summary-grid { grid-template-columns: 1fr; } }
.summary-item { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-sm); padding: 12px 14px; font-size: 13.5px; display: flex; align-items: flex-start; gap: 8px; }
.summary-check { color: var(--gum); font-weight: 700; flex-shrink: 0; }

/* ── Comparison cards ── */
.compare-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; margin: 20px 0; }
.compare-card { border-radius: var(--radius-md); padding: 18px; border: 1px solid var(--gray-200); background: var(--white); }
.compare-card.highlight { border-color: var(--gum); box-shadow: 0 0 0 1px var(--gum); }
.compare-card h4 { font-size: 14px; margin-bottom: 8px; font-weight: 600; }
.compare-card p { font-size: 13px; color: var(--gray-700); line-height: 1.6; }

/* ── Architecture diagram (dark terminal) ── */
.arch-diagram { background: var(--gray-900); color: var(--white); border-radius: var(--radius-md); padding: 24px; margin: 16px 0; font-family: 'Fira Code', monospace; font-size: 13px; line-height: 1.8; overflow-x: auto; }
.arch-diagram .title { color: #a5b4fc; font-weight: 600; margin-bottom: 8px; }
.arch-diagram .dim { color: #64748b; }
.arch-diagram .green { color: #6ee7b7; }
.arch-diagram .blue { color: #93c5fd; }
.arch-diagram .purple { color: #c4b5fd; }
.arch-diagram .yellow { color: #fcd34d; }
.arch-diagram .red { color: #fca5a5; }
.arch-diagram .orange { color: #fdba74; }
.arch-diagram .highlight { color: #E0F82E; font-weight: 600; }

/* ── Pattern loop diagram ── */
.loop-box { background: var(--gray-900); color: var(--white); border-radius: var(--radius-md); padding: 20px 24px; margin: 16px 0; font-family: 'Fira Code', monospace; font-size: 13px; line-height: 1.8; text-align: center; }

/* ── Responsive ── */
@media (max-width: 768px) {
  .mod-hero h1 { font-size: 24px; }
  .topic-body { padding-left: 0; }
  .step-card { flex-direction: column; gap: 10px; }
  .sched-card { flex-direction: column; gap: 6px; }
  .sched-time { min-width: auto; }
}
</style>

<div class="mod-page">

<!-- Breadcrumb -->
<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 3</span>
</nav>

<!-- Hero -->
<div class="mod-hero">
  <h1>Unit 3 — Chain Composition with LangChain</h1>
  <p class="mod-hero-sub">Time to write real code. LangChain is the most popular orchestration framework for building LLM-powered applications. In this unit you'll go from zero to building composable chains, connecting tools, parsing structured outputs, and creating your first autonomous agent — all with the LangChain Expression Language (LCEL).</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track B · Orchestration Toolkits</span>
    <span class="mod-pill time">⏱ ~9 hrs across 5 days (Week 4)</span>
    <span class="mod-pill hands">🛠 1 hands-on project</span>
  </div>
</div>

<!-- Prerequisites -->
<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/03/28/u2-agentic-ai-architecture-design-patterns/" style="color: var(--gum);">Unit 2 — Agent Blueprints & Reasoning Strategies</a> first. You'll need a solid understanding of agent architecture types, the six framework modules, and the five design patterns (especially ReAct and Tool Use) to follow along.
</div>

<!-- Objectives -->
<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Install LangChain and navigate its modular ecosystem (core, community, openai, langsmith)</li>
    <li>Wrap any LLM (OpenAI, Anthropic, Ollama) with a unified interface and swap providers without changing code</li>
    <li>Author reusable prompt templates with dynamic variables, few-shot examples, and message placeholders</li>
    <li>Parse LLM output into structured data using StrOutputParser, JsonOutputParser, and PydanticOutputParser</li>
    <li>Compose multi-step pipelines using LCEL's pipe operator, RunnablePassthrough, RunnableLambda, and RunnableParallel</li>
    <li>Add conversational memory to chains with ConversationBufferMemory, SummaryMemory, and RunnableWithMessageHistory</li>
    <li>Build custom tools with the @tool decorator and wire them into a ReAct agent via create_react_agent</li>
    <li>Debug and trace chains with LangSmith, callbacks, verbose mode, and token-level cost estimation</li>
  </ul>
</div>

<!-- Skills badge -->
<div style="display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 28px;">
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(84,100,20,0.1); color: var(--gum);">LangChain & LCEL Fundamentals</span>
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(172,100,46,0.1); color: var(--earth);">Prompt Engineering & Output Parsing</span>
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(224,248,46,0.15); color: var(--gum-dark);">Building Tool-Using Agents</span>
</div>

<!-- ═══════════════════════════════════════════════
     DAY TABS
     ═══════════════════════════════════════════════ -->
<div class="day-tabs" role="tablist">
  <button class="day-tab active" onclick="switchDay(1)" role="tab">Day 1</button>
  <button class="day-tab" onclick="switchDay(2)" role="tab">Day 2</button>
  <button class="day-tab" onclick="switchDay(3)" role="tab">Day 3</button>
  <button class="day-tab" onclick="switchDay(4)" role="tab">Day 4</button>
  <button class="day-tab" onclick="switchDay(5)" role="tab">Day 5</button>
</div>

<!-- ═══════════════════════════════════════════════
     DAY 1 — LangChain Fundamentals
     ═══════════════════════════════════════════════ -->
<div id="day1" class="day-panel active">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d1prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 1 overview</div>
  <div class="sched-body">
    <h4>Get up and running — install LangChain, run your first chain</h4>
    <p>Two topics · ~2 hours · Cover: Why LangChain exists + LLM wrappers & chat models</p>
  </div>
</div>

<!-- ── TOPIC 1 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">1</div>
    <h2>What Is LangChain & Why It Exists</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>In Unit 2 you designed agent architectures on paper — perception modules, cognitive loops, tool registries. Now imagine building all of that from scratch for every project: writing HTTP clients for each LLM provider, managing conversation history, parsing tool calls, handling retries. That's months of boilerplate. <strong>LangChain eliminates that boilerplate.</strong></p>

    <p>LangChain is an open-source Python (and JavaScript) framework that provides standardised abstractions for every building block in an LLM application: models, prompts, output parsers, memory, tools, agents, and chains. Instead of writing one-off integration code for OpenAI, Anthropic, Ollama, or Google, you write against LangChain's unified interface — and swap providers with a single line change.</p>

    <p>Think of LangChain as the <strong>SQLAlchemy of LLM applications</strong>. SQLAlchemy doesn't replace PostgreSQL or MySQL — it gives you a consistent API so your application code doesn't break when you change databases. LangChain does the same for language models, vector stores, and retrieval systems.</p>

    <div class="insight-box">
      <strong>Why not just use the OpenAI SDK directly?</strong> You can — and for simple one-shot calls, the raw SDK is fine. But the moment you need prompt templates, output parsing, memory, tool calling, retries, streaming, or multi-step chains, you'll end up reinventing what LangChain already provides. The framework shines when you compose multiple steps together.
    </div>

    <h3>The LangChain ecosystem</h3>
    <p>LangChain isn't a single monolithic package. It's split into focused modules so you install only what you need:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>📦 langchain-core</h4>
        <p>The foundation. Contains base abstractions: Runnable protocol, prompt templates, output parsers, chat message types. Always installed. No provider-specific code.</p>
      </div>
      <div class="block-card">
        <h4>🔌 langchain-openai</h4>
        <p>OpenAI-specific wrappers: ChatOpenAI, OpenAIEmbeddings. Handles API authentication, streaming, function calling, structured outputs.</p>
      </div>
      <div class="block-card">
        <h4>🌐 langchain-community</h4>
        <p>Third-party integrations maintained by the community: Ollama, HuggingFace, Wikipedia, Tavily, various vector stores. Install per-integration.</p>
      </div>
      <div class="block-card">
        <h4>🔍 langsmith</h4>
        <p>Observability platform. Traces every LLM call, tool invocation, and chain step. Shows latency, token usage, cost. Essential for debugging production chains.</p>
      </div>
    </div>

    <div class="arch-diagram">
      <div class="title">LANGCHAIN ECOSYSTEM MAP</div>
      <div><span class="yellow">┌──────────────────────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="highlight">YOUR APPLICATION CODE</span>                              <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬──────────────────────────────────────┘</span></div>
      <div><span class="dim">                │  uses</span></div>
      <div><span class="yellow">┌───────────────▼──────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="blue">langchain</span>  <span class="dim">— chains, agents, retrieval strategies</span>    <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬──────────────────────────────────────┘</span></div>
      <div><span class="dim">                │  built on</span></div>
      <div><span class="yellow">┌───────────────▼──────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="green">langchain-core</span>  <span class="dim">— Runnable, prompts, parsers, messages</span><span class="yellow">│</span></div>
      <div><span class="yellow">└───────┬──────────────────┬────────────────────────────┘</span></div>
      <div><span class="dim">        │                  │</span></div>
      <div><span class="dim">   ┌────▼──────────┐  ┌────▼──────────────┐</span></div>
      <div><span class="dim">   │</span><span class="purple">langchain-openai</span><span class="dim">│  │</span><span class="orange">langchain-community</span><span class="dim">│</span></div>
      <div><span class="dim">   │</span><span class="purple"> ChatOpenAI     </span><span class="dim">│  │</span><span class="orange"> Ollama, Tavily,   </span><span class="dim">│</span></div>
      <div><span class="dim">   │</span><span class="purple"> Embeddings     </span><span class="dim">│  │</span><span class="orange"> Wikipedia, FAISS  </span><span class="dim">│</span></div>
      <div><span class="dim">   └───────────────┘  └───────────────────┘</span></div>
      <div style="margin-top:8px;"><span class="dim">Observability:</span> <span class="red">LangSmith</span> <span class="dim">— traces, evals, cost tracking</span></div>
    </div>

    <h3>Installation and first "Hello World" chain</h3>
    <p>Let's get LangChain installed and run your very first chain. This takes under 5 minutes:</p>

    <div class="arch-diagram">
      <div class="title">INSTALLATION</div>
      <div><span class="green">$</span> <span class="dim">pip install langchain langchain-openai langchain-community</span></div>
      <div><span class="green">$</span> <span class="dim">pip install python-dotenv  # for API key management</span></div>
      <div style="margin-top:12px;"><span class="title">FIRST CHAIN — hello_langchain.py</span></div>
      <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> ChatOpenAI</div>
      <div><span class="purple">from</span> langchain_core.prompts <span class="purple">import</span> ChatPromptTemplate</div>
      <div><span class="purple">from</span> langchain_core.output_parsers <span class="purple">import</span> StrOutputParser</div>
      <div></div>
      <div><span class="dim"># 1. Model — wraps the OpenAI API</span></div>
      <div>model = ChatOpenAI(model=<span class="green">"gpt-4o-mini"</span>, temperature=<span class="yellow">0</span>)</div>
      <div></div>
      <div><span class="dim"># 2. Prompt — defines the template</span></div>
      <div>prompt = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"You are a helpful coding tutor."</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"Explain {concept} in one paragraph."</span>),</div>
      <div>])</div>
      <div></div>
      <div><span class="dim"># 3. Chain — pipe operator composes the steps</span></div>
      <div>chain = prompt <span class="highlight">|</span> model <span class="highlight">|</span> StrOutputParser()</div>
      <div></div>
      <div><span class="dim"># 4. Invoke — run the chain</span></div>
      <div>result = chain.invoke({<span class="green">"concept"</span>: <span class="green">"recursion"</span>})</div>
      <div>print(result)</div>
    </div>

    <p>That's it — three components piped together with <code>|</code>. The prompt formats the message, the model generates the response, and the parser extracts the string. This pipe syntax is called <strong>LCEL</strong> (LangChain Expression Language), and it's the core composability model you'll use throughout this unit.</p>

    <div class="insight-box">
      <strong>Security note:</strong> Never hardcode API keys. Use environment variables (<code>OPENAI_API_KEY</code>) or a <code>.env</code> file with <code>python-dotenv</code>. LangChain automatically reads from environment variables — you don't need to pass the key explicitly.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Set up a new Python virtual environment and install the three LangChain packages</li>
        <li>Create <code>hello_langchain.py</code> from the code above and run it</li>
        <li>Change the concept to "Big-O notation" and verify the output changes</li>
        <li>Add a second variable to the prompt: <code>"Explain {concept} to a {audience}."</code> and invoke with <code>{"concept": "recursion", "audience": "five-year-old"}</code></li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 2 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">2</div>
    <h2>LLM Wrappers & Chat Models</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>LangChain's model wrappers solve a critical problem: every LLM provider has a different API format, different authentication, different parameter names, and different response shapes. Without a wrapper, switching from OpenAI to Anthropic means rewriting every API call in your codebase.</p>

    <p>With LangChain, you instantiate a model object once — <code>ChatOpenAI</code>, <code>ChatAnthropic</code>, <code>ChatOllama</code> — and the rest of your chain code stays identical. The Runnable protocol guarantees that every model exposes the same methods: <code>invoke()</code>, <code>batch()</code>, <code>stream()</code>, and <code>ainvoke()</code>.</p>

    <h3>ChatOpenAI — the most common wrapper</h3>
    <p>This wraps OpenAI's chat completion API. Here are the key parameters you need to understand:</p>

    <table class="cmp-table">
      <thead><tr><th>Parameter</th><th>What It Does</th><th>Default</th><th>When to Change</th></tr></thead>
      <tbody>
        <tr><td><strong>model</strong></td><td>Which model to call (gpt-4o, gpt-4o-mini, etc.)</td><td>gpt-3.5-turbo</td><td>Always set this explicitly</td></tr>
        <tr><td><strong>temperature</strong></td><td>Randomness (0 = deterministic, 1 = creative)</td><td>0.7</td><td>Use 0 for structured tasks, 0.7-1.0 for creative</td></tr>
        <tr><td><strong>max_tokens</strong></td><td>Maximum length of the response</td><td>None (model default)</td><td>Set to control cost and prevent runaway generation</td></tr>
        <tr><td><strong>top_p</strong></td><td>Nucleus sampling — alternative to temperature</td><td>1</td><td>Rarely. Use temperature OR top_p, not both</td></tr>
        <tr><td><strong>streaming</strong></td><td>Stream tokens as they're generated</td><td>False</td><td>Set True for real-time UIs (chatbots, demos)</td></tr>
      </tbody>
    </table>

    <h3>Model switching — swap providers without changing code</h3>
    <p>This is LangChain's killer feature for production systems. Your chain code stays exactly the same — only the model instantiation changes:</p>

    <div class="arch-diagram">
      <div class="title">SWAP PROVIDERS IN ONE LINE</div>
      <div><span class="dim"># Option A: OpenAI (cloud, paid)</span></div>
      <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> ChatOpenAI</div>
      <div>model = ChatOpenAI(model=<span class="green">"gpt-4o-mini"</span>, temperature=<span class="yellow">0</span>)</div>
      <div></div>
      <div><span class="dim"># Option B: Anthropic (cloud, paid)</span></div>
      <div><span class="purple">from</span> langchain_anthropic <span class="purple">import</span> ChatAnthropic</div>
      <div>model = ChatAnthropic(model=<span class="green">"claude-sonnet-4-20250514"</span>, temperature=<span class="yellow">0</span>)</div>
      <div></div>
      <div><span class="dim"># Option C: Ollama (local, free)</span></div>
      <div><span class="purple">from</span> langchain_community.chat_models <span class="purple">import</span> ChatOllama</div>
      <div>model = ChatOllama(model=<span class="green">"llama3"</span>, temperature=<span class="yellow">0</span>)</div>
      <div></div>
      <div><span class="dim"># The rest of your chain is IDENTICAL regardless of provider:</span></div>
      <div>chain = prompt <span class="highlight">|</span> model <span class="highlight">|</span> StrOutputParser()</div>
      <div>result = chain.invoke({<span class="green">"concept"</span>: <span class="green">"recursion"</span>})</div>
    </div>

    <h3>Streaming responses</h3>
    <p>For interactive applications (chatbots, live demos), you don't want to wait for the entire response to arrive — you want to display tokens as they stream in. LangChain makes this trivial with the <code>stream()</code> method:</p>

    <div class="arch-diagram">
      <div class="title">STREAMING EXAMPLE</div>
      <div><span class="purple">for</span> chunk <span class="purple">in</span> chain.stream({<span class="green">"concept"</span>: <span class="green">"recursion"</span>}):</div>
      <div>    print(chunk, end=<span class="green">""</span>, flush=<span class="yellow">True</span>)</div>
      <div></div>
      <div><span class="dim"># Output appears token-by-token in real time:</span></div>
      <div><span class="green">Rec</span><span class="green">ursion</span><span class="green"> is</span><span class="green"> when</span><span class="green"> a</span><span class="green"> function</span><span class="green"> calls</span><span class="green"> itself</span><span class="green">...</span></div>
    </div>

    <div class="insight-box">
      <strong>Production tip:</strong> Always set <code>temperature=0</code> for deterministic tasks (data extraction, code generation, classification). Use <code>temperature=0.7+</code> only when you genuinely want creative variation. Inconsistent outputs from the same input are a debugging nightmare in production.
    </div>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ invoke() — single call</h4>
        <p>Process one input synchronously. Returns the complete result. Use for most development and testing.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #93c5fd;">
        <h4>📦 batch() — parallel calls</h4>
        <p>Process a list of inputs in parallel. <code>chain.batch([{"concept": "recursion"}, {"concept": "hashing"}])</code>. Great for bulk processing.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #c4b5fd;">
        <h4>🌊 stream() — real-time</h4>
        <p>Yields tokens as they arrive. Essential for chat UIs. Works with the entire chain, not just the model.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fcd34d;">
        <h4>⚡ ainvoke() — async</h4>
        <p>Async version of invoke. Use in FastAPI, async web servers, or when running multiple chains concurrently with <code>asyncio.gather()</code>.</p>
      </div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Create a ChatOpenAI instance with <code>temperature=0</code>. Invoke the same prompt three times and confirm the output is identical each time.</li>
        <li>Change temperature to <code>1.0</code> and invoke three times. Observe how outputs vary.</li>
        <li>Use <code>chain.batch()</code> to process 5 different concepts in a single call. Measure the total time vs. 5 sequential <code>invoke()</code> calls.</li>
        <li>If you have Ollama installed: swap to <code>ChatOllama(model="llama3")</code> and verify the chain works without changing any other code.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day1 -->

<!-- ═══════════════════════════════════════════════
     DAY 2 — Prompt Engineering & Output Parsing
     ═══════════════════════════════════════════════ -->
<div id="day2" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d2prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 2 overview</div>
  <div class="sched-body">
    <h4>Template your prompts, parse your outputs — the two bookends of every chain</h4>
    <p>Two topics · ~2 hours · Cover: Prompt templates & few-shot learning + Output parsers & structured data</p>
  </div>
</div>

<!-- ── TOPIC 3 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">3</div>
    <h2>Prompt Templates & Few-Shot Learning</h2>
    <span class="topic-time">50 min</span>
  </div>
  <div class="topic-body">
    <p>Hardcoding prompts as raw strings is fine for a quick test, but it falls apart in production. What if you need to inject a user's name, today's date, the last 5 messages, or a set of examples? That's why LangChain provides <strong>prompt templates</strong> — reusable, composable prompt factories with typed variables.</p>

    <p>A prompt template separates the <em>structure</em> of your prompt from the <em>data</em>. You define the template once with placeholder variables, and at runtime LangChain fills in the blanks. This makes your prompts testable, version-controllable, and safe from accidental injection of formatting characters.</p>

    <h3>PromptTemplate — simple string templates</h3>
    <p>The most basic template. Takes a string with <code>{variable}</code> placeholders and returns a formatted string:</p>

    <div class="arch-diagram">
      <div class="title">PROMPTTEMPLATE</div>
      <div><span class="purple">from</span> langchain_core.prompts <span class="purple">import</span> PromptTemplate</div>
      <div></div>
      <div>template = PromptTemplate.from_template(</div>
      <div>    <span class="green">"Translate the following {language} code to Python:\n\n{code}"</span></div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># At runtime — fill in the variables</span></div>
      <div>formatted = template.invoke({</div>
      <div>    <span class="green">"language"</span>: <span class="green">"JavaScript"</span>,</div>
      <div>    <span class="green">"code"</span>: <span class="green">"const sum = (a, b) => a + b;"</span></div>
      <div>})</div>
      <div><span class="dim"># → "Translate the following JavaScript code to Python:\n\nconst sum = (a, b) => a + b;"</span></div>
    </div>

    <h3>ChatPromptTemplate — structured chat messages</h3>
    <p>Most LLMs use chat-format messages (system, human, ai). <code>ChatPromptTemplate</code> lets you define a sequence of typed messages, each with their own variables:</p>

    <div class="arch-diagram">
      <div class="title">CHATPROMPTTEMPLATE</div>
      <div><span class="purple">from</span> langchain_core.prompts <span class="purple">import</span> ChatPromptTemplate</div>
      <div></div>
      <div>prompt = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"You are a {role}. Always respond in {format} format."</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{query}"</span>),</div>
      <div>])</div>
      <div></div>
      <div><span class="dim"># Produces a list of messages:</span></div>
      <div><span class="dim"># [SystemMessage("You are a data analyst. Always respond in JSON format."),</span></div>
      <div><span class="dim">#  HumanMessage("What were last quarter's sales?")]</span></div>
    </div>

    <h3>FewShotPromptTemplate — teach by example</h3>
    <p>Few-shot prompting is one of the most powerful techniques for steering LLM behaviour. Instead of describing what you want in abstract terms, you <em>show</em> the model 2–5 worked examples. LangChain's <code>FewShotPromptTemplate</code> makes this systematic:</p>

    <div class="arch-diagram">
      <div class="title">FEW-SHOT PROMPTING</div>
      <div><span class="purple">from</span> langchain_core.prompts <span class="purple">import</span> FewShotPromptTemplate, PromptTemplate</div>
      <div></div>
      <div>examples = [</div>
      <div>    {<span class="green">"input"</span>: <span class="green">"happy"</span>, <span class="green">"output"</span>: <span class="green">"sad"</span>},</div>
      <div>    {<span class="green">"input"</span>: <span class="green">"tall"</span>, <span class="green">"output"</span>: <span class="green">"short"</span>},</div>
      <div>    {<span class="green">"input"</span>: <span class="green">"fast"</span>, <span class="green">"output"</span>: <span class="green">"slow"</span>},</div>
      <div>]</div>
      <div></div>
      <div>example_prompt = PromptTemplate.from_template(</div>
      <div>    <span class="green">"Input: {input}\nOutput: {output}"</span></div>
      <div>)</div>
      <div></div>
      <div>few_shot = FewShotPromptTemplate(</div>
      <div>    examples=examples,</div>
      <div>    example_prompt=example_prompt,</div>
      <div>    prefix=<span class="green">"Give the antonym of every input."</span>,</div>
      <div>    suffix=<span class="green">"Input: {input}\nOutput:"</span>,</div>
      <div>    input_variables=[<span class="green">"input"</span>],</div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># few_shot.invoke({"input": "bright"}) → shows all examples + "Input: bright\nOutput:"</span></div>
    </div>

    <h3>MessagesPlaceholder — inject dynamic message history</h3>
    <p>When building chat applications, you need to inject the conversation history into the prompt. <code>MessagesPlaceholder</code> reserves a slot in the template for a list of messages that gets filled at runtime:</p>

    <div class="arch-diagram">
      <div class="title">MESSAGESPLACEHOLDER FOR CHAT HISTORY</div>
      <div><span class="purple">from</span> langchain_core.prompts <span class="purple">import</span> ChatPromptTemplate, MessagesPlaceholder</div>
      <div></div>
      <div>prompt = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"You are a helpful assistant."</span>),</div>
      <div>    MessagesPlaceholder(variable_name=<span class="green">"history"</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{input}"</span>),</div>
      <div>])</div>
      <div></div>
      <div><span class="dim"># At runtime, "history" is a list of HumanMessage / AIMessage objects</span></div>
      <div><span class="dim"># from previous turns of the conversation.</span></div>
    </div>

    <div class="insight-box">
      <strong>Template composition:</strong> You can compose templates. Build small, reusable prompt fragments (a persona block, a formatting instruction, an examples section) and combine them into larger templates. This is the prompt engineering equivalent of writing functions instead of copy-pasting code.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Create a <code>ChatPromptTemplate</code> with system and human messages. Add 3 different variables and verify they all get filled.</li>
        <li>Build a <code>FewShotPromptTemplate</code> that teaches the model to convert natural language to SQL queries. Provide 3 examples and test with a new query.</li>
        <li>Add a <code>MessagesPlaceholder</code> to your chat prompt and pass in a list of 2 fake history messages. Print the formatted output to verify it injects correctly.</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 4 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">4</div>
    <h2>Output Parsers & Structured Data</h2>
    <span class="topic-time">40 min</span>
  </div>
  <div class="topic-body">
    <p>LLMs respond with unstructured text. But your application needs structured data — a JSON object, a Python dict, a Pydantic model, a boolean. <strong>Output parsers</strong> bridge this gap. They tell the LLM what format to produce (via format instructions injected into the prompt) and then parse the raw text response into a typed object.</p>

    <p>Without output parsers, you'd write fragile regex patterns to extract data from LLM responses. With output parsers, you define the schema once, and LangChain handles the formatting instructions, the parsing, and even retries when the LLM produces malformed output.</p>

    <h3>The three parsers you'll use most</h3>

    <table class="cmp-table">
      <thead><tr><th>Parser</th><th>Output Type</th><th>When to Use</th><th>Complexity</th></tr></thead>
      <tbody>
        <tr><td><strong>StrOutputParser</strong></td><td>Plain string</td><td>Free-text responses (summaries, explanations, creative content)</td><td>Simplest</td></tr>
        <tr><td><strong>JsonOutputParser</strong></td><td>Python dict</td><td>When you need key-value data but don't want to define a full schema</td><td>Medium</td></tr>
        <tr><td><strong>PydanticOutputParser</strong></td><td>Pydantic model</td><td>When you need strict typing, validation, and complex nested schemas</td><td>Most robust</td></tr>
      </tbody>
    </table>

    <h3>StrOutputParser — extract the text</h3>
    <p>The simplest parser. It takes the LLM's response (an <code>AIMessage</code> object) and returns just the string content. You already used this in Topic 1:</p>

    <div class="arch-diagram">
      <div class="title">STROUTPUTPARSER</div>
      <div><span class="purple">from</span> langchain_core.output_parsers <span class="purple">import</span> StrOutputParser</div>
      <div></div>
      <div>chain = prompt | model | StrOutputParser()</div>
      <div><span class="dim"># AIMessage(content="Recursion is...") → "Recursion is..."</span></div>
    </div>

    <h3>JsonOutputParser — get structured dicts</h3>
    <p>When you need the LLM to return a JSON object, <code>JsonOutputParser</code> injects formatting instructions into the prompt and parses the response into a Python dict:</p>

    <div class="arch-diagram">
      <div class="title">JSONOUTPUTPARSER</div>
      <div><span class="purple">from</span> langchain_core.output_parsers <span class="purple">import</span> JsonOutputParser</div>
      <div></div>
      <div>parser = JsonOutputParser()</div>
      <div></div>
      <div>prompt = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"Extract the person's details.\n{format_instructions}"</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{text}"</span>),</div>
      <div>])</div>
      <div></div>
      <div><span class="dim"># Inject the parser's format instructions into the prompt</span></div>
      <div>prompt = prompt.partial(format_instructions=parser.get_format_instructions())</div>
      <div></div>
      <div>chain = prompt | model | parser</div>
      <div>result = chain.invoke({<span class="green">"text"</span>: <span class="green">"John Doe is 30 years old and lives in NYC"</span>})</div>
      <div><span class="dim"># → {"name": "John Doe", "age": 30, "city": "NYC"}</span></div>
    </div>

    <h3>PydanticOutputParser — full type safety</h3>
    <p>The gold standard for production applications. Define a Pydantic model with types, descriptions, and validation rules. The parser generates precise format instructions and validates the LLM's output against your schema:</p>

    <div class="arch-diagram">
      <div class="title">PYDANTICOUTPUTPARSER</div>
      <div><span class="purple">from</span> langchain_core.output_parsers <span class="purple">import</span> PydanticOutputParser</div>
      <div><span class="purple">from</span> pydantic <span class="purple">import</span> BaseModel, Field</div>
      <div></div>
      <div><span class="blue">class</span> <span class="yellow">CodeReview</span>(BaseModel):</div>
      <div>    has_bugs: <span class="blue">bool</span> = Field(description=<span class="green">"Whether the code contains bugs"</span>)</div>
      <div>    severity: <span class="blue">str</span> = Field(description=<span class="green">"low, medium, or high"</span>)</div>
      <div>    issues: list[<span class="blue">str</span>] = Field(description=<span class="green">"List of specific issues found"</span>)</div>
      <div>    fixed_code: <span class="blue">str</span> = Field(description=<span class="green">"The corrected version of the code"</span>)</div>
      <div></div>
      <div>parser = PydanticOutputParser(pydantic_object=CodeReview)</div>
      <div></div>
      <div><span class="dim"># parser.get_format_instructions() → detailed JSON schema for the LLM</span></div>
      <div><span class="dim"># parser.parse(llm_output) → validated CodeReview instance</span></div>
    </div>

    <h3>Handling malformed output — the retry parser</h3>
    <p>LLMs sometimes produce invalid JSON — a missing comma, an extra closing bracket, or wrapping the JSON in markdown code fences. LangChain's <code>OutputFixingParser</code> catches parse failures and asks the LLM to fix the output:</p>

    <div class="arch-diagram">
      <div class="title">RETRY ON PARSE FAILURE</div>
      <div><span class="purple">from</span> langchain.output_parsers <span class="purple">import</span> OutputFixingParser</div>
      <div></div>
      <div>fixing_parser = OutputFixingParser.from_llm(</div>
      <div>    parser=parser,  <span class="dim"># your PydanticOutputParser</span></div>
      <div>    llm=model,      <span class="dim"># LLM to use for fixing</span></div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># If the initial parse fails, it sends the malformed output</span></div>
      <div><span class="dim"># back to the LLM with: "Fix this JSON to match the schema"</span></div>
    </div>

    <div class="insight-box">
      <strong>When to use which parser:</strong> Use <code>StrOutputParser</code> for free-text chains (summarisation, creative writing). Use <code>JsonOutputParser</code> for quick structured extraction where you don't need validation. Use <code>PydanticOutputParser</code> whenever the downstream code expects strict types — APIs, databases, conditionals. In production, always use Pydantic.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a chain with <code>PydanticOutputParser</code> that extracts a movie review into: <code>title</code>, <code>rating</code> (int 1-10), <code>sentiment</code> (positive/negative/mixed), and <code>summary</code> (str).</li>
        <li>Feed it 3 different movie reviews and verify the parsed Pydantic objects are valid.</li>
        <li>Intentionally break the chain by setting <code>temperature=1.5</code> and see if the parser fails. Then add <code>OutputFixingParser</code> and test again.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day2 -->

<!-- ═══════════════════════════════════════════════
     DAY 3 — LCEL: The Composable Pipeline
     ═══════════════════════════════════════════════ -->
<div id="day3" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d3prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 3 overview</div>
  <div class="sched-body">
    <h4>The pipe operator — compose anything with LCEL</h4>
    <p>Two topics · ~2 hours · Cover: LCEL fundamentals + chains in practice</p>
  </div>
</div>

<!-- ── TOPIC 5 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">5</div>
    <h2>LCEL — LangChain Expression Language</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>LCEL is the foundational composability model of LangChain. It's not a separate language — it's a protocol that makes every LangChain component pipeable with the <code>|</code> operator, just like Unix pipes. If component A's output type matches component B's input type, you can pipe them together: <code>A | B</code>.</p>

    <p>Under the hood, every LangChain component implements the <strong>Runnable</strong> interface. This means every component — prompts, models, parsers, retrievers, custom functions — exposes the same four methods: <code>invoke()</code>, <code>batch()</code>, <code>stream()</code>, and <code>ainvoke()</code>. When you pipe them, LangChain creates a <code>RunnableSequence</code> that calls each component in order, passing the output of one as the input to the next.</p>

    <p>This is powerful because it means you get streaming, batching, and async for <em>free</em> on any chain — you don't need to implement those capabilities for each component. Build the chain, and all four execution modes just work.</p>

    <div class="arch-diagram">
      <div class="title">THE RUNNABLE PROTOCOL</div>
      <div><span class="yellow">┌───────────────────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  Every LangChain component implements <span class="highlight">Runnable</span>    <span class="yellow">│</span></div>
      <div><span class="yellow">├───────────────────────────────────────────────────┤</span></div>
      <div><span class="yellow">│</span>  <span class="green">.invoke(input)</span>    <span class="dim">→ single call, returns result</span>   <span class="yellow">│</span></div>
      <div><span class="yellow">│</span>  <span class="blue">.batch([inputs])</span>  <span class="dim">→ parallel calls, returns list</span>  <span class="yellow">│</span></div>
      <div><span class="yellow">│</span>  <span class="purple">.stream(input)</span>    <span class="dim">→ yields chunks in real time</span>   <span class="yellow">│</span></div>
      <div><span class="yellow">│</span>  <span class="orange">.ainvoke(input)</span>   <span class="dim">→ async single call</span>             <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────────────────────────────────────────┘</span></div>
      <div style="margin-top:8px;"><span class="dim">Pipe operator:</span> <span class="highlight">A | B | C</span> <span class="dim">→ RunnableSequence(A, B, C)</span></div>
      <div><span class="dim">All four methods work on the entire sequence automatically.</span></div>
    </div>

    <h3>Key Runnable primitives</h3>
    <p>LCEL provides several utility Runnables that act as plumbing — they transform, fork, merge, or inject data as it flows through the chain:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>🔗 RunnablePassthrough</h4>
        <p>Passes input through unchanged. Used to carry original data alongside transformed data. <code>RunnablePassthrough.assign(summary=chain)</code> adds the chain's output as a new key while keeping the original input.</p>
      </div>
      <div class="block-card">
        <h4>🔧 RunnableLambda</h4>
        <p>Wraps any Python function as a Runnable. <code>RunnableLambda(lambda x: x.upper())</code> becomes a pipeable step. Use for data transformation, filtering, or custom logic.</p>
      </div>
      <div class="block-card">
        <h4>⚡ RunnableParallel</h4>
        <p>Runs multiple chains in parallel on the same input. Returns a dict with each chain's output. <code>RunnableParallel(summary=chain_a, sentiment=chain_b)</code>.</p>
      </div>
      <div class="block-card">
        <h4>🛡 with_fallbacks()</h4>
        <p>Wraps a Runnable with fallback alternatives. If the primary chain fails, it tries the next one. <code>chain.with_fallbacks([backup_chain])</code>.</p>
      </div>
    </div>

    <h3>Building a chain step by step</h3>
    <p>Let's build a real chain that takes a piece of text, processes it through three parallel analyses, and combines the results:</p>

    <div class="arch-diagram">
      <div class="title">STEP-BY-STEP CHAIN CONSTRUCTION</div>
      <div><span class="purple">from</span> langchain_core.runnables <span class="purple">import</span> (</div>
      <div>    RunnablePassthrough, RunnableLambda, RunnableParallel</div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># Step 1: Define sub-chains</span></div>
      <div>summarize = summary_prompt | model | StrOutputParser()</div>
      <div>extract_keywords = keyword_prompt | model | JsonOutputParser()</div>
      <div>detect_sentiment = sentiment_prompt | model | StrOutputParser()</div>
      <div></div>
      <div><span class="dim"># Step 2: Run all three in parallel</span></div>
      <div>analyze = RunnableParallel(</div>
      <div>    summary=summarize,</div>
      <div>    keywords=extract_keywords,</div>
      <div>    sentiment=detect_sentiment,</div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># Step 3: Invoke</span></div>
      <div>result = analyze.invoke({<span class="green">"text"</span>: <span class="green">"LangChain is a framework for..."</span>})</div>
      <div></div>
      <div><span class="dim"># result = {</span></div>
      <div><span class="dim">#   "summary": "LangChain provides...",</span></div>
      <div><span class="dim">#   "keywords": ["framework", "LLM", "chains"],</span></div>
      <div><span class="dim">#   "sentiment": "positive"</span></div>
      <div><span class="dim"># }</span></div>
    </div>

    <div class="insight-box">
      <strong>Why LCEL over the old chain APIs:</strong> LangChain v0.1 had classes like <code>LLMChain</code>, <code>SequentialChain</code>, <code>TransformChain</code>. These are deprecated. LCEL replaces all of them with a single composable syntax. If you see legacy tutorials using <code>LLMChain</code>, mentally translate to <code>prompt | model | parser</code>.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a chain that uses <code>RunnablePassthrough.assign()</code> to add a "word_count" field to the input using a <code>RunnableLambda</code> that counts words.</li>
        <li>Create a <code>RunnableParallel</code> that runs two different prompts (a summary and a translation) on the same input simultaneously.</li>
        <li>Use <code>.stream()</code> on your parallel chain and observe how the streaming works with parallel branches.</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 6 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">6</div>
    <h2>Chains in Practice</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>Now that you understand the LCEL primitives, let's combine them into real-world chain patterns. These patterns show up in almost every LLM application — learn them once, use them everywhere.</p>

    <h3>Pattern 1: Sequential chain (summarise → translate → format)</h3>
    <p>The most common pattern. Data flows through a pipeline where each step transforms the output of the previous step. This is exactly how Unix pipes work: <code>cat file | grep error | wc -l</code>.</p>

    <div class="arch-diagram">
      <div class="title">SEQUENTIAL CHAIN: SUMMARISE → TRANSLATE → FORMAT</div>
      <div><span class="dim"># Each step is a mini-chain: prompt | model | parser</span></div>
      <div></div>
      <div>summarize = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"Summarise the text in 2 sentences."</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{text}"</span>),</div>
      <div>]) | model | StrOutputParser()</div>
      <div></div>
      <div>translate = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"Translate to Hindi."</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{text}"</span>),</div>
      <div>]) | model | StrOutputParser()</div>
      <div></div>
      <div>format_md = ChatPromptTemplate.from_messages([</div>
      <div>    (<span class="green">"system"</span>, <span class="green">"Format as a markdown bullet list."</span>),</div>
      <div>    (<span class="green">"human"</span>, <span class="green">"{text}"</span>),</div>
      <div>]) | model | StrOutputParser()</div>
      <div></div>
      <div><span class="dim"># Wire them together — output of each becomes {text} for the next</span></div>
      <div>pipeline = (</div>
      <div>    summarize</div>
      <div>    | RunnableLambda(<span class="purple">lambda</span> s: {<span class="green">"text"</span>: s})</div>
      <div>    | translate</div>
      <div>    | RunnableLambda(<span class="purple">lambda</span> s: {<span class="green">"text"</span>: s})</div>
      <div>    | format_md</div>
      <div>)</div>
    </div>

    <h3>Pattern 2: Branching chain (RunnableParallel)</h3>
    <p>When you need multiple independent analyses of the same input. Each branch runs in parallel, and the results are merged into a single dict. This is the <strong>fan-out</strong> pattern.</p>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num act">1</div>
        <div class="step-body">
          <div class="step-label act">FAN OUT</div>
          <div class="step-title">RunnableParallel splits the input</div>
          <div class="step-desc">The same input dict is passed to all branches simultaneously. Each branch runs its own prompt → model → parser chain independently.</div>
          <div class="step-tools">
            <span class="tool-badge green">Parallel execution</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">2</div>
        <div class="step-body">
          <div class="step-label plan">FAN IN</div>
          <div class="step-title">Results merge into a dict</div>
          <div class="step-desc">Each branch's output becomes a key in the result dict: <code>{"summary": "...", "keywords": [...], "tone": "formal"}</code>. Downstream steps can access any key.</div>
          <div class="step-tools">
            <span class="tool-badge purple">Dict merge</span>
          </div>
        </div>
      </div>
    </div>

    <h3>Pattern 3: Fallback chain (with_fallbacks)</h3>
    <p>Production systems need resilience. If your primary model (GPT-4o) is down or returns an error, fall back to a cheaper model (GPT-4o-mini) or a local model (Ollama). LangChain makes this a one-liner:</p>

    <div class="arch-diagram">
      <div class="title">FALLBACK CHAIN</div>
      <div><span class="dim"># Primary: GPT-4o (best quality)</span></div>
      <div>primary = prompt | ChatOpenAI(model=<span class="green">"gpt-4o"</span>) | parser</div>
      <div></div>
      <div><span class="dim"># Fallback: GPT-4o-mini (cheaper, always available)</span></div>
      <div>backup = prompt | ChatOpenAI(model=<span class="green">"gpt-4o-mini"</span>) | parser</div>
      <div></div>
      <div><span class="dim"># Chain with automatic fallback</span></div>
      <div>resilient_chain = primary.with_fallbacks([backup])</div>
      <div></div>
      <div><span class="dim"># If primary raises an exception, backup runs automatically</span></div>
      <div>result = resilient_chain.invoke({<span class="green">"text"</span>: <span class="green">"Analyse this..."</span>})</div>
    </div>

    <h3>Debugging chains — verbose mode and callbacks</h3>
    <p>When a chain produces unexpected output, you need to see what's happening at each step. LangChain provides several debugging tools:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>🔍 Verbose mode</h4>
        <p>Set <code>set_verbose(True)</code> globally or pass <code>config={"verbose": True}</code> to see every prompt and response printed to the console.</p>
      </div>
      <div class="block-card">
        <h4>📊 Callbacks</h4>
        <p>Attach custom callback handlers to log, measure, or modify behaviour at each step. <code>chain.invoke(input, config={"callbacks": [handler]})</code>.</p>
      </div>
    </div>

    <div class="insight-box">
      <strong>Chain debugging golden rule:</strong> If the final output is wrong, <strong>inspect the intermediate outputs</strong>. Break the chain into individual steps, invoke each one separately, and find where the data gets corrupted. LCEL makes this easy — each <code>|</code> component is independently invocable.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a sequential chain: take a product description → generate marketing copy → translate to Spanish → extract key phrases.</li>
        <li>Add a fallback: if the primary model fails, fall back to a different model (or a mock response for testing).</li>
        <li>Enable verbose mode and trace how data transforms at each stage. Identify where the most tokens are used.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day3 -->

<!-- ═══════════════════════════════════════════════
     DAY 4 — Memory, Tools & Agents
     ═══════════════════════════════════════════════ -->
<div id="day4" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d4prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 4 overview</div>
  <div class="sched-body">
    <h4>Give your chains memory, tools, and agency</h4>
    <p>Two topics · ~2 hours · Cover: Conversational memory + Tools & agents in LangChain</p>
  </div>
</div>

<!-- ── TOPIC 7 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">7</div>
    <h2>Conversational Memory</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>By default, every LLM call is stateless — the model has no idea what happened in the previous turn of conversation. If a user says "Book the cheapest one" and the model doesn't remember that the previous turn returned three flight options, the chain fails. <strong>Memory</strong> fixes this by injecting conversation history into each prompt.</p>

    <p>In Unit 2 you learned about four types of agent memory (working, episodic, semantic, procedural). LangChain's memory classes implement <strong>working memory</strong> — the per-conversation state that tracks what's been said so far. The strategy you choose determines how much history the LLM sees and how much it costs.</p>

    <h3>Three memory strategies</h3>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num act">1</div>
        <div class="step-body">
          <div class="step-label act">BUFFER MEMORY</div>
          <div class="step-title">ConversationBufferMemory</div>
          <div class="step-desc">Stores every message verbatim. Simple and complete — but the context window fills up fast. After 20–30 turns, you'll hit token limits. Best for short conversations (5–10 turns).</div>
          <div class="step-tools">
            <span class="tool-badge green">Complete history</span>
            <span class="tool-badge red">Token-expensive</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num perceive">2</div>
        <div class="step-body">
          <div class="step-label perceive">WINDOW MEMORY</div>
          <div class="step-title">ConversationBufferWindowMemory</div>
          <div class="step-desc">Keeps only the last <em>k</em> messages (e.g., the last 10 turns). Older messages are dropped. Fixed token cost regardless of conversation length. Best for when recent context is more important than historical context.</div>
          <div class="step-tools">
            <span class="tool-badge blue">Fixed cost</span>
            <span class="tool-badge amber">Loses old context</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">3</div>
        <div class="step-body">
          <div class="step-label plan">SUMMARY MEMORY</div>
          <div class="step-title">ConversationSummaryMemory</div>
          <div class="step-desc">Uses an LLM to summarise older parts of the conversation into a compressed paragraph. Recent messages are kept verbatim. Best of both worlds — retains key context from early messages without the token cost. The trade-off: summarisation has its own LLM cost and can lose nuance.</div>
          <div class="step-tools">
            <span class="tool-badge purple">Balanced</span>
            <span class="tool-badge amber">Summary cost</span>
          </div>
        </div>
      </div>
    </div>

    <h3>Comparison at a glance</h3>
    <table class="cmp-table">
      <thead><tr><th>Memory Type</th><th>Token Cost</th><th>Completeness</th><th>Best For</th></tr></thead>
      <tbody>
        <tr><td><strong>Buffer</strong></td><td>Grows with each turn</td><td>Complete — every word kept</td><td>Short conversations (≤10 turns)</td></tr>
        <tr><td><strong>Window (k)</strong></td><td>Fixed at k messages</td><td>Recent context only</td><td>Task-focused chats where old context doesn't matter</td></tr>
        <tr><td><strong>Summary</strong></td><td>Moderate (summary + recent)</td><td>Compressed old + full recent</td><td>Long conversations where both old and new context matter</td></tr>
      </tbody>
    </table>

    <h3>Adding memory to LCEL chains — RunnableWithMessageHistory</h3>
    <p>The modern way to add memory in LangChain is <code>RunnableWithMessageHistory</code>. It wraps any chain and automatically loads/saves conversation history per session:</p>

    <div class="arch-diagram">
      <div class="title">RUNNABLEWITHMESSAGEHISTORY</div>
      <div><span class="purple">from</span> langchain_core.runnables.history <span class="purple">import</span> RunnableWithMessageHistory</div>
      <div><span class="purple">from</span> langchain_community.chat_message_histories <span class="purple">import</span> ChatMessageHistory</div>
      <div></div>
      <div><span class="dim"># In-memory store — use Redis/DB in production</span></div>
      <div>store = {}</div>
      <div></div>
      <div><span class="blue">def</span> <span class="yellow">get_session_history</span>(session_id: <span class="blue">str</span>):</div>
      <div>    <span class="purple">if</span> session_id <span class="purple">not in</span> store:</div>
      <div>        store[session_id] = ChatMessageHistory()</div>
      <div>    <span class="purple">return</span> store[session_id]</div>
      <div></div>
      <div><span class="dim"># Wrap your chain with message history</span></div>
      <div>chain_with_memory = RunnableWithMessageHistory(</div>
      <div>    chain,  <span class="dim"># your LCEL chain (prompt | model | parser)</span></div>
      <div>    get_session_history,</div>
      <div>    input_messages_key=<span class="green">"input"</span>,</div>
      <div>    history_messages_key=<span class="green">"history"</span>,</div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># Each invoke automatically loads + saves history for that session</span></div>
      <div>chain_with_memory.invoke(</div>
      <div>    {<span class="green">"input"</span>: <span class="green">"What's LangChain?"</span>},</div>
      <div>    config={<span class="green">"configurable"</span>: {<span class="green">"session_id"</span>: <span class="green">"user-123"</span>}},</div>
      <div>)</div>
    </div>

    <div class="insight-box">
      <strong>Production memory:</strong> The in-memory <code>ChatMessageHistory</code> is fine for development. For production, use <code>RedisChatMessageHistory</code>, <code>SQLChatMessageHistory</code>, or <code>FirestoreChatMessageHistory</code> — these persist across server restarts and support horizontal scaling.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a chatbot chain with <code>RunnableWithMessageHistory</code>. Have a 5-turn conversation and verify the model remembers earlier turns.</li>
        <li>Switch from <code>ChatMessageHistory</code> to a window-based approach (keep only the last 3 messages). Verify the model forgets messages from turn 1 when you're on turn 5.</li>
        <li>Calculate the token cost difference between Buffer and Window memory for a 20-turn conversation with ~100 tokens per message.</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 8 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">8</div>
    <h2>Tools & Agents in LangChain</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>This is where everything from Units 2 and 3 converges. You've learned about the Tool Use pattern and the ReAct loop on paper. You've built chains with LCEL. Now you'll connect them — giving your chains the ability to <strong>call external tools</strong> and <strong>make autonomous decisions</strong> about which tools to use.</p>

    <p>A LangChain <strong>Tool</strong> is a function that the LLM can decide to call. The LLM reads the tool's name and description, determines whether to call it, generates the appropriate arguments, and the framework executes the function and returns the result. This is the <strong>Action Module</strong> from Unit 2 — implemented in code.</p>

    <h3>Creating tools — the @tool decorator</h3>
    <p>The fastest way to create a tool is to decorate a Python function with <code>@tool</code>. LangChain extracts the name, description, and parameter types from the function signature and docstring:</p>

    <div class="arch-diagram">
      <div class="title">CREATING CUSTOM TOOLS</div>
      <div><span class="purple">from</span> langchain_core.tools <span class="purple">import</span> tool</div>
      <div></div>
      <div><span class="blue">@tool</span></div>
      <div><span class="blue">def</span> <span class="yellow">calculate_bmi</span>(weight_kg: <span class="blue">float</span>, height_m: <span class="blue">float</span>) -> <span class="blue">str</span>:</div>
      <div>    <span class="green">"""Calculate Body Mass Index given weight in kg and height in meters."""</span></div>
      <div>    bmi = weight_kg / (height_m ** <span class="yellow">2</span>)</div>
      <div>    category = (</div>
      <div>        <span class="green">"underweight"</span> <span class="purple">if</span> bmi < <span class="yellow">18.5</span></div>
      <div>        <span class="purple">else</span> <span class="green">"normal"</span> <span class="purple">if</span> bmi < <span class="yellow">25</span></div>
      <div>        <span class="purple">else</span> <span class="green">"overweight"</span> <span class="purple">if</span> bmi < <span class="yellow">30</span></div>
      <div>        <span class="purple">else</span> <span class="green">"obese"</span></div>
      <div>    )</div>
      <div>    <span class="purple">return</span> f<span class="green">"BMI: {bmi:.1f} ({category})"</span></div>
      <div></div>
      <div><span class="dim"># LangChain reads: name="calculate_bmi", description from docstring,</span></div>
      <div><span class="dim"># params: {"weight_kg": float, "height_m": float}</span></div>
    </div>

    <h3>Built-in tools — ready to use</h3>
    <p>LangChain includes integrations with popular external services. Install the relevant package and they're ready to wire into your agents:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>🔍 Tavily Search</h4>
        <p>Web search optimised for LLM consumption. Returns clean, concise search results instead of raw HTML. <code>pip install langchain-tavily</code></p>
      </div>
      <div class="block-card">
        <h4>📚 Wikipedia</h4>
        <p>Query Wikipedia articles for factual information. Great for knowledge-grounded agents. <code>pip install wikipedia</code></p>
      </div>
      <div class="block-card">
        <h4>🐍 Python REPL</h4>
        <p>Execute Python code in a sandboxed environment. The agent can write and run code to solve math problems, data analysis, or testing. Use with caution in production.</p>
      </div>
      <div class="block-card">
        <h4>🔧 Custom tools</h4>
        <p>Any Python function can become a tool with <code>@tool</code>. Database queries, API calls, file operations — if Python can do it, your agent can do it.</p>
      </div>
    </div>

    <h3>AgentExecutor and create_react_agent</h3>
    <p>An <strong>agent</strong> combines an LLM, a set of tools, and a reasoning strategy into an autonomous loop. LangChain provides <code>create_react_agent</code> — which implements the ReAct pattern from Unit 2 — out of the box:</p>

    <div class="arch-diagram">
      <div class="title">BUILDING A REACT AGENT</div>
      <div><span class="purple">from</span> langchain.agents <span class="purple">import</span> create_react_agent, AgentExecutor</div>
      <div><span class="purple">from</span> langchain <span class="purple">import</span> hub</div>
      <div></div>
      <div><span class="dim"># 1. Define tools</span></div>
      <div>tools = [calculate_bmi, tavily_search, python_repl]</div>
      <div></div>
      <div><span class="dim"># 2. Get the ReAct prompt template from LangChain Hub</span></div>
      <div>prompt = hub.pull(<span class="green">"hwchase17/react"</span>)</div>
      <div></div>
      <div><span class="dim"># 3. Create the agent (reasoning engine)</span></div>
      <div>agent = create_react_agent(model, tools, prompt)</div>
      <div></div>
      <div><span class="dim"># 4. Wrap in AgentExecutor (manages the loop)</span></div>
      <div>executor = AgentExecutor(</div>
      <div>    agent=agent,</div>
      <div>    tools=tools,</div>
      <div>    verbose=<span class="yellow">True</span>,   <span class="dim"># see Thought/Action/Observation</span></div>
      <div>    max_iterations=<span class="yellow">10</span>,  <span class="dim"># safety limit</span></div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># 5. Run it</span></div>
      <div>result = executor.invoke({</div>
      <div>    <span class="green">"input"</span>: <span class="green">"I weigh 75kg and am 1.78m tall. What's my BMI?"</span></div>
      <div>})</div>
    </div>

    <h3>How it connects to Unit 2's ReAct pattern</h3>
    <p>When you set <code>verbose=True</code>, you'll see the exact Thought → Action → Observation loop from Unit 2 playing out in real code:</p>

    <div class="arch-diagram">
      <div class="title">REACT LOOP IN ACTION (verbose output)</div>
      <div><span class="blue">Thought:</span> <span class="dim">The user wants their BMI calculated. I have the</span></div>
      <div><span class="dim">         calculate_bmi tool. Let me use it with their measurements.</span></div>
      <div><span class="green">Action:</span> <span class="dim">calculate_bmi</span></div>
      <div><span class="green">Action Input:</span> <span class="dim">{"weight_kg": 75.0, "height_m": 1.78}</span></div>
      <div><span class="yellow">Observation:</span> <span class="dim">BMI: 23.7 (normal)</span></div>
      <div><span class="blue">Thought:</span> <span class="dim">I have the BMI result. It's 23.7, which falls in the</span></div>
      <div><span class="dim">         normal range. I can provide the final answer.</span></div>
      <div><span class="purple">Final Answer:</span> <span class="dim">Your BMI is 23.7, which falls in the "normal"</span></div>
      <div><span class="dim">              range (18.5–24.9). You're at a healthy weight!</span></div>
    </div>

    <div class="insight-box">
      <strong>Tool description quality matters enormously.</strong> The LLM decides which tool to call based almost entirely on the tool's name and docstring. A vague docstring like "does calculations" will cause the agent to misuse the tool. Write docstrings like you're writing API docs for a junior developer — specific, clear, with example inputs and outputs.
    </div>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ create_react_agent</h4>
        <p>Implements the ReAct pattern. The agent can think, act, observe, and iterate. Best for tasks with uncertainty or multiple possible paths.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>⚠️ Safety: always set max_iterations</h4>
        <p>Without a cap, a confused agent can loop forever — racking up API costs. Set <code>max_iterations=10</code> as a sane default. Also set <code>max_execution_time=60</code> for a hard timeout.</p>
      </div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Create two custom tools with <code>@tool</code>: a temperature converter (C→F, F→C) and a string reverser.</li>
        <li>Wire them into a ReAct agent with <code>create_react_agent</code> and <code>AgentExecutor</code>.</li>
        <li>Ask the agent: "Convert 100°C to Fahrenheit, then reverse the result text." Watch the Thought/Action/Observation loop.</li>
        <li>Set <code>verbose=True</code> and trace the entire execution. Count the number of LLM calls and tool calls.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day4 -->

<!-- ═══════════════════════════════════════════════
     DAY 5 — Callbacks, Debugging & Project
     ═══════════════════════════════════════════════ -->
<div id="day5" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d5prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 5 overview</div>
  <div class="sched-body">
    <h4>Observe, debug, and build your first real agent project</h4>
    <p>One topic + project lab · ~2 hours · Cover: Callbacks & tracing + Auto-Debugging Code Helper</p>
  </div>
</div>

<!-- ── TOPIC 9 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">9</div>
    <h2>Callbacks, Tracing & Debugging</h2>
    <span class="topic-time">30 min</span>
  </div>
  <div class="topic-body">
    <p>You've built chains, added memory, created tools, and wired agents. Now the question every production engineer asks: <strong>what happens when something goes wrong?</strong> How do you see what the LLM actually received as a prompt? How do you know which tool call failed? How much did that 15-step agent run cost?</p>

    <p>LangChain's callback system gives you hooks into every stage of chain execution. Combined with LangSmith (their hosted tracing platform), you get full observability — every LLM call, every tool invocation, every token, every millisecond, every dollar.</p>

    <h3>CallbackHandler — hooks into chain execution</h3>
    <p>A callback handler is a class that implements event hooks. LangChain fires events at key moments: when a chain starts, when an LLM call begins/ends, when a tool is invoked, when an error occurs. You write handlers to log, measure, or modify behaviour.</p>

    <div class="arch-diagram">
      <div class="title">CUSTOM CALLBACK HANDLER</div>
      <div><span class="purple">from</span> langchain_core.callbacks <span class="purple">import</span> BaseCallbackHandler</div>
      <div></div>
      <div><span class="blue">class</span> <span class="yellow">CostTracker</span>(BaseCallbackHandler):</div>
      <div>    <span class="blue">def</span> <span class="yellow">__init__</span>(self):</div>
      <div>        self.total_tokens = <span class="yellow">0</span></div>
      <div>        self.total_cost = <span class="yellow">0.0</span></div>
      <div></div>
      <div>    <span class="blue">def</span> <span class="yellow">on_llm_end</span>(self, response, **kwargs):</div>
      <div>        usage = response.llm_output.get(<span class="green">"token_usage"</span>, {})</div>
      <div>        tokens = usage.get(<span class="green">"total_tokens"</span>, <span class="yellow">0</span>)</div>
      <div>        self.total_tokens += tokens</div>
      <div>        <span class="dim"># GPT-4o-mini pricing: ~$0.15/1M input, $0.60/1M output</span></div>
      <div>        self.total_cost += tokens * <span class="yellow">0.0000004</span></div>
      <div>        print(f<span class="green">"Tokens: {tokens} | Running cost: ${self.total_cost:.6f}"</span>)</div>
      <div></div>
      <div><span class="dim"># Attach to any chain</span></div>
      <div>tracker = CostTracker()</div>
      <div>result = chain.invoke(input, config={<span class="green">"callbacks"</span>: [tracker]})</div>
      <div>print(f<span class="green">"Total: {tracker.total_tokens} tokens, ${tracker.total_cost:.4f}"</span>)</div>
    </div>

    <h3>LangSmith — full observability</h3>
    <p>LangSmith is LangChain's hosted tracing and evaluation platform. It captures every detail of every chain execution in a visual timeline. To enable it, set two environment variables — no code changes needed:</p>

    <div class="arch-diagram">
      <div class="title">ENABLE LANGSMITH TRACING</div>
      <div><span class="dim"># Add to your .env file</span></div>
      <div><span class="green">LANGCHAIN_TRACING_V2</span>=<span class="yellow">true</span></div>
      <div><span class="green">LANGCHAIN_API_KEY</span>=<span class="yellow">your-langsmith-api-key</span></div>
      <div></div>
      <div><span class="dim"># That's it. Every chain.invoke() is now traced.</span></div>
      <div><span class="dim"># Open smith.langchain.com to see:</span></div>
      <div><span class="dim">#   ✓ Full prompt sent to LLM (every message)</span></div>
      <div><span class="dim">#   ✓ Complete LLM response</span></div>
      <div><span class="dim">#   ✓ Token counts (input, output, total)</span></div>
      <div><span class="dim">#   ✓ Latency per step (ms)</span></div>
      <div><span class="dim">#   ✓ Tool calls with inputs and outputs</span></div>
      <div><span class="dim">#   ✓ Error traces with stack traces</span></div>
    </div>

    <h3>Token counting and cost estimation</h3>
    <p>Every LLM call costs money. In a ReAct agent that makes 8 iterations, you're paying for 8 LLM calls — each with growing context. Tracking cost is not optional in production:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>📊 Per-call tracking</h4>
        <p>Use the <code>on_llm_end</code> callback to capture <code>token_usage</code> from each response. Sum across the entire chain execution for total cost.</p>
      </div>
      <div class="block-card">
        <h4>💰 Budget guards</h4>
        <p>Set a max token budget per execution. If the running total exceeds the limit, abort the chain early. This prevents runaway costs from looping agents.</p>
      </div>
    </div>

    <div class="insight-box">
      <strong>The debugging workflow:</strong> (1) Enable <code>verbose=True</code> during development for quick console output. (2) Use LangSmith in staging for detailed traces with the full prompt/response at each step. (3) Deploy custom callback handlers in production for metrics, alerting, and cost tracking. Layer these — don't rely on just one.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Write a <code>CostTracker</code> callback handler (as shown above) and attach it to a 3-step chain. Invoke the chain and print total tokens and cost.</li>
        <li>If you have a LangSmith account: enable tracing and inspect the trace timeline for your ReAct agent from Topic 8.</li>
        <li>Add a budget guard: if total tokens exceed 1000 mid-execution, raise an exception to abort the chain.</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── PROJECT LAB ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background: var(--earth);">P</div>
    <h2>Project — Build an Auto-Debugging Code Helper</h2>
    <span class="topic-time">90 min</span>
  </div>
  <div class="topic-body">
    <div class="lab-box">
      <h4>🛠 Hands-on Project — Auto-Debugging Agent</h4>
      <p style="margin-bottom: 12px;">Build an agent that receives buggy Python code, diagnoses the error, tests fixes using a Python REPL, critiques its own solution (Reflection pattern), and returns working code with an explanation. This project synthesises everything you've learned in this unit.</p>

      <h4 style="color: var(--earth); margin-top: 16px;">Agent requirements</h4>
      <div class="step-flow" style="margin-top: 12px;">
        <div class="step-card">
          <div class="step-num perceive">1</div>
          <div class="step-body">
            <div class="step-label perceive">RECEIVE</div>
            <div class="step-title">Accept buggy code + error message</div>
            <div class="step-desc">The user provides a Python code snippet and the error it produces. The agent parses and understands the code structure and the error type.</div>
          </div>
        </div>
        <div class="step-card">
          <div class="step-num plan">2</div>
          <div class="step-body">
            <div class="step-label plan">ANALYSE</div>
            <div class="step-title">Diagnose the root cause</div>
            <div class="step-desc">The agent reasons about the error: Is it a syntax error? Logic error? Type error? Missing import? It produces a diagnosis before attempting a fix.</div>
          </div>
        </div>
        <div class="step-card">
          <div class="step-num act">3</div>
          <div class="step-body">
            <div class="step-label act">FIX & TEST</div>
            <div class="step-title">Use Python REPL tool to test the fix</div>
            <div class="step-desc">The agent generates a fixed version of the code and uses the Python REPL tool to execute it. If it still errors, the agent iterates — this is the ReAct loop in action.</div>
            <div class="step-tools">
              <span class="tool-badge green">Python REPL tool</span>
              <span class="tool-badge blue">Web search tool</span>
            </div>
          </div>
        </div>
        <div class="step-card">
          <div class="step-num" style="background: #f59e0b;">4</div>
          <div class="step-body">
            <div class="step-label" style="color: #fcd34d;">REFLECT</div>
            <div class="step-title">Critique the fix using Reflection pattern</div>
            <div class="step-desc">A second LLM call reviews the fix: "Does this fix the root cause or just mask the symptom? Are there edge cases? Is the fix idiomatic Python?" If the critique identifies issues, the agent revises.</div>
          </div>
        </div>
        <div class="step-card">
          <div class="step-num learn">5</div>
          <div class="step-body">
            <div class="step-label learn">DELIVER</div>
            <div class="step-title">Return working code + explanation</div>
            <div class="step-desc">The final output includes: the fixed code, what was wrong, why the fix works, and any caveats. All delivered in a clean, structured format.</div>
          </div>
        </div>
      </div>

      <h4 style="color: var(--earth); margin-top: 16px;">Technical deliverables</h4>
      <ol>
        <li><strong>LCEL chain:</strong> The main agent logic must be composed using LCEL (pipe syntax), not legacy chain classes</li>
        <li><strong>At least 2 tools:</strong> Python REPL (for testing code) and web search (for looking up error messages or documentation)</li>
        <li><strong>Memory:</strong> <code>RunnableWithMessageHistory</code> so the user can have a multi-turn debugging conversation ("now fix the edge case where input is empty")</li>
        <li><strong>Reflection:</strong> After generating a fix, run a separate critique chain that evaluates the fix quality — then revise if needed</li>
        <li><strong>Callbacks:</strong> Attach a cost tracker that reports total tokens and estimated cost at the end of each execution</li>
      </ol>

      <h4 style="color: var(--earth); margin-top: 16px;">Test your agent with these bugs</h4>
      <div class="blocks-grid" style="margin-top: 8px;">
        <div class="block-card" style="border-left: 3px solid #fca5a5;">
          <h4>Bug 1: Off-by-one error</h4>
          <p><code>def get_last(lst): return lst[len(lst)]</code> — IndexError: list index out of range</p>
        </div>
        <div class="block-card" style="border-left: 3px solid #fcd34d;">
          <h4>Bug 2: Type error</h4>
          <p><code>def add(a, b): return a + b; add("5", 3)</code> — TypeError: can only concatenate str to str</p>
        </div>
        <div class="block-card" style="border-left: 3px solid #93c5fd;">
          <h4>Bug 3: Logic error</h4>
          <p>A function that's supposed to check if a number is prime but returns True for 1 and False for 2</p>
        </div>
        <div class="block-card" style="border-left: 3px solid #c4b5fd;">
          <h4>Bug 4: Missing import</h4>
          <p><code>data = json.loads('{"name": "test"}'); print(data["name"])</code> — NameError: name 'json' is not defined</p>
        </div>
      </div>
    </div>

    <div class="arch-diagram">
      <div class="title">PROJECT ARCHITECTURE</div>
      <div><span class="yellow">┌──────────────────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="highlight">USER INPUT</span>: buggy code + error message            <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬──────────────────────────────────┘</span></div>
      <div><span class="dim">                │</span></div>
      <div><span class="yellow">┌───────────────▼──────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="blue">REACT AGENT</span> (create_react_agent + AgentExecutor) <span class="yellow">│</span></div>
      <div><span class="yellow">│</span>  <span class="dim">Thought → Action → Observation loop</span>              <span class="yellow">│</span></div>
      <div><span class="yellow">└───────┬──────────────────┬───────────────────────┘</span></div>
      <div><span class="dim">        │                  │</span></div>
      <div><span class="dim">   ┌────▼──────────┐  ┌────▼──────────┐</span></div>
      <div><span class="dim">   │</span><span class="green"> Python REPL  </span><span class="dim">│  │</span><span class="purple"> Web Search   </span><span class="dim">│</span></div>
      <div><span class="dim">   │</span><span class="green"> (test fixes) </span><span class="dim">│  │</span><span class="purple"> (lookup docs)</span><span class="dim">│</span></div>
      <div><span class="dim">   └──────────────┘  └──────────────┘</span></div>
      <div><span class="dim">                │</span></div>
      <div><span class="yellow">┌───────────────▼──────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="orange">REFLECTION CHAIN</span> (critique → revise)             <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬──────────────────────────────────┘</span></div>
      <div><span class="dim">                │</span></div>
      <div><span class="yellow">┌───────────────▼──────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="highlight">OUTPUT</span>: fixed code + explanation + cost report    <span class="yellow">│</span></div>
      <div><span class="yellow">└──────────────────────────────────────────────────┘</span></div>
    </div>

    <div class="insight-box">
      <strong>Stretch goals:</strong> (1) Add a third tool that reads files from disk so the agent can debug multi-file projects. (2) Use <code>PydanticOutputParser</code> to structure the final output into a typed object: <code>DebugResult(fixed_code, root_cause, explanation, confidence, tokens_used)</code>. (3) Add a <code>with_fallbacks</code> wrapper so the agent degrades gracefully if the primary model is unavailable.
    </div>

  </div>
</div>

</div><!-- /day5 -->

<!-- ═══════════════════════════════════════════════
     MODULE SUMMARY
     ═══════════════════════════════════════════════ -->
<hr class="section-divider">

<h2 style="font-size: 22px; font-weight: 700; margin-bottom: 16px;">Module Summary — What You Now Know</h2>

<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LangChain's purpose</strong> — eliminates boilerplate by providing unified abstractions for LLM apps</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Ecosystem packages</strong> — langchain-core, langchain-openai, langchain-community, langsmith</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LLM wrappers</strong> — ChatOpenAI, ChatAnthropic, ChatOllama with a unified Runnable interface</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Model parameters</strong> — temperature, max_tokens, top_p and when to tune each</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Prompt templates</strong> — PromptTemplate, ChatPromptTemplate, FewShotPromptTemplate, MessagesPlaceholder</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Output parsers</strong> — StrOutputParser, JsonOutputParser, PydanticOutputParser, OutputFixingParser</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LCEL pipe syntax</strong> — compose chains with | operator; every component is a Runnable</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Runnable primitives</strong> — RunnablePassthrough, RunnableLambda, RunnableParallel, with_fallbacks</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Chain patterns</strong> — sequential, branching (fan-out/fan-in), fallback, and debugging</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Conversational memory</strong> — Buffer, Window, Summary strategies + RunnableWithMessageHistory</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Tools</strong> — @tool decorator, built-in tools (Tavily, Wikipedia, Python REPL), custom tools</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>ReAct agents</strong> — create_react_agent + AgentExecutor implementing the Thought/Action/Observation loop</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Callbacks & tracing</strong> — BaseCallbackHandler, LangSmith integration, verbose mode</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cost tracking</strong> — token counting, per-call cost estimation, budget guards</span></div>
</div>

<h3 style="font-size: 17px; margin-top: 24px; margin-bottom: 12px;">Check Your Understanding</h3>
<p style="font-size: 14px; margin-bottom: 8px;">Before moving to Unit 4, make sure you can answer:</p>
<ol style="padding-left: 20px; font-size: 14px; line-height: 1.8;">
  <li>What problem does LangChain solve that raw LLM SDKs don't? When would you NOT use LangChain?</li>
  <li>Explain the Runnable protocol. What four methods does every Runnable expose, and why is this useful?</li>
  <li>Write a chain from scratch using LCEL that: takes user input → formats a prompt → calls the LLM → parses JSON output. Which classes do you use for each step?</li>
  <li>Compare ConversationBufferMemory, ConversationBufferWindowMemory, and ConversationSummaryMemory. When would you choose each? What's the cost trade-off?</li>
  <li>How do you create a custom tool in LangChain? What makes a good tool description?</li>
  <li>Trace the execution of a ReAct agent through the Thought → Action → Observation loop. How does this connect to Unit 2's ReAct pattern?</li>
  <li>You have an agent that's costing $5 per run. Describe three specific techniques — using concepts from this unit — to reduce the cost by at least 50%.</li>
</ol>

<div style="margin-top: 24px; display: flex; gap: 12px; flex-wrap: wrap; justify-content: center;">
  <a href="/blog/2026/03/28/u2-agentic-ai-architecture-design-patterns/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gray-200); color: var(--gray-700); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    ← Unit 2
  </a>
  <a href="/courses/agentic-ai-engineering/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gum); color: var(--white); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    Course Overview
  </a>
  <a href="#" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gray-200); color: var(--gray-700); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    Unit 4 →
  </a>
</div>

</div><!-- /mod-page -->

<script>
function switchDay(n) {
  document.querySelectorAll('.day-tab').forEach(function(t, i) {
    t.classList.toggle('active', i === n - 1);
  });
  document.querySelectorAll('.day-panel').forEach(function(p, i) {
    p.classList.toggle('active', i === n - 1);
  });
  window.scrollTo({ top: document.querySelector('.day-tabs').offsetTop - 70, behavior: 'smooth' });
}
</script>
