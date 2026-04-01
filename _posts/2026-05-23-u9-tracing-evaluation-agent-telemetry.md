---
layout: default
title: "Unit 9 — Tracing, Evaluation & Agent Telemetry"
date: 2026-05-23
categories: [agentic-ai, production]
permalink: /blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/
description: "Instrument your agents with observability — trace every LLM call, evaluate outputs with automated scoring, track costs, and debug failures using Langfuse and LangSmith."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 9</span>
</nav>

<div class="mod-hero">
  <h1>Unit 9 — Tracing, Evaluation & Agent Telemetry</h1>
  <p class="mod-hero-sub">You can build agents. Now you need to <strong>see inside them</strong>. When an agent gives a wrong answer, which step failed? When costs spike, which tool call is expensive? When latency doubles, where's the bottleneck? This unit teaches you to instrument, monitor, and evaluate your agents in production using Langfuse and LangSmith.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track D · Production & Deployment</span>
    <span class="mod-pill time">⏱ ~8 hrs across 5 days (Week 11)</span>
    <span class="mod-pill hands">🛠 2 hands-on labs</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/05/16/u8-conversational-agent-networks-autogen/" style="color:var(--gum);">Unit 8 — AutoGen</a>. You should have built agents with multiple frameworks by now. This unit applies equally to LangChain, Phidata, CrewAI, and AutoGen agents.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Explain why observability matters for LLM applications (cost, quality, latency, debugging)</li>
    <li>Instrument a LangChain agent with Langfuse for full trace capture</li>
    <li>Navigate the Langfuse dashboard: traces, spans, generations, scores</li>
    <li>Set up automated evaluation: LLM-as-judge, heuristic scoring, human feedback</li>
    <li>Build a dataset of test cases and run batch evaluations</li>
    <li>Instrument with LangSmith: traces, datasets, annotation queues</li>
    <li>Compare Langfuse vs. LangSmith: features, pricing, self-hosting options</li>
    <li>Build a cost tracking dashboard and set up latency alerts</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">Langfuse</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">LangSmith</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Evaluation & Scoring</span>
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
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>Why observability matters — the case for tracing</h4><p>Two topics · ~1.5 hours · Cover: Observability fundamentals + the trace data model</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>The Observability Problem in AI Agents</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>Traditional software is deterministic: given the same input, you get the same output. Agents are stochastic: the same input can produce different outputs, different tool call sequences, and different costs. Without observability, you're flying blind.</p>

<h3>The four pillars of agent observability</h3>
<div class="blocks-grid">
  <div class="block-card"><h4>🔍 Tracing</h4><p>See the full execution path: which LLM was called, what prompt was sent, what tools were invoked, and in what order.</p></div>
  <div class="block-card"><h4>📊 Evaluation</h4><p>Score agent outputs: is the response correct? relevant? safe? Use automated scoring, LLM-as-judge, and human review.</p></div>
  <div class="block-card"><h4>💰 Cost tracking</h4><p>Token counts per call, per agent, per day. Identify expensive tool calls and optimise prompt length.</p></div>
  <div class="block-card"><h4>⏱ Latency monitoring</h4><p>Time per LLM call, per tool call, end-to-end. Identify bottlenecks and set latency SLAs.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">TRACE DATA MODEL</div>
  <div></div>
  <div><span class="highlight">Trace</span> <span class="dim">— one end-to-end agent invocation</span></div>
  <div>  <span class="dim">├──</span> <span class="blue">Span</span> <span class="dim">— a logical step (e.g., "research phase")</span></div>
  <div>  <span class="dim">│     ├──</span> <span class="green">Generation</span> <span class="dim">— one LLM call (prompt → response)</span></div>
  <div>  <span class="dim">│     │     input, output, model, tokens, latency, cost</span></div>
  <div>  <span class="dim">│     └──</span> <span class="green">Generation</span> <span class="dim">— another LLM call</span></div>
  <div>  <span class="dim">├──</span> <span class="blue">Span</span> <span class="dim">— "tool execution"</span></div>
  <div>  <span class="dim">│     └──</span> <span class="purple">Event</span> <span class="dim">— tool call: name, args, result, duration</span></div>
  <div>  <span class="dim">└──</span> <span class="orange">Score</span> <span class="dim">— evaluation result: accuracy=0.85, relevance=0.92</span></div>
