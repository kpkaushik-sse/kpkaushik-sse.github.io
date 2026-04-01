---
layout: default
title: "Unit 4 — Stateful Agent Workflows with LangGraph"
date: 2026-04-18
categories: [agentic-ai, orchestration]
permalink: /blog/2026/04/18/u4-stateful-agent-workflows-langgraph/
description: "Build production-grade agent workflows with LangGraph — master state machines, conditional branching, cycles, human-in-the-loop checkpoints, and multi-step agent orchestration."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}
.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}
.mod-breadcrumb a{color:var(--gum);text-decoration:none}
.mod-breadcrumb a:hover{color:var(--earth)}
.mod-hero{margin-bottom:32px}
.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}
.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}
.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}
.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}
.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}
.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}
.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}
.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}
.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}
.obj-card ul{list-style:none;padding:0}
.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}
.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}
.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}
.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}
.day-tab:hover{color:var(--gray-700)}
.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}
.day-panel{display:none;padding-top:24px}
.day-panel.active{display:block}
.topic-section{margin-bottom:36px}
.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}
.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}
.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}
.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}
.topic-body{padding-left:48px}
.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}
.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}
.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}
.insight-box strong{color:var(--gum-dark)}
.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}
@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}
.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}
.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}
.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}
.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}
.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}
.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}
.cmp-table tr:last-child td{border-bottom:none}
.cmp-table tr:hover td{background:rgba(84,100,20,.03)}
.step-flow{display:flex;flex-direction:column;gap:12px;margin:20px 0}
.step-card{background:var(--gray-900);border-radius:var(--radius-md);padding:20px 22px;color:var(--white);display:flex;gap:16px}
.step-num{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:700;flex-shrink:0}
.step-num.perceive{background:#6366f1;color:#fff}
.step-num.plan{background:#8b5cf6;color:#fff}
.step-num.act{background:var(--gum);color:#fff}
.step-num.learn{background:var(--earth);color:#fff}
.step-body{flex:1}
.step-label{font-size:11px;font-weight:600;text-transform:uppercase;letter-spacing:.5px;margin-bottom:2px}
.step-label.perceive{color:#a5b4fc}
.step-label.plan{color:#c4b5fd}
.step-label.act{color:#d9f99d}
.step-label.learn{color:#fed7aa}
.step-title{font-size:17px;font-weight:600;margin-bottom:6px}
.step-desc{font-size:13.5px;line-height:1.65;color:#d1d5db}
.step-tools{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap}
.tool-badge{padding:4px 10px;border-radius:4px;font-size:11px;font-weight:600}
.tool-badge.green{background:rgba(16,185,129,.2);color:#6ee7b7}
.tool-badge.red{background:rgba(239,68,68,.2);color:#fca5a5}
.tool-badge.blue{background:rgba(96,165,250,.2);color:#93c5fd}
.tool-badge.amber{background:rgba(245,158,11,.2);color:#fcd34d}
.tool-badge.purple{background:rgba(139,92,246,.2);color:#c4b5fd}
.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}
.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}
.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}
.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}
.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}
.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}
.lab-box ol,.lab-box ul{padding-left:20px}
.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}
.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}
.day-progress-fill{height:100%;background:var(--gum);border-radius:6px;transition:width .4s ease}
.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}
.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}
@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}
.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}
.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}
.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}
.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}
.arch-diagram .dim{color:#64748b}
.arch-diagram .green{color:#6ee7b7}
.arch-diagram .blue{color:#93c5fd}
.arch-diagram .purple{color:#c4b5fd}
.arch-diagram .yellow{color:#fcd34d}
.arch-diagram .red{color:#fca5a5}
.arch-diagram .orange{color:#fdba74}
.arch-diagram .highlight{color:#E0F82E;font-weight:600}
@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}.step-card{flex-direction:column;gap:10px}.sched-card{flex-direction:column;gap:6px}.sched-time{min-width:auto}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 4</span>
</nav>

<div class="mod-hero">
  <h1>Unit 4 — Stateful Agent Workflows with LangGraph</h1>
  <p class="mod-hero-sub">LangChain chains are linear — data flows in one direction. But real agents loop, branch, retry, and wait for human approval. LangGraph adds the missing piece: a graph-based state machine for building cyclic, stateful, production-grade agent workflows. In this unit you go from chains to graphs.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track B · Orchestration Toolkits</span>
    <span class="mod-pill time">⏱ ~12 hrs across 5 days (Weeks 5–6)</span>
    <span class="mod-pill hands">🛠 1 hands-on project</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/04/11/u3-chain-composition-langchain/" style="color:var(--gum);">Unit 3 — Chain Composition with LangChain</a> first. You need LCEL fluency, tool creation with @tool, and a working understanding of <code>create_react_agent</code> before diving into LangGraph.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Explain why chains are insufficient for complex agent workflows and when to switch to LangGraph</li>
    <li>Define a typed state schema using TypedDict and Annotated fields</li>
    <li>Build a StateGraph with nodes (functions) and edges (transitions) and compile it into a runnable</li>
    <li>Add conditional branching with <code>add_conditional_edges</code> to route execution based on state</li>
    <li>Create cyclic workflows where agents loop until a condition is met (the core of ReAct in LangGraph)</li>
    <li>Implement human-in-the-loop checkpoints that pause execution and wait for approval</li>
    <li>Persist state across runs using SQLite and PostgreSQL checkpointers</li>
    <li>Build a multi-step personal budget advisor agent with tool calls, state management, and human review</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">Graph-Based Agent Architecture</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">State Machines & Conditional Routing</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Human-in-the-Loop Workflows</span>
</div>

<!-- DAY TABS -->
<div class="day-tabs" role="tablist">
  <button class="day-tab active" onclick="switchDay(1)" role="tab">Day 1</button>
  <button class="day-tab" onclick="switchDay(2)" role="tab">Day 2</button>
  <button class="day-tab" onclick="switchDay(3)" role="tab">Day 3</button>
  <button class="day-tab" onclick="switchDay(4)" role="tab">Day 4</button>
  <button class="day-tab" onclick="switchDay(5)" role="tab">Day 5</button>
</div>

<!-- ═══════════════════════════════════════════
     DAY 1 — Why LangGraph & Core Concepts
     ═══════════════════════════════════════════ -->
<div id="day1" class="day-panel active">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 1 overview</div>
  <div class="sched-body">
    <h4>From chains to graphs — why linear pipelines hit a wall</h4>
    <p>Two topics · ~2.5 hours · Cover: Limitations of chains + LangGraph fundamentals</p>
  </div>
</div>

<!-- TOPIC 1 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">1</div>
    <h2>Why Chains Are Not Enough</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>In Unit 3 you built chains with LCEL — prompt → model → parser, piped together with <code>|</code>. These chains are powerful for linear workflows: summarise a document, translate it, format the output. But the moment your agent needs to <strong>loop</strong>, <strong>branch dynamically</strong>, or <strong>pause for human input</strong>, chains break down.</p>

    <p>Consider a customer support agent that needs to: (1) classify the issue, (2) if billing → check the account balance, (3) if technical → run diagnostics, (4) if the diagnostics fail → escalate to a human, (5) if the human approves → issue a refund. This workflow has <strong>conditional branches</strong>, <strong>cycles</strong> (retry diagnostics), and <strong>human checkpoints</strong>. You cannot express this as a linear pipe.</p>

    <h3>The five limitations of LCEL chains</h3>

    <table class="cmp-table">
      <thead><tr><th>Limitation</th><th>What Happens</th><th>LangGraph Solution</th></tr></thead>
      <tbody>
        <tr><td><strong>No cycles</strong></td><td>Data flows forward only. A ReAct loop (think → act → observe → repeat) can't be expressed natively.</td><td>Graphs allow edges that point backward — true cycles.</td></tr>
        <tr><td><strong>No conditional routing</strong></td><td>Every input goes through every step. You can't skip step 3 if step 2 says "no action needed."</td><td><code>add_conditional_edges</code> routes based on state values.</td></tr>
        <tr><td><strong>No persistent state</strong></td><td>Each <code>invoke()</code> starts fresh. The chain has no memory of what it did in the last iteration.</td><td>TypedDict state persists across all nodes within a run.</td></tr>
        <tr><td><strong>No checkpoints</strong></td><td>If the chain crashes at step 7 of 10, you start over from step 1.</td><td>Checkpointers save state after each node — resume from where it failed.</td></tr>
        <tr><td><strong>No human gates</strong></td><td>No built-in way to pause, show results to a human, and resume.</td><td>Interrupt nodes pause execution and yield state for human review.</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>The mental model:</strong> LCEL chains are like a factory conveyor belt — items move in one direction. LangGraph is like a city road network — traffic can take different routes, make U-turns, stop at traffic lights, and merge back together. Both are useful, but complex agents need the road network.
    </div>

    <h3>When to use chains vs. graphs</h3>
    <div class="blocks-grid">
      <div class="block-card" style="border-left:3px solid #93c5fd;">
        <h4>Use LCEL Chains When</h4>
        <p>Linear workflows: summarise → translate → format. Single LLM calls with parsing. ETL pipelines where data flows one way. Simple chatbots without complex routing.</p>
      </div>
      <div class="block-card" style="border-left:3px solid var(--gum);">
        <h4>Use LangGraph When</h4>
        <p>Agents that loop (ReAct). Multi-step workflows with branches. Human approval gates. Long-running tasks that need checkpointing. Multi-agent coordination.</p>
      </div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Take your ReAct agent from Unit 3 (Topic 8). List every place where it loops or makes a conditional decision.</li>
        <li>Try to draw the agent's execution as a directed graph on paper. Where do edges point backward? Where do edges branch?</li>
        <li>Write down 3 real-world agent scenarios where LCEL chains would fail. For each, explain which of the five limitations applies.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- TOPIC 2 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">2</div>
    <h2>LangGraph Fundamentals — Graphs, Nodes, Edges</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>LangGraph models agent workflows as <strong>directed graphs</strong> where nodes are functions and edges are transitions. Every graph has exactly one entry point (<code>START</code>), at least one exit point (<code>END</code>), and a shared <strong>state</strong> object that every node can read from and write to.</p>

    <p>The three core concepts are:</p>

    <div class="blocks-grid" style="grid-template-columns:repeat(3,1fr);">
      <div class="block-card">
        <h4>📋 State</h4>
        <p>A TypedDict that defines the shape of data flowing through the graph. Every node receives the full state, modifies some fields, and returns the updates.</p>
      </div>
      <div class="block-card">
        <h4>⚙️ Nodes</h4>
        <p>Python functions that do work: call an LLM, run a tool, check a condition, format output. Each node takes state as input and returns a partial state update.</p>
      </div>
      <div class="block-card">
        <h4>➡️ Edges</h4>
        <p>Transitions between nodes. Normal edges always fire. Conditional edges evaluate a function to decide which node runs next.</p>
      </div>
    </div>

    <h3>Your first LangGraph — a two-step workflow</h3>

    <div class="arch-diagram">
      <div class="title">MINIMAL LANGGRAPH EXAMPLE</div>
      <div><span class="purple">from</span> langgraph.graph <span class="purple">import</span> StateGraph, START, END</div>
      <div><span class="purple">from</span> typing <span class="purple">import</span> TypedDict</div>
      <div></div>
      <div><span class="dim"># 1. Define the state schema</span></div>
      <div><span class="blue">class</span> <span class="yellow">AgentState</span>(TypedDict):</div>
      <div>    messages: list[str]</div>
      <div>    current_step: str</div>
      <div></div>
      <div><span class="dim"># 2. Define node functions</span></div>
      <div><span class="blue">def</span> <span class="yellow">greet</span>(state: AgentState) -> dict:</div>
      <div>    <span class="purple">return</span> {<span class="green">"messages"</span>: state[<span class="green">"messages"</span>] + [<span class="green">"Hello!"</span>], <span class="green">"current_step"</span>: <span class="green">"greeted"</span>}</div>
      <div></div>
      <div><span class="blue">def</span> <span class="yellow">farewell</span>(state: AgentState) -> dict:</div>
      <div>    <span class="purple">return</span> {<span class="green">"messages"</span>: state[<span class="green">"messages"</span>] + [<span class="green">"Goodbye!"</span>], <span class="green">"current_step"</span>: <span class="green">"done"</span>}</div>
      <div></div>
      <div><span class="dim"># 3. Build the graph</span></div>
      <div>graph = StateGraph(AgentState)</div>
      <div>graph.add_node(<span class="green">"greet"</span>, greet)</div>
      <div>graph.add_node(<span class="green">"farewell"</span>, farewell)</div>
      <div></div>
      <div><span class="dim"># 4. Wire the edges</span></div>
      <div>graph.add_edge(START, <span class="green">"greet"</span>)</div>
      <div>graph.add_edge(<span class="green">"greet"</span>, <span class="green">"farewell"</span>)</div>
      <div>graph.add_edge(<span class="green">"farewell"</span>, END)</div>
      <div></div>
      <div><span class="dim"># 5. Compile and run</span></div>
      <div>app = graph.<span class="highlight">compile()</span></div>
      <div>result = app.invoke({<span class="green">"messages"</span>: [], <span class="green">"current_step"</span>: <span class="green">"start"</span>})</div>
      <div><span class="dim"># result["messages"] → ["Hello!", "Goodbye!"]</span></div>
    </div>

    <h3>Visualising the graph</h3>
    <p>LangGraph can render your workflow as a Mermaid diagram — incredibly useful for debugging complex graphs:</p>

    <div class="arch-diagram">
      <div class="title">GRAPH VISUALISATION</div>
      <div>print(app.get_graph().draw_mermaid())</div>
      <div></div>
      <div><span class="dim"># Output:</span></div>
      <div><span class="green">graph TD</span></div>
      <div><span class="green">    __start__ --> greet</span></div>
      <div><span class="green">    greet --> farewell</span></div>
      <div><span class="green">    farewell --> __end__</span></div>
    </div>

    <div class="insight-box">
      <strong>State updates are merged, not replaced.</strong> When a node returns <code>{"current_step": "greeted"}</code>, LangGraph merges this into the existing state — it doesn't overwrite the entire state object. Only the keys you return get updated. This is why nodes return partial dicts, not the full state.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Install LangGraph: <code>pip install langgraph</code></li>
        <li>Build the two-node graph above and run it. Print the final state.</li>
        <li>Add a third node called "ask_name" between greet and farewell. It should append "What's your name?" to messages.</li>
        <li>Use <code>get_graph().draw_mermaid()</code> to visualise your three-node graph.</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day1 -->

<!-- ═══════════════════════════════════════════
     DAY 2 — Conditional Edges & Cycles
     ═══════════════════════════════════════════ -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 2 overview</div>
  <div class="sched-body">
    <h4>Branching, routing, and looping — the three superpowers of graph-based agents</h4>
    <p>Two topics · ~2.5 hours · Cover: Conditional edges + Cyclic workflows (ReAct in LangGraph)</p>
  </div>
</div>

<!-- TOPIC 3 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">3</div>
    <h2>Conditional Edges — Dynamic Routing</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>Normal edges are static — node A always goes to node B. But real agents need to route dynamically: <em>if the customer issue is billing, go to the billing node; if it's technical, go to diagnostics; if it's a complaint, go to escalation.</em> This is what <code>add_conditional_edges</code> does.</p>

    <p>A conditional edge takes three arguments: (1) the source node, (2) a routing function that inspects the state and returns a string, and (3) a mapping from those strings to destination nodes.</p>

    <div class="arch-diagram">
      <div class="title">CONDITIONAL ROUTING EXAMPLE</div>
      <div><span class="blue">class</span> <span class="yellow">SupportState</span>(TypedDict):</div>
      <div>    issue_type: str</div>
      <div>    messages: list[str]</div>
      <div>    resolved: bool</div>
      <div></div>
      <div><span class="blue">def</span> <span class="yellow">classify</span>(state):</div>
      <div>    <span class="dim"># LLM classifies the issue</span></div>
      <div>    <span class="purple">return</span> {<span class="green">"issue_type"</span>: <span class="green">"billing"</span>}  <span class="dim"># or "technical" or "complaint"</span></div>
      <div></div>
      <div><span class="blue">def</span> <span class="yellow">route_issue</span>(state) -> str:</div>
      <div>    <span class="purple">return</span> state[<span class="green">"issue_type"</span>]  <span class="dim"># returns the key for the mapping</span></div>
      <div></div>
      <div><span class="dim"># Wire the conditional edge</span></div>
      <div>graph.add_conditional_edges(</div>
      <div>    <span class="green">"classify"</span>,       <span class="dim"># source node</span></div>
      <div>    route_issue,         <span class="dim"># routing function</span></div>
      <div>    {                    <span class="dim"># destination mapping</span></div>
      <div>        <span class="green">"billing"</span>:    <span class="green">"handle_billing"</span>,</div>
      <div>        <span class="green">"technical"</span>:  <span class="green">"run_diagnostics"</span>,</div>
      <div>        <span class="green">"complaint"</span>:  <span class="green">"escalate"</span>,</div>
      <div>    }</div>
      <div>)</div>
    </div>

    <h3>The routing function pattern</h3>
    <p>The routing function is the decision-maker. It receives the current state and returns a string key that maps to the next node. This function can be simple (check a field) or complex (call an LLM to decide):</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>📋 Field-based routing</h4>
        <p>Check a state field directly: <code>return state["issue_type"]</code>. Fast, deterministic, no LLM call needed. Use when the previous node already classified the input.</p>
      </div>
      <div class="block-card">
        <h4>🤖 LLM-based routing</h4>
        <p>Call an LLM inside the routing function. Useful when the routing decision requires language understanding. More expensive but more flexible.</p>
      </div>
    </div>

    <h3>Multi-branch graph walkthrough</h3>
    <p>Here's a complete support agent with three branches that merge back to a single response node:</p>

    <div class="arch-diagram">
      <div class="title">SUPPORT AGENT — CONDITIONAL BRANCHING</div>
      <div></div>
      <div><span class="yellow">         ┌─── handle_billing ───┐</span></div>
      <div><span class="yellow">         │                      │</span></div>
      <div><span class="green">START → classify</span> <span class="yellow">─── run_diagnostics ─── respond → END</span></div>
      <div><span class="yellow">         │                      │</span></div>
      <div><span class="yellow">         └──── escalate ────────┘</span></div>
      <div></div>
      <div><span class="dim">The classify node determines which branch to take.</span></div>
      <div><span class="dim">All three branches merge at the respond node.</span></div>
    </div>

    <div class="insight-box">
      <strong>Edge case handling:</strong> Always include a default route in your conditional mapping. If the routing function returns a value that doesn't exist in the mapping, LangGraph raises an error. Add a fallback: <code>"default": "handle_unknown"</code>.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a three-branch support agent graph as shown above. The classify node can return a hardcoded issue type for now.</li>
        <li>Test all three branches by changing the hardcoded issue type and verifying the correct branch executes.</li>
        <li>Replace the hardcoded classification with an LLM call using ChatOpenAI. The LLM should read the user's message from state and return "billing", "technical", or "complaint".</li>
        <li>Visualise the graph with <code>draw_mermaid()</code> and verify it matches the diagram above.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- TOPIC 4 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">4</div>
    <h2>Cyclic Workflows — The ReAct Loop in LangGraph</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>This is where LangGraph truly differentiates itself from LCEL. A <strong>cycle</strong> is an edge that points backward in the graph — node B routes back to node A. This is how you implement ReAct: the agent thinks, acts, observes, and if the task isn't done, it loops back to think again.</p>

    <p>In LCEL you'd rely on <code>AgentExecutor</code> to handle the loop internally, and you had no control over how many iterations to allow, what state to carry between iterations, or how to inject human input mid-loop. LangGraph makes the loop explicit — you see it in the graph, you control it with conditional edges, and you can interrupt it at any point.</p>

    <h3>The agent loop pattern</h3>

    <div class="arch-diagram">
      <div class="title">REACT LOOP IN LANGGRAPH</div>
      <div></div>
      <div><span class="green">START</span> → <span class="blue">agent</span> ──<span class="yellow">should_continue?</span>──┐</div>
      <div><span class="dim">          ↑                     │</span></div>
      <div><span class="dim">          │    ┌── "continue" ──┘</span></div>
      <div><span class="dim">          │    ↓</span></div>
      <div><span class="dim">          └── </span><span class="purple">tools</span></div>
      <div><span class="dim">               │</span></div>
      <div><span class="dim">          "end" → </span><span class="red">END</span></div>
      <div></div>
      <div><span class="dim">The agent node calls the LLM.</span></div>
      <div><span class="dim">If the LLM returns tool calls → route to the tools node.</span></div>
      <div><span class="dim">The tools node executes the tools and loops back to agent.</span></div>
      <div><span class="dim">If the LLM returns a final answer → route to END.</span></div>
    </div>

    <h3>Implementing the ReAct loop</h3>

    <div class="arch-diagram">
      <div class="title">REACT AGENT WITH LANGGRAPH</div>
      <div><span class="purple">from</span> langgraph.graph <span class="purple">import</span> StateGraph, START, END</div>
      <div><span class="purple">from</span> langgraph.prebuilt <span class="purple">import</span> ToolNode</div>
      <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> ChatOpenAI</div>
      <div></div>
      <div><span class="dim"># State includes the message history</span></div>
      <div><span class="blue">class</span> <span class="yellow">AgentState</span>(TypedDict):</div>
      <div>    messages: Annotated[list, add_messages]</div>
      <div></div>
      <div><span class="dim"># The agent node — calls the LLM with tools bound</span></div>
      <div>model = ChatOpenAI(model=<span class="green">"gpt-4o-mini"</span>).bind_tools(tools)</div>
      <div></div>
      <div><span class="blue">def</span> <span class="yellow">agent</span>(state):</div>
      <div>    response = model.invoke(state[<span class="green">"messages"</span>])</div>
      <div>    <span class="purple">return</span> {<span class="green">"messages"</span>: [response]}</div>
      <div></div>
      <div><span class="dim"># The routing function — check if agent wants to use tools</span></div>
      <div><span class="blue">def</span> <span class="yellow">should_continue</span>(state) -> str:</div>
      <div>    last = state[<span class="green">"messages"</span>][-<span class="yellow">1</span>]</div>
      <div>    <span class="purple">if</span> last.tool_calls:</div>
      <div>        <span class="purple">return</span> <span class="green">"continue"</span></div>
      <div>    <span class="purple">return</span> <span class="green">"end"</span></div>
      <div></div>
      <div><span class="dim"># Build the graph</span></div>
      <div>graph = StateGraph(AgentState)</div>
      <div>graph.add_node(<span class="green">"agent"</span>, agent)</div>
      <div>graph.add_node(<span class="green">"tools"</span>, ToolNode(tools))</div>
      <div></div>
      <div>graph.add_edge(START, <span class="green">"agent"</span>)</div>
      <div>graph.add_conditional_edges(<span class="green">"agent"</span>, should_continue, {</div>
      <div>    <span class="green">"continue"</span>: <span class="green">"tools"</span>,</div>
      <div>    <span class="green">"end"</span>: END,</div>
      <div>})</div>
      <div>graph.add_edge(<span class="green">"tools"</span>, <span class="green">"agent"</span>)  <span class="dim"># ← THE CYCLE</span></div>
      <div></div>
      <div>app = graph.compile()</div>
    </div>

    <p>Notice the key line: <code>graph.add_edge("tools", "agent")</code>. This creates the cycle — after executing tools, control flows back to the agent node, which calls the LLM again with the tool results. The LLM decides whether to call more tools or return a final answer.</p>

    <h3>Controlling loop iterations</h3>
    <p>Unbounded loops are dangerous (and expensive). LangGraph provides a <code>recursion_limit</code> parameter to cap the maximum number of node executions:</p>

    <div class="arch-diagram">
      <div class="title">RECURSION LIMIT</div>
      <div><span class="dim"># Maximum 25 node executions (not iterations — each node counts)</span></div>
      <div>result = app.invoke(</div>
      <div>    {<span class="green">"messages"</span>: [(<span class="green">"human"</span>, <span class="green">"What's the weather in Delhi?"</span>)]},</div>
      <div>    config={<span class="green">"recursion_limit"</span>: <span class="yellow">25</span>}</div>
      <div>)</div>
    </div>

    <div class="insight-box">
      <strong>Why LangGraph beats AgentExecutor for ReAct:</strong> With <code>AgentExecutor</code> from Unit 3, the loop was hidden — you couldn't inspect the state mid-loop, couldn't add extra logic between iterations, and couldn't persist state across failures. With LangGraph, every iteration is visible as a graph node, and you can add logging, human approval, or state mutation between any iteration.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build the ReAct agent loop shown above using a simple calculator tool and a web search tool from Unit 3.</li>
        <li>Ask the agent: "What is the population of India divided by the population of France?" — this requires two tool calls and one calculation.</li>
        <li>Add a <code>recursion_limit</code> of 5 and ask a question that would normally take 4+ iterations. What happens when the limit is hit?</li>
        <li>Add a print statement inside the <code>agent</code> node that logs the iteration number. Verify the loop count matches your expectation.</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day2 -->

<!-- ═══════════════════════════════════════════
     DAY 3 — State Management & Persistence
     ═══════════════════════════════════════════ -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 3 overview</div>
  <div class="sched-body">
    <h4>Typed state, reducers, and persistent checkpoints</h4>
    <p>Two topics · ~2.5 hours · Cover: Advanced state schemas + Checkpointers & persistence</p>
  </div>
</div>

<!-- TOPIC 5 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">5</div>
    <h2>Advanced State Schemas</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>The state schema isn't just a data container — it's the <strong>contract</strong> that every node in your graph adheres to. A well-designed state schema makes your graph predictable, debuggable, and maintainable. A poorly designed one leads to mysterious bugs where nodes overwrite each other's data.</p>

    <h3>Annotated fields and reducers</h3>
    <p>When two nodes both update the same field, LangGraph needs to know how to merge the updates. By default, the latest write wins. But for list fields (like messages), you usually want to <strong>append</strong>, not replace. This is what <strong>reducers</strong> do:</p>

    <div class="arch-diagram">
      <div class="title">STATE WITH REDUCERS</div>
      <div><span class="purple">from</span> typing <span class="purple">import</span> Annotated, TypedDict</div>
      <div><span class="purple">from</span> langgraph.graph.message <span class="purple">import</span> add_messages</div>
      <div></div>
      <div><span class="blue">class</span> <span class="yellow">AgentState</span>(TypedDict):</div>
      <div>    <span class="dim"># add_messages reducer: appends new messages instead of replacing</span></div>
      <div>    messages: Annotated[list, add_messages]</div>
      <div></div>
      <div>    <span class="dim"># No reducer: latest write wins (default)</span></div>
      <div>    current_step: str</div>
      <div></div>
      <div>    <span class="dim"># Custom reducer: always keep the higher value</span></div>
      <div>    confidence: Annotated[float, <span class="purple">lambda</span> old, new: max(old, new)]</div>
      <div></div>
      <div>    <span class="dim"># List reducer: concatenate lists</span></div>
      <div>    tool_results: Annotated[list, <span class="purple">lambda</span> old, new: old + new]</div>
    </div>

    <p>The <code>add_messages</code> reducer is the most important one. It handles message deduplication (by ID), ensures the conversation history grows correctly across loop iterations, and is the standard reducer for chat-based agents.</p>

    <h3>Designing state for complex agents</h3>
    <p>A well-structured state for a multi-step agent might look like this:</p>

    <div class="arch-diagram">
      <div class="title">REAL-WORLD STATE SCHEMA</div>
      <div><span class="blue">class</span> <span class="yellow">BudgetAdvisorState</span>(TypedDict):</div>
      <div>    <span class="dim"># Conversation</span></div>
      <div>    messages: Annotated[list, add_messages]</div>
      <div></div>
      <div>    <span class="dim"># User context</span></div>
      <div>    user_id: str</div>
      <div>    monthly_income: float</div>
      <div>    expense_categories: dict</div>
      <div></div>
      <div>    <span class="dim"># Workflow tracking</span></div>
      <div>    current_phase: str  <span class="dim"># "gathering" | "analysing" | "recommending"</span></div>
      <div>    analysis_complete: bool</div>
      <div></div>
      <div>    <span class="dim"># Tool outputs</span></div>
      <div>    tool_results: Annotated[list, <span class="purple">lambda</span> a, b: a + b]</div>
      <div></div>
      <div>    <span class="dim"># Human review</span></div>
      <div>    needs_approval: bool</div>
      <div>    approved: bool</div>
    </div>

    <div class="insight-box">
      <strong>State design principle:</strong> Include enough fields to make routing decisions without calling the LLM. If your conditional edge needs to check whether analysis is complete, store <code>analysis_complete: bool</code> in state rather than asking the LLM "is the analysis done?" every time. This saves tokens and latency.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Design a state schema for a job application agent that: collects resume data, searches job listings, matches skills, and drafts cover letters. Identify which fields need reducers.</li>
        <li>Implement the <code>add_messages</code> reducer. Create two nodes that each add a message, and verify the messages list grows correctly.</li>
        <li>Create a custom reducer that keeps a running average of confidence scores across iterations.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- TOPIC 6 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">6</div>
    <h2>Checkpointers & Persistent State</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>When a graph runs, LangGraph can save the state after every node execution. This snapshot is called a <strong>checkpoint</strong>. Checkpoints enable three critical capabilities: (1) resume from failures, (2) rewind to a previous state, and (3) pause for human review and resume later — even after the server restarts.</p>

    <h3>In-memory vs. persistent checkpointers</h3>

    <table class="cmp-table">
      <thead><tr><th>Checkpointer</th><th>Storage</th><th>Survives Restart?</th><th>Use Case</th></tr></thead>
      <tbody>
        <tr><td><strong>MemorySaver</strong></td><td>Python dict in RAM</td><td>No</td><td>Development, testing, short-lived demos</td></tr>
        <tr><td><strong>SqliteSaver</strong></td><td>SQLite file</td><td>Yes</td><td>Single-server production, prototypes</td></tr>
        <tr><td><strong>PostgresSaver</strong></td><td>PostgreSQL</td><td>Yes</td><td>Multi-server production, high availability</td></tr>
      </tbody>
    </table>

    <div class="arch-diagram">
      <div class="title">ADDING A CHECKPOINTER</div>
      <div><span class="purple">from</span> langgraph.checkpoint.memory <span class="purple">import</span> MemorySaver</div>
      <div></div>
      <div>checkpointer = MemorySaver()</div>
      <div>app = graph.compile(<span class="highlight">checkpointer=checkpointer</span>)</div>
      <div></div>
      <div><span class="dim"># Every invoke needs a thread_id to track the conversation</span></div>
      <div>config = {<span class="green">"configurable"</span>: {<span class="green">"thread_id"</span>: <span class="green">"user-123"</span>}}</div>
      <div></div>
      <div><span class="dim"># First message</span></div>
      <div>result = app.invoke({<span class="green">"messages"</span>: [(<span class="green">"human"</span>, <span class="green">"Hi!"</span>)]}, config)</div>
      <div></div>
      <div><span class="dim"># Second message — the graph remembers the first!</span></div>
      <div>result = app.invoke({<span class="green">"messages"</span>: [(<span class="green">"human"</span>, <span class="green">"What did I just say?"</span>)]}, config)</div>
      <div><span class="dim"># → The agent can see "Hi!" in the message history</span></div>
    </div>

    <h3>Browsing checkpoint history</h3>
    <p>You can inspect the full history of state snapshots for any thread:</p>

    <div class="arch-diagram">
      <div class="title">INSPECTING CHECKPOINTS</div>
      <div><span class="dim"># Get all saved states for a thread</span></div>
      <div><span class="purple">for</span> state <span class="purple">in</span> app.get_state_history(config):</div>
      <div>    print(f<span class="green">"Step: {state.metadata['step']}"</span>)</div>
      <div>    print(f<span class="green">"Node: {state.metadata.get('source', 'unknown')}"</span>)</div>
      <div>    print(f<span class="green">"Messages: {len(state.values['messages'])}"</span>)</div>
      <div>    print(<span class="green">"---"</span>)</div>
    </div>

    <div class="insight-box">
      <strong>Thread IDs are your session keys.</strong> Each <code>thread_id</code> represents an independent conversation. Two different thread IDs have completely separate state histories. Use the user's session ID or a unique conversation ID as the thread_id.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Add <code>MemorySaver</code> to your ReAct agent from Day 2. Have a multi-turn conversation and verify the agent remembers previous turns.</li>
        <li>Use <code>get_state_history()</code> to inspect all checkpoint snapshots. Count how many states were saved for a single conversation.</li>
        <li>Switch to <code>SqliteSaver</code>. Run a conversation, kill the Python process, restart it, and verify the agent can resume the thread.</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day3 -->

<!-- ═══════════════════════════════════════════
     DAY 4 — Human-in-the-Loop & Streaming
     ═══════════════════════════════════════════ -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 4 overview</div>
  <div class="sched-body">
    <h4>Pause, review, approve — adding humans to the agent loop</h4>
    <p>Two topics · ~2.5 hours · Cover: Human-in-the-loop interrupts + Streaming graph execution</p>
  </div>
</div>

<!-- TOPIC 7 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">7</div>
    <h2>Human-in-the-Loop Workflows</h2>
    <span class="topic-time">75 min</span>
  </div>
  <div class="topic-body">
    <p>Not every agent decision should be autonomous. Transferring money, sending emails, deleting data, approving refunds — these actions need human oversight. LangGraph's <strong>interrupt</strong> mechanism lets you pause the graph at any node, show the proposed action to a human, and resume only after approval.</p>

    <p>This directly implements the Human-in-the-Loop concept from Unit 1 and the Security Module from Unit 2. The agent does the reasoning and preparation; the human makes the final call.</p>

    <h3>The interrupt_before pattern</h3>
    <p>The simplest approach: tell LangGraph to pause execution before a specific node runs. The graph saves its state to the checkpointer and returns control to your application. When the human approves, you resume the graph from exactly where it stopped.</p>

    <div class="arch-diagram">
      <div class="title">INTERRUPT BEFORE A NODE</div>
      <div><span class="dim"># Compile with interrupt_before — pause before "execute_action"</span></div>
      <div>app = graph.compile(</div>
      <div>    checkpointer=MemorySaver(),</div>
      <div>    <span class="highlight">interrupt_before=["execute_action"]</span></div>
      <div>)</div>
      <div></div>
      <div><span class="dim"># First invoke — runs until it hits the interrupt</span></div>
      <div>result = app.invoke(input, config)</div>
      <div><span class="dim"># Graph pauses. result contains the proposed action in state.</span></div>
      <div></div>
      <div><span class="dim"># Show the proposed action to the human...</span></div>
      <div>state = app.get_state(config)</div>
      <div>print(f<span class="green">"Agent wants to: {state.values['proposed_action']}"</span>)</div>
      <div></div>
      <div><span class="dim"># Human approves → resume</span></div>
      <div>app.update_state(config, {<span class="green">"approved"</span>: <span class="yellow">True</span>})</div>
      <div>result = app.invoke(<span class="yellow">None</span>, config)  <span class="dim"># None = resume from checkpoint</span></div>
    </div>

    <h3>The three HITL patterns</h3>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num perceive">1</div>
        <div class="step-body">
          <div class="step-label perceive">APPROVE / REJECT</div>
          <div class="step-title">Gate a dangerous action</div>
          <div class="step-desc">The agent proposes an action (send email, transfer money). The graph pauses. The human reviews and either approves (resume) or rejects (update state with "rejected" and resume to handle the rejection).</div>
          <div class="step-tools">
            <span class="tool-badge green">interrupt_before</span>
            <span class="tool-badge blue">update_state</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">2</div>
        <div class="step-body">
          <div class="step-label plan">EDIT & RESUME</div>
          <div class="step-title">Correct the agent's work</div>
          <div class="step-desc">The agent drafts a response or plan. The graph pauses. The human edits the draft directly in the state, then resumes. The agent continues with the human-edited version.</div>
          <div class="step-tools">
            <span class="tool-badge purple">get_state</span>
            <span class="tool-badge amber">update_state</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">3</div>
        <div class="step-body">
          <div class="step-label act">PROVIDE INPUT</div>
          <div class="step-title">Supply missing information</div>
          <div class="step-desc">The agent reaches a point where it needs information only the human has (a password, a preference, a file). The graph pauses. The human provides the input via <code>update_state</code>, and the agent continues.</div>
          <div class="step-tools">
            <span class="tool-badge green">interrupt_before</span>
            <span class="tool-badge red">Human input</span>
          </div>
        </div>
      </div>
    </div>

    <div class="insight-box">
      <strong>Checkpointers are mandatory for HITL.</strong> Without a checkpointer, the graph cannot save its state when it pauses, and there's nothing to resume from. Always compile with a checkpointer when using <code>interrupt_before</code> or <code>interrupt_after</code>.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Modify your ReAct agent to pause before executing any tool call. Print the proposed tool and arguments to the console.</li>
        <li>Implement an approve/reject flow: if the human types "yes", resume; if "no", update the state to skip the tool and let the agent try a different approach.</li>
        <li>Implement the "edit & resume" pattern: pause after the agent drafts a response, let the human modify the draft, then send the edited version.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- TOPIC 8 -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">8</div>
    <h2>Streaming Graph Execution</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>In production, users don't want to wait 30 seconds for an agent to finish a 5-step workflow. They want to see progress: "Thinking... Searching... Found 3 results... Generating response..." LangGraph's streaming API gives you real-time visibility into graph execution.</p>

    <h3>Stream modes</h3>

    <table class="cmp-table">
      <thead><tr><th>Mode</th><th>What It Streams</th><th>Use Case</th></tr></thead>
      <tbody>
        <tr><td><strong>values</strong></td><td>Full state after each node</td><td>Progress tracking, UI updates</td></tr>
        <tr><td><strong>updates</strong></td><td>Only the state changes (delta) from each node</td><td>Efficient streaming where you only need the diff</td></tr>
        <tr><td><strong>messages</strong></td><td>LLM tokens as they're generated</td><td>Chat UIs with token-by-token display</td></tr>
      </tbody>
    </table>

    <div class="arch-diagram">
      <div class="title">STREAMING NODE-BY-NODE PROGRESS</div>
      <div><span class="purple">for</span> event <span class="purple">in</span> app.stream(input, config, stream_mode=<span class="green">"values"</span>):</div>
      <div>    current_node = event.get(<span class="green">"current_step"</span>, <span class="green">"unknown"</span>)</div>
      <div>    msg_count = len(event.get(<span class="green">"messages"</span>, []))</div>
      <div>    print(f<span class="green">"[{current_node}] Messages so far: {msg_count}"</span>)</div>
      <div></div>
      <div><span class="dim"># Output:</span></div>
      <div><span class="dim"># [agent] Messages so far: 2</span></div>
      <div><span class="dim"># [tools] Messages so far: 3</span></div>
      <div><span class="dim"># [agent] Messages so far: 4</span></div>
      <div><span class="dim"># [agent] Messages so far: 5  (final answer)</span></div>
    </div>

    <div class="arch-diagram">
      <div class="title">STREAMING LLM TOKENS</div>
      <div><span class="purple">async for</span> event <span class="purple">in</span> app.astream_events(input, config, version=<span class="green">"v2"</span>):</div>
      <div>    <span class="purple">if</span> event[<span class="green">"event"</span>] == <span class="green">"on_chat_model_stream"</span>:</div>
      <div>        chunk = event[<span class="green">"data"</span>][<span class="green">"chunk"</span>]</div>
      <div>        print(chunk.content, end=<span class="green">""</span>, flush=<span class="yellow">True</span>)</div>
    </div>

    <div class="insight-box">
      <strong>Streaming + HITL together:</strong> In a web app, you stream node progress to the frontend. When the graph hits an interrupt, you stream the paused state to the UI, show an approval button, and when the user clicks approve, you resume streaming. This creates a smooth, interactive experience.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Use <code>stream_mode="values"</code> on your ReAct agent and print the current node name after each step.</li>
        <li>Use <code>astream_events</code> to stream LLM tokens in real time. Build a simple terminal chat that shows tokens as they arrive.</li>
        <li>Combine streaming with HITL: stream progress, pause at the tool execution node, wait for input, then resume streaming.</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day4 -->

<!-- ═══════════════════════════════════════════
     DAY 5 — Project: Personal Budget Advisor
     ═══════════════════════════════════════════ -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 5 overview</div>
  <div class="sched-body">
    <h4>Put it all together — build a multi-step budget advisor with LangGraph</h4>
    <p>One project · ~3 hours · Combines: state management, conditional routing, cycles, tools, HITL, streaming</p>
  </div>
</div>

<!-- PROJECT -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background:var(--earth);">P</div>
    <h2>Project — Personal Budget Advisor Agent</h2>
    <span class="topic-time">3 hrs</span>
  </div>
  <div class="topic-body">
    <p>Build a complete personal budget advisor agent that demonstrates every LangGraph concept from this unit. The agent helps users analyse their spending, set budget goals, and get actionable recommendations — with human approval before any major changes.</p>

    <h3>Project architecture</h3>

    <div class="arch-diagram">
      <div class="title">BUDGET ADVISOR — GRAPH ARCHITECTURE</div>
      <div></div>
      <div><span class="green">START</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="blue">gather_info</span> <span class="dim">← Collects income, expenses, goals via conversation</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="yellow">is_info_complete?</span> ─── <span class="red">No</span> ──→ <span class="blue">ask_followup</span> ──→ <span class="blue">gather_info</span> <span class="dim">(cycle)</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="green">Yes</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="purple">analyse_spending</span> <span class="dim">← Categorises expenses, calculates ratios</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="purple">generate_plan</span> <span class="dim">← Creates a personalised budget plan</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="orange">⏸ HUMAN REVIEW</span> <span class="dim">← interrupt_before: user reviews the plan</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="yellow">approved?</span> ─── <span class="red">No</span> ──→ <span class="purple">revise_plan</span> ──→ <span class="orange">⏸ HUMAN REVIEW</span> <span class="dim">(cycle)</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="green">Yes</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="green">present_final</span> <span class="dim">← Formats and delivers the approved plan</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="red">END</span></div>
    </div>

    <h3>Phase 1 — State schema & basic graph (45 min)</h3>
    <div class="lab-box">
      <h4>✏️ Tasks</h4>
      <ol>
        <li>Define <code>BudgetAdvisorState</code> with fields: messages (with add_messages), user_income, expenses (dict), goals (list), info_complete (bool), analysis (dict), budget_plan (str), approved (bool).</li>
        <li>Create the <code>gather_info</code> node. It calls an LLM with a system prompt that asks about income, expenses, and financial goals. Parse the response and update state.</li>
        <li>Create the <code>is_info_complete</code> routing function. Check if income, expenses, and goals are all populated.</li>
        <li>Wire the gather → check → ask_followup cycle. Test with 3 rounds of conversation.</li>
      </ol>
    </div>

    <h3>Phase 2 — Analysis & plan generation (45 min)</h3>
    <div class="lab-box">
      <h4>✏️ Tasks</h4>
      <ol>
        <li>Create the <code>analyse_spending</code> node. Calculate: expense-to-income ratio, top 3 spending categories, potential savings areas. Store as a dict in state.</li>
        <li>Create a <code>@tool</code> for "calculate_50_30_20" that applies the 50/30/20 budgeting rule (50% needs, 30% wants, 20% savings) to the user's income.</li>
        <li>Create the <code>generate_plan</code> node. Call the LLM with the analysis results and the 50/30/20 breakdown. Generate a personalised budget plan as formatted text.</li>
      </ol>
    </div>

    <h3>Phase 3 — Human review loop (45 min)</h3>
    <div class="lab-box">
      <h4>✏️ Tasks</h4>
      <ol>
        <li>Add <code>interrupt_before=["present_final"]</code> to the compile step. Print the proposed budget plan when the interrupt fires.</li>
        <li>Implement the approve/reject flow: if approved, continue to present_final; if rejected, call <code>revise_plan</code> which asks the LLM to adjust based on feedback.</li>
        <li>Add streaming with <code>stream_mode="values"</code> so the user sees progress: "Gathering info... Analysing spending... Generating plan... Awaiting your review..."</li>
        <li>Use <code>MemorySaver</code> so the conversation persists across multiple invoke() calls.</li>
      </ol>
    </div>

    <h3>Phase 4 — Polish & test (45 min)</h3>
    <div class="lab-box">
      <h4>✏️ Tasks</h4>
      <ol>
        <li>Test the full flow end-to-end: start a conversation, provide income and expenses, review the plan, reject once with feedback, approve the revised plan.</li>
        <li>Use <code>get_graph().draw_mermaid()</code> to generate the full graph diagram and verify it matches the architecture above.</li>
        <li>Add error handling: what if the user provides invalid numbers? What if the LLM hallucinates expense categories?</li>
        <li>Add a <code>recursion_limit</code> and test what happens when the info-gathering loop cycles too many times.</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day5 -->

<!-- ═══════════════════════════════════════════
     MODULE SUMMARY
     ═══════════════════════════════════════════ -->
<hr class="section-divider">

<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 4 — Summary</h2>

<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Chains vs. graphs</strong> — chains are linear; graphs support cycles, branches, and interrupts</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>StateGraph</strong> — nodes (functions), edges (transitions), shared TypedDict state</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Conditional edges</strong> — routing function inspects state and returns destination key</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cyclic workflows</strong> — edges that point backward create the agent loop (ReAct in LangGraph)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>State reducers</strong> — Annotated fields with add_messages, custom merge functions</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Checkpointers</strong> — MemorySaver, SqliteSaver, PostgresSaver for persistence</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Human-in-the-loop</strong> — interrupt_before, update_state, approve/reject/edit patterns</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Streaming</strong> — values, updates, messages modes for real-time UI progress</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Recursion limits</strong> — cap node executions to prevent runaway loops</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Graph visualisation</strong> — draw_mermaid() for debugging and documentation</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>Why can't LCEL chains implement a ReAct loop natively? What specific graph feature enables it?</li>
  <li>Explain the difference between a normal edge and a conditional edge. When would you use each?</li>
  <li>What is a reducer, and why is <code>add_messages</code> essential for chat-based agents?</li>
  <li>Design a checkpoint strategy for a production agent that handles 10,000 concurrent conversations. Which checkpointer and why?</li>
  <li>Compare the three HITL patterns (approve/reject, edit & resume, provide input). Give a real-world scenario for each.</li>
  <li>You have an agent that sometimes loops forever. Describe two mechanisms to prevent this.</li>
  <li>How would you combine LangGraph streaming with a React frontend to show real-time agent progress?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/04/11/u3-chain-composition-langchain/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 3</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/04/25/u5-retrieval-augmented-agent-pipelines/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 5 →</a>
</div>

</div><!-- /mod-page -->

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