</div>

<div class="insight-box"><strong>The debugging loop:</strong> User reports "bad answer" → You find the trace → You see the agent called the right tool but the retrieved document was irrelevant → You fix the retrieval logic → You verify with the same input → Score improves. Without tracing, you'd be guessing.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Think about your U5 RAG agent. List 5 things that could go wrong (wrong retrieval, hallucination, wrong tool, high latency, excessive cost).</li>
  <li>For each failure mode, identify which observability pillar would catch it.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>The Observability Landscape</h2><span class="topic-time">35 min</span></div>
<div class="topic-body">
<p>Several tools compete in the LLM observability space. This unit focuses on the two most mature options:</p>

<table class="cmp-table">
  <thead><tr><th>Feature</th><th>Langfuse</th><th>LangSmith</th></tr></thead>
  <tbody>
    <tr><td><strong>Maker</strong></td><td>Langfuse (open-source company)</td><td>LangChain (same company as the framework)</td></tr>
    <tr><td><strong>Open source</strong></td><td>Yes — self-host or use cloud</td><td>No — cloud only (managed service)</td></tr>
    <tr><td><strong>Framework support</strong></td><td>LangChain, LlamaIndex, OpenAI, any via SDK</td><td>LangChain native, others via API</td></tr>
    <tr><td><strong>Tracing</strong></td><td>Full traces with nested spans</td><td>Full traces with LangChain auto-instrumentation</td></tr>
    <tr><td><strong>Evaluation</strong></td><td>Built-in evaluators + custom scoring</td><td>Built-in evaluators + annotation queues</td></tr>
    <tr><td><strong>Datasets</strong></td><td>Upload test cases, run batch evaluations</td><td>Datasets + experiments + comparisons</td></tr>
    <tr><td><strong>Pricing</strong></td><td>Free tier, self-hosted is free forever</td><td>Free tier (5k traces/mo), paid plans</td></tr>
    <tr><td><strong>Best for</strong></td><td>Privacy-sensitive orgs, multi-framework setups</td><td>LangChain-heavy stacks, quick setup</td></tr>
  </tbody>
</table>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Create accounts on both Langfuse Cloud and LangSmith. Both have free tiers.</li>
  <li>Note your API keys for use in the upcoming labs.</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Lab 1 — Langfuse: instrument, trace, and evaluate</h4><p>One full lab · ~2 hours · Cover: Langfuse setup, tracing, scoring</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">L1</div><h2>Lab — Langfuse End-to-End</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">

<div class="lab-box"><h4>✏️ Step 1 — Integration Setup (20 min)</h4><ol>
  <li>Install: <code>pip install langfuse langchain-community</code></li>
  <li>Set environment variables: <code>LANGFUSE_PUBLIC_KEY</code>, <code>LANGFUSE_SECRET_KEY</code>, <code>LANGFUSE_HOST</code>.</li>
  <li>Create a simple LangChain agent (use the one from U3 or U5).</li>
  <li>Add the Langfuse callback handler:</li>
</ol></div>

<div class="arch-diagram">
  <div class="title">LANGFUSE + LANGCHAIN</div>
  <div><span class="purple">from</span> langfuse.callback <span class="purple">import</span> CallbackHandler</div>
  <div></div>
  <div>handler = CallbackHandler()</div>
  <div></div>
  <div><span class="dim"># Pass to any LangChain runnable</span></div>
  <div>result = agent.invoke(</div>
  <div>    {<span class="green">"input"</span>: <span class="green">"What's the latest on NVDA?"</span>},</div>
  <div>    config={<span class="green">"callbacks"</span>: [handler]},</div>
  <div>)</div>
  <div></div>
  <div>handler.flush()  <span class="dim"># ensure traces are sent</span></div>
</div>

<div class="lab-box"><h4>✏️ Step 2 — Explore the Dashboard (20 min)</h4><ol>
  <li>Open Langfuse Cloud. Navigate to the Traces view.</li>
  <li>Click on a trace. Explore: total duration, number of LLM calls, total tokens, cost estimate.</li>
  <li>Drill into a Generation: see the exact prompt, response, model, token counts.</li>
  <li>Find a tool call event. What arguments were passed? What was returned?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 3 — Add Custom Scores (30 min)</h4><ol>
  <li>Score a trace manually in the UI: add a "relevance" score of 0–1.</li>
  <li>Score programmatically using the Langfuse SDK:</li>
</ol></div>

<div class="arch-diagram">
  <div class="title">PROGRAMMATIC SCORING</div>
  <div><span class="purple">from</span> langfuse <span class="purple">import</span> Langfuse</div>
  <div></div>
  <div>lf = Langfuse()</div>
  <div></div>
  <div>lf.score(</div>
  <div>    trace_id=<span class="green">"trace-abc-123"</span>,</div>
  <div>    name=<span class="green">"accuracy"</span>,</div>
  <div>    value=<span class="yellow">0.85</span>,</div>
  <div>    comment=<span class="green">"Correct answer but missing one detail"</span>,</div>
  <div>)</div>
</div>

<div class="lab-box"><h4>✏️ Step 4 — LLM-as-Judge Evaluation (30 min)</h4><ol>
  <li>Write an evaluator prompt: "Given the question and the agent's answer, rate the accuracy from 0 to 1."</li>
  <li>Call GPT-4o-mini with this prompt for 10 traces. Store scores in Langfuse.</li>
  <li>Compare your manual scores with the LLM judge scores. How well do they correlate?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 5 — Dataset Evaluation (20 min)</h4><ol>
  <li>Create a dataset in Langfuse with 10 test cases (input + expected_output).</li>
  <li>Run your agent on all 10 test cases. Score each trace automatically.</li>
  <li>View the evaluation results: average score, worst-performing cases, patterns in failures.</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>Lab 2 — LangSmith: traces, datasets, and annotation</h4><p>One full lab · ~2 hours · Cover: LangSmith setup, experiments, annotation queues</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">L2</div><h2>Lab — LangSmith End-to-End</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">

<div class="lab-box"><h4>✏️ Step 1 — Integration Setup (15 min)</h4><ol>
  <li>Set environment variables: <code>LANGCHAIN_TRACING_V2=true</code>, <code>LANGCHAIN_API_KEY</code>.</li>
  <li>That's it — LangSmith auto-instruments all LangChain calls. No callback handler needed.</li>
  <li>Run your LangChain agent and verify traces appear in LangSmith.</li>
</ol></div>

<div class="arch-diagram">
  <div class="title">LANGSMITH AUTO-INSTRUMENTATION</div>
  <div><span class="purple">import</span> os</div>
  <div>os.environ[<span class="green">"LANGCHAIN_TRACING_V2"</span>] = <span class="green">"true"</span></div>
  <div>os.environ[<span class="green">"LANGCHAIN_API_KEY"</span>] = <span class="green">"ls_..."</span></div>
  <div></div>
  <div><span class="dim"># All LangChain calls are now automatically traced!</span></div>
  <div>result = agent.invoke({<span class="green">"input"</span>: <span class="green">"..."</span>})</div>
</div>

<div class="lab-box"><h4>✏️ Step 2 — Explore Traces (20 min)</h4><ol>
  <li>Open LangSmith dashboard. Navigate to your project's traces.</li>
  <li>Compare the trace visualisation with Langfuse. Note differences in UI and detail level.</li>
  <li>Find the most expensive trace. Find the slowest trace. Are they the same one?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 3 — Create a Dataset & Run Experiments (40 min)</h4><ol>
  <li>Create a dataset in LangSmith with the same 10 test cases you used in Langfuse.</li>
  <li>Run an experiment: execute your agent on all test cases and auto-evaluate.</li>
  <li>Use LangSmith's built-in evaluators: correctness, helpfulness, relevance.</li>
  <li>Compare experiment results across different models (gpt-4o-mini vs. gpt-4o).</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 4 — Annotation Queues (25 min)</h4><ol>
  <li>Create an annotation queue for human review.</li>
  <li>Send 5 traces to the queue. Open the annotation UI and score each one.</li>
  <li>LangSmith tracks annotator agreement — useful when multiple reviewers score the same traces.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 5 — Comparison (20 min)</h4><ol>
  <li>Create a table comparing your Langfuse and LangSmith experiences:</li>
  <li>Setup difficulty, trace quality, evaluation features, UI polish, pricing.</li>
  <li>Which would you recommend for: (a) a startup, (b) a privacy-sensitive enterprise, (c) a LangChain-only stack?</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Advanced evaluation — automated scoring pipelines</h4><p>Two topics · ~1.5 hours · Cover: Evaluation strategies + cost/latency dashboards</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Evaluation Strategy Design</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>Evaluation isn't one-size-fits-all. Different agent types need different evaluation strategies:</p>

<table class="cmp-table">
  <thead><tr><th>Agent Type</th><th>Key Metrics</th><th>Evaluation Method</th></tr></thead>
  <tbody>
    <tr><td><strong>RAG agent</strong></td><td>Faithfulness, relevance, recall</td><td>Compare answer against retrieved docs + ground truth</td></tr>
    <tr><td><strong>Code agent</strong></td><td>Correctness, executability</td><td>Run generated code, check output matches expected</td></tr>
    <tr><td><strong>Conversational agent</strong></td><td>Helpfulness, coherence, safety</td><td>LLM-as-judge + human review</td></tr>
    <tr><td><strong>Multi-agent crew</strong></td><td>Task completion, delegation efficiency</td><td>End-to-end output quality + intermediate trace analysis</td></tr>
  </tbody>
</table>

<h3>Three evaluation patterns</h3>
<div class="blocks-grid">
  <div class="block-card"><h4>🤖 LLM-as-Judge</h4><p>Use a strong model (GPT-4o) to evaluate a cheaper model's output. Fast, scalable, but can be biased.</p></div>
  <div class="block-card"><h4>📏 Heuristic scoring</h4><p>Rule-based: check for keywords, length, format, JSON validity. Cheap and deterministic.</p></div>
  <div class="block-card"><h4>👤 Human review</h4><p>Expert annotators score outputs. Gold standard but expensive and slow. Use for calibration.</p></div>
</div>

<div class="insight-box"><strong>The evaluation pyramid:</strong> Use heuristics for 100% coverage (fast, cheap), LLM-as-judge for 20% coverage (moderate cost), and human review for 5% coverage (slow, expensive). This gives you both breadth and depth.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Design an evaluation strategy for your U5 RAG agent. Which metrics matter most?</li>
  <li>Write a heuristic scorer: check if the response contains at least one URL citation.</li>
  <li>Write an LLM-as-judge prompt that evaluates faithfulness (does the answer match the retrieved docs?).</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">4</div><h2>Cost & Latency Dashboards</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>Both Langfuse and LangSmith track costs and latency. But for production monitoring, you often need custom dashboards.</p>

<div class="arch-diagram">
  <div class="title">COST TRACKING WITH LANGFUSE</div>
  <div><span class="purple">from</span> langfuse <span class="purple">import</span> Langfuse</div>
  <div></div>
  <div>lf = Langfuse()</div>
  <div></div>
  <div><span class="dim"># Fetch all traces from the last 24 hours</span></div>
  <div>traces = lf.fetch_traces(</div>
  <div>    limit=<span class="yellow">100</span>,</div>
  <div>    order_by=<span class="green">"timestamp"</span>,</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># Calculate total cost</span></div>
  <div>total_cost = sum(t.total_cost <span class="purple">for</span> t <span class="purple">in</span> traces.data <span class="purple">if</span> t.total_cost)</div>
  <div>print(f<span class="green">"Last 100 traces cost: ${total_cost:.4f}"</span>)</div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Fetch your last 50 traces from Langfuse. Calculate: total cost, average cost per trace, most expensive trace.</li>
  <li>Identify which model (gpt-4o vs. gpt-4o-mini) accounts for most of the cost.</li>
  <li>Set up a simple alert: if any single trace costs more than $0.10, log a warning.</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Putting it together — observability playbook</h4><p>One topic · ~1.5 hours · Cover: Production observability checklist + framework comparison</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">5</div><h2>The Production Observability Playbook</h2><span class="topic-time">75 min</span></div>
<div class="topic-body">
<p>You've learned Langfuse and LangSmith. Now let's synthesise everything into an actionable playbook for any agent you deploy.</p>

<h3>Pre-deployment checklist</h3>
<div class="blocks-grid">
  <div class="block-card"><h4>✅ Tracing enabled</h4><p>Every LLM call, tool call, and agent step is captured with timestamps, tokens, and costs.</p></div>
  <div class="block-card"><h4>✅ Evaluation dataset</h4><p>At least 20 test cases with expected outputs. Run automated evaluation before every deployment.</p></div>
  <div class="block-card"><h4>✅ Cost budget</h4><p>Set a per-trace cost limit. Alert if exceeded. Set a daily budget cap.</p></div>
  <div class="block-card"><h4>✅ Latency SLA</h4><p>Define acceptable end-to-end latency. Alert if P95 exceeds threshold.</p></div>
  <div class="block-card"><h4>✅ Error tracking</h4><p>Capture and categorise errors: API timeouts, tool failures, hallucination detections.</p></div>
  <div class="block-card"><h4>✅ Human review pipeline</h4><p>5% of traces go to annotation queue for human scoring. Use to calibrate automated evaluators.</p></div>
</div>

<h3>Framework decision matrix</h3>
<table class="cmp-table">
  <thead><tr><th>Scenario</th><th>Recommended Tool</th><th>Why</th></tr></thead>
  <tbody>
    <tr><td><strong>LangChain-only stack</strong></td><td>LangSmith</td><td>Zero-config auto-instrumentation, tight integration</td></tr>
    <tr><td><strong>Multi-framework (LC + Phidata + custom)</strong></td><td>Langfuse</td><td>Framework-agnostic SDK, works with anything</td></tr>
    <tr><td><strong>Privacy-sensitive (healthcare, finance)</strong></td><td>Langfuse self-hosted</td><td>Data never leaves your infrastructure</td></tr>
    <tr><td><strong>Rapid prototyping</strong></td><td>Either (both have free tiers)</td><td>Pick whichever has better UI for your workflow</td></tr>
    <tr><td><strong>Enterprise with SOC2 requirements</strong></td><td>Langfuse self-hosted or LangSmith Enterprise</td><td>Both offer enterprise compliance options</td></tr>
  </tbody>
</table>

<div class="lab-box"><h4>✏️ Final exercise</h4><ol>
  <li>Pick one agent you've built in this course (U3, U5, U6, or U7).</li>
  <li>Instrument it with both Langfuse and LangSmith simultaneously.</li>
  <li>Run 20 diverse queries. Score all traces with both automated and manual methods.</li>
  <li>Create a one-page observability report: average cost, P50/P95 latency, accuracy score, top 3 failure modes.</li>
  <li>Write a recommendation: which tool would you use in production and why?</li>
</ol></div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 9 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Four pillars</strong> — tracing, evaluation, cost tracking, latency monitoring</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Trace data model</strong> — traces → spans → generations → events → scores</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Langfuse</strong> — open-source, self-hostable, framework-agnostic</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LangSmith</strong> — LangChain-native, auto-instrumentation, annotation queues</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LLM-as-Judge</strong> — automated evaluation using a strong model</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Evaluation pyramid</strong> — heuristics (100%) + LLM judge (20%) + human (5%)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cost dashboards</strong> — per-trace, per-model, per-day cost tracking</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Production playbook</strong> — pre-deployment checklist for any agent</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>An agent's accuracy dropped from 90% to 70% overnight. Walk through how you'd diagnose the issue using traces.</li>
  <li>Compare the pros and cons of LLM-as-judge vs. human evaluation for a healthcare Q&A agent.</li>
  <li>Your agent costs $0.50 per query. The business needs it under $0.10. List 5 optimisation strategies.</li>
  <li>When would you choose self-hosted Langfuse over cloud Langfuse? What infrastructure do you need?</li>
  <li>Design an evaluation pipeline for a multi-agent CrewAI system. How do you score intermediate outputs?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/05/16/u8-conversational-agent-networks-autogen/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 8</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/23/u10-visual-low-code-agent-builders/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 10 →</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
