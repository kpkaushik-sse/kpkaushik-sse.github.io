---
layout: default
title: "Unit 7 — Coordinated Agent Teams with CrewAI"
date: 2026-05-09
categories: [agentic-ai, specialized-agents]
permalink: /blog/2026/05/09/u7-coordinated-agent-teams-crewai/
description: "Design multi-agent crews with CrewAI — define agents with roles and backstories, wire sequential and hierarchical task workflows, share context via delegation, and build real production crews."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 7</span>
</nav>

<div class="mod-hero">
  <h1>Unit 7 — Coordinated Agent Teams with CrewAI</h1>
  <p class="mod-hero-sub">CrewAI models multi-agent collaboration the way real teams work: each agent has a <strong>role</strong>, a <strong>goal</strong>, and a <strong>backstory</strong>. Agents collaborate through sequential or hierarchical task processes, share context, delegate subtasks, and produce structured outputs. This unit teaches you to design, wire, and run production crews.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track C · Collaborative & Specialized Agents</span>
    <span class="mod-pill time">⏱ ~10 hrs across 5 days (Week 9)</span>
    <span class="mod-pill hands">🛠 2 hands-on projects</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/05/02/u6-rapid-agent-prototyping-phidata/" style="color:var(--gum);">Unit 6 — Phidata</a>. You've seen single-agent deployment; now you'll graduate to true multi-agent orchestration.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Define agents with role, goal, backstory, and tool access</li>
    <li>Create tasks with descriptions, expected outputs, and assigned agents</li>
    <li>Wire agents into sequential processes (assembly line) and hierarchical processes (manager delegates)</li>
    <li>Enable agent delegation so agents can autonomously ask other agents for help</li>
    <li>Build custom CrewAI tools with the @tool decorator</li>
    <li>Use CrewAI's memory system: short-term, long-term, and entity memory</li>
    <li>Handle structured outputs with Pydantic models on tasks</li>
    <li>Debug crews with verbose logging, step callbacks, and task callbacks</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">CrewAI Agents & Tasks</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Sequential & Hierarchical Processes</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Delegation & Memory</span>
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
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>CrewAI fundamentals — agents, tasks, and crews</h4><p>Two topics · ~2 hours · Cover: Core concepts + first crew</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>The CrewAI Mental Model</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">
<p>CrewAI borrows from real-world team management. Think of it as hiring a team: you define who's on the team (Agents), what they need to accomplish (Tasks), and how they work together (Process). The Crew ties everything together and kicks off execution.</p>

<div class="blocks-grid">
  <div class="block-card"><h4>👤 Agent</h4><p>A persona with a role, goal, backstory, and optionally tools. The backstory gives the LLM context for how to behave — like a job description.</p></div>
  <div class="block-card"><h4>📋 Task</h4><p>A unit of work with a description, expected_output, and agent assignment. Tasks can also specify output_pydantic for structured results.</p></div>
  <div class="block-card"><h4>⚙️ Process</h4><p>How tasks are executed: <strong>sequential</strong> (one after another) or <strong>hierarchical</strong> (manager delegates to workers).</p></div>
  <div class="block-card"><h4>🚀 Crew</h4><p>The orchestrator that combines agents, tasks, and process. Call crew.kickoff() to start execution.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">CREWAI — CORE ARCHITECTURE</div>
  <div></div>
  <div>  <span class="green">Crew</span></div>
  <div>  <span class="dim">├──</span> <span class="blue">agents:</span> [Agent_1, Agent_2, Agent_3]</div>
  <div>  <span class="dim">├──</span> <span class="purple">tasks:</span>  [Task_A, Task_B, Task_C]</div>
  <div>  <span class="dim">├──</span> <span class="yellow">process:</span> sequential <span class="dim">│</span> hierarchical</div>
  <div>  <span class="dim">└──</span> <span class="orange">memory:</span> <span class="yellow">True</span></div>
  <div></div>
  <div>  <span class="dim">Sequential flow:</span></div>
  <div>  Task_A <span class="dim">→</span> <span class="blue">Agent_1</span> <span class="dim">→ output →</span> Task_B <span class="dim">→</span> <span class="purple">Agent_2</span> <span class="dim">→ output →</span> Task_C <span class="dim">→</span> <span class="orange">Agent_3</span></div>
  <div></div>
  <div>  <span class="dim">Hierarchical flow:</span></div>
  <div>  <span class="highlight">Manager</span> <span class="dim">→ delegates →</span> <span class="blue">Agent_1</span> <span class="dim">or</span> <span class="purple">Agent_2</span> <span class="dim">or</span> <span class="orange">Agent_3</span></div>
  <div>  <span class="dim">           ← receives results ← agents</span></div>
</div>

<div class="insight-box"><strong>CrewAI vs. Phidata teams:</strong> Phidata's team feature lets a lead agent call sub-agents as tools. CrewAI takes a deeper approach: agents have personas (backstories), tasks have expected outputs, and the process defines the collaboration pattern. CrewAI is better when you need predictable multi-step workflows with clear handoffs.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Install CrewAI: <code>pip install crewai crewai-tools</code></li>
  <li>Read the CrewAI docs: identify the four core classes (Agent, Task, Crew, Process).</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>Your First Crew — Research & Write</h2><span class="topic-time">60 min</span></div>
<div class="topic-body">
<p>The classic CrewAI demo: a two-agent crew where a Researcher finds information and a Writer turns it into a polished article. The sequential process ensures the Writer waits for the Researcher's output.</p>

<div class="arch-diagram">
  <div class="title">RESEARCH & WRITE CREW</div>
  <div><span class="purple">from</span> crewai <span class="purple">import</span> Agent, Task, Crew, Process</div>
  <div><span class="purple">from</span> crewai_tools <span class="purple">import</span> SerperDevTool</div>
  <div></div>
  <div>search = SerperDevTool()</div>
  <div></div>
  <div>researcher = Agent(</div>
  <div>    role=<span class="green">"Senior Research Analyst"</span>,</div>
  <div>    goal=<span class="green">"Find comprehensive, accurate information on the given topic"</span>,</div>
  <div>    backstory=<span class="green">"You are a veteran research analyst at a top consulting firm. "</span></div>
  <div>             <span class="green">"You are known for thorough analysis and finding non-obvious insights."</span>,</div>
  <div>    tools=[search],</div>
  <div>    verbose=<span class="yellow">True</span>,</div>
  <div>)</div>
  <div></div>
  <div>writer = Agent(</div>
  <div>    role=<span class="green">"Content Strategist"</span>,</div>
  <div>    goal=<span class="green">"Transform research into engaging, well-structured articles"</span>,</div>
  <div>    backstory=<span class="green">"You are a seasoned tech writer who makes complex topics accessible."</span>,</div>
  <div>    verbose=<span class="yellow">True</span>,</div>
  <div>)</div>
  <div></div>
  <div>research_task = Task(</div>
  <div>    description=<span class="green">"Research the current state of AI agent frameworks in 2026."</span>,</div>
  <div>    expected_output=<span class="green">"A detailed summary with key players, trends, and comparisons."</span>,</div>
  <div>    agent=researcher,</div>
  <div>)</div>
  <div></div>
  <div>write_task = Task(</div>
  <div>    description=<span class="green">"Write a 500-word article based on the research findings."</span>,</div>
  <div>    expected_output=<span class="green">"A polished blog post in markdown format."</span>,</div>
  <div>    agent=writer,</div>
  <div>)</div>
  <div></div>
  <div>crew = Crew(</div>
  <div>    agents=[researcher, writer],</div>
  <div>    tasks=[research_task, write_task],</div>
  <div>    process=Process.<span class="highlight">sequential</span>,</div>
  <div>    verbose=<span class="yellow">True</span>,</div>
  <div>)</div>
  <div></div>
  <div>result = crew.kickoff()</div>
  <div>print(result)</div>
</div>

<p>Notice how the Writer's task doesn't explicitly receive the Researcher's output — CrewAI automatically passes the output of each task to the next task in a sequential process. This is the "assembly line" pattern.</p>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build the research & write crew above. Run it and inspect the verbose output.</li>
  <li>Add a third agent — an Editor — that proofs the article. Add an editing task at the end.</li>
  <li>Change the topic to something technical (e.g., "RAG vs. fine-tuning") and run again.</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Hierarchical process & delegation</h4><p>Two topics · ~2 hours · Cover: Manager-based routing + agent delegation</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Hierarchical Process — The Manager Pattern</h2><span class="topic-time">55 min</span></div>
<div class="topic-body">
<p>Sequential processes work when tasks have a clear order. But what if the order depends on the input? In a hierarchical process, CrewAI creates a virtual Manager agent that reads all tasks, decides which agent should handle each one, and coordinates the flow dynamically.</p>

<div class="arch-diagram">
  <div class="title">HIERARCHICAL CREW</div>
  <div>crew = Crew(</div>
  <div>    agents=[researcher, writer, analyst],</div>
  <div>    tasks=[research_task, analysis_task, write_task],</div>
  <div>    process=Process.<span class="highlight">hierarchical</span>,</div>
  <div>    manager_llm=<span class="green">"gpt-4o"</span>,  <span class="dim"># use a smart model for the manager</span></div>
  <div>    verbose=<span class="yellow">True</span>,</div>
  <div>)</div>
</div>

<table class="cmp-table">
  <thead><tr><th>Feature</th><th>Sequential</th><th>Hierarchical</th></tr></thead>
  <tbody>
    <tr><td><strong>Task order</strong></td><td>Fixed (list order)</td><td>Dynamic (manager decides)</td></tr>
    <tr><td><strong>Context sharing</strong></td><td>Previous task output → next task</td><td>Manager routes context to relevant agents</td></tr>
    <tr><td><strong>Best for</strong></td><td>Linear pipelines (research→write→edit)</td><td>Complex requests needing flexible routing</td></tr>
    <tr><td><strong>Cost</strong></td><td>Lower (no manager LLM calls)</td><td>Higher (manager makes extra LLM calls)</td></tr>
    <tr><td><strong>Predictability</strong></td><td>High (always same order)</td><td>Medium (manager may route differently)</td></tr>
  </tbody>
</table>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Convert your research & write crew to hierarchical. Compare the execution logs.</li>
  <li>Ask a question that could go to either agent first. Does the manager route it correctly?</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">4</div><h2>Agent Delegation — Agents Asking Agents for Help</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>CrewAI supports <strong>delegation</strong>: an agent can decide mid-task that it needs help from another agent and delegate a subtask. This is different from the manager pattern — here, any agent can request help from any other agent.</p>

<div class="arch-diagram">
  <div class="title">DELEGATION IN ACTION</div>
  <div>researcher = Agent(</div>
  <div>    role=<span class="green">"Researcher"</span>,</div>
  <div>    goal=<span class="green">"Find information"</span>,</div>
  <div>    backstory=<span class="green">"..."</span>,</div>
  <div>    <span class="highlight">allow_delegation=True</span>,  <span class="dim"># can ask other agents for help</span></div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># When the researcher encounters a financial question it can't</span></div>
  <div><span class="dim"># handle, it can delegate to the analyst agent automatically.</span></div>
</div>

<div class="insight-box"><strong>Delegation hazard:</strong> Agents can get into delegation loops — Agent A asks Agent B, who asks Agent A. Use <code>max_iter</code> on agents or <code>max_rpm</code> on the crew to prevent runaway loops. Also set clear backstories so agents know what they should and shouldn't delegate.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Enable delegation on the researcher. Send a query with a financial component. Watch the researcher delegate to the analyst.</li>
  <li>Disable delegation and run the same query. Compare the outputs — is the quality different?</li>
  <li>Intentionally create a delegation loop and observe how <code>max_iter</code> catches it.</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>Custom tools, memory, and structured outputs</h4><p>Three topics · ~2 hours · Cover: Tool creation + memory system + Pydantic outputs</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">5</div><h2>Building Custom Tools</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>CrewAI ships with built-in tools (web search, file read, scraping), but you'll often need custom tools for your specific domain — CRM lookups, database queries, API calls, etc.</p>

<div class="arch-diagram">
  <div class="title">CUSTOM TOOL — TWO PATTERNS</div>
  <div><span class="dim"># Pattern 1: @tool decorator (simple)</span></div>
  <div><span class="purple">from</span> crewai_tools <span class="purple">import</span> tool</div>
  <div></div>
  <div><span class="blue">@tool</span>(<span class="green">"Company Lookup"</span>)</div>
  <div><span class="blue">def</span> <span class="yellow">company_lookup</span>(name: str) -> str:</div>
  <div>    <span class="green">"""Look up company details by name in our CRM."""</span></div>
  <div>    <span class="dim"># your CRM API call here</span></div>
  <div>    <span class="purple">return</span> f<span class="green">"Company: {name}, Industry: Tech, Size: 500+"</span></div>
  <div></div>
  <div><span class="dim"># Pattern 2: BaseTool class (advanced)</span></div>
  <div><span class="purple">from</span> crewai_tools <span class="purple">import</span> BaseTool</div>
  <div></div>
  <div><span class="blue">class</span> <span class="yellow">DatabaseQuery</span>(BaseTool):</div>
  <div>    name: str = <span class="green">"Database Query"</span></div>
  <div>    description: str = <span class="green">"Execute a read-only SQL query"</span></div>
  <div></div>
  <div>    <span class="blue">def</span> <span class="yellow">_run</span>(self, query: str) -> str:</div>
  <div>        <span class="dim"># execute query, return results</span></div>
  <div>        <span class="purple">return</span> <span class="green">"query results..."</span></div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Create a custom tool that reads a local JSON file and returns the content.</li>
  <li>Create a tool that calls a public API (e.g., OpenWeatherMap) and returns weather data.</li>
  <li>Assign both tools to an agent and run queries that require each tool.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">6</div><h2>CrewAI Memory System</h2><span class="topic-time">35 min</span></div>
<div class="topic-body">
<p>CrewAI includes a three-layer memory system that helps agents learn from past interactions:</p>

<div class="blocks-grid">
  <div class="block-card"><h4>💾 Short-term memory</h4><p>Conversation context within the current crew execution. Automatically managed.</p></div>
  <div class="block-card"><h4>📚 Long-term memory</h4><p>Persists across executions. Agents remember insights from previous runs.</p></div>
  <div class="block-card"><h4>🏷️ Entity memory</h4><p>Tracks named entities (people, companies, products) across interactions.</p></div>
  <div class="block-card"><h4>🧠 User memory</h4><p>Stores information about specific users for personalised responses.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">ENABLE MEMORY</div>
  <div>crew = Crew(</div>
  <div>    agents=[researcher, writer],</div>
  <div>    tasks=[research_task, write_task],</div>
  <div>    <span class="highlight">memory=True</span>,  <span class="dim"># enables all memory layers</span></div>
  <div>    verbose=<span class="yellow">True</span>,</div>
  <div>)</div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Enable memory on your crew. Run a research task about a specific company.</li>
  <li>Run a second task about the same company. Does the agent recall prior insights?</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">7</div><h2>Structured Outputs with Pydantic</h2><span class="topic-time">30 min</span></div>
<div class="topic-body">
<p>For reliable downstream processing, you can enforce structured output on individual tasks using Pydantic models.</p>

<div class="arch-diagram">
  <div class="title">STRUCTURED TASK OUTPUT</div>
  <div><span class="purple">from</span> pydantic <span class="purple">import</span> BaseModel</div>
  <div></div>
  <div><span class="blue">class</span> <span class="yellow">CompanyReport</span>(BaseModel):</div>
  <div>    company: str</div>
  <div>    industry: str</div>
  <div>    strengths: list[str]</div>
  <div>    risks: list[str]</div>
  <div>    recommendation: str</div>
  <div></div>
  <div>analysis_task = Task(</div>
  <div>    description=<span class="green">"Analyse ACME Corp"</span>,</div>
  <div>    expected_output=<span class="green">"A structured company report"</span>,</div>
  <div>    agent=analyst,</div>
  <div>    <span class="highlight">output_pydantic=CompanyReport</span>,</div>
  <div>)</div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Create a Pydantic model for an article (title, summary, key_points, word_count).</li>
  <li>Use <code>output_pydantic</code> on the write task. Verify the output matches the model.</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Project 1 — Help-desk Automation Crew</h4><p>One project · ~2 hours · Build a full customer support crew</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">P1</div><h2>Project — Help-desk Automation Crew</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">
<p>Build a multi-agent crew that handles customer support tickets. A Classifier triages the ticket, a Researcher looks up relevant documentation, and a Responder drafts a reply. The crew should handle billing questions, technical issues, and feature requests.</p>

<div class="lab-box"><h4>✏️ Phase 1 — Define Agents (30 min)</h4><ol>
  <li>Create a <strong>Classifier</strong> agent that reads a support ticket and categorises it (billing, technical, feature_request, other).</li>
  <li>Create a <strong>Researcher</strong> agent with a custom tool that searches a FAQ document (JSON or text file).</li>
  <li>Create a <strong>Responder</strong> agent that drafts a professional, empathetic reply.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 2 — Define Tasks & Crew (30 min)</h4><ol>
  <li>Create three tasks: classify_task, research_task, respond_task.</li>
  <li>Use <code>output_pydantic</code> on classify_task to enforce a structured classification result.</li>
  <li>Wire everything into a sequential crew. Run with a sample ticket.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 3 — Test & Iterate (30 min)</h4><ol>
  <li>Test with 5 different ticket types. Check classification accuracy.</li>
  <li>Enable memory so the crew remembers recurring customers.</li>
  <li>Add verbose logging and callback hooks for observability.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 4 — Hierarchical Upgrade (30 min)</h4><ol>
  <li>Convert to hierarchical process. Does the manager route tickets better than sequential?</li>
  <li>Add an Escalation agent for tickets the Responder can't handle.</li>
  <li>Compare cost and quality between sequential and hierarchical runs.</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Project 2 — Equity Screening Assistant</h4><p>One project · ~2 hours · Build a crew that screens stocks</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">P2</div><h2>Project — Equity Screening Assistant</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">
<p>Build a crew that takes an investment thesis (e.g., "Find undervalued tech stocks with strong cash flow") and returns a ranked shortlist with analysis. Three agents: Screener (filters universe), Analyst (deep-dives each candidate), and Reporter (produces the final report).</p>

<div class="lab-box"><h4>✏️ Phase 1 — Agent Design (30 min)</h4><ol>
  <li>Create a <strong>Screener</strong> agent with web search tools. It takes an investment thesis and returns a list of 5–10 candidate tickers.</li>
  <li>Create an <strong>Analyst</strong> agent with YFinance tools. It analyses each ticker: P/E ratio, revenue growth, cash flow, analyst consensus.</li>
  <li>Create a <strong>Reporter</strong> agent that produces a structured ranking report.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 2 — Tasks & Structured Output (30 min)</h4><ol>
  <li>Define tasks for screening, analysis, and reporting.</li>
  <li>Create Pydantic models: <code>TickerScreen</code> (list of tickers), <code>StockAnalysis</code> (per-ticker metrics), <code>RankedReport</code> (final output).</li>
  <li>Wire as sequential: screen → analyse → report.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 3 — Execution & Iteration (30 min)</h4><ol>
  <li>Run with the thesis: "Undervalued tech stocks with strong cash flow."</li>
  <li>Run with a different thesis: "High-growth healthcare stocks."</li>
  <li>Compare outputs. Is the agent consistent? Does it cite real data?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 4 — Polish (30 min)</h4><ol>
  <li>Enable memory so the crew remembers prior screening results.</li>
  <li>Add error handling: what if YFinance returns no data for a delisted stock?</li>
  <li>Export the final report as a formatted markdown file.</li>
</ol></div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 7 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>CrewAI mental model</strong> — agents, tasks, processes, crews</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agent personas</strong> — role, goal, backstory shape agent behaviour</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Sequential process</strong> — assembly-line task execution</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Hierarchical process</strong> — manager-based dynamic routing</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Delegation</strong> — agents asking other agents for help mid-task</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Custom tools</strong> — @tool decorator and BaseTool class</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Memory system</strong> — short-term, long-term, entity, user memory</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Structured outputs</strong> — output_pydantic on tasks</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>When would you choose hierarchical over sequential process? Give a concrete example.</li>
  <li>How does agent delegation differ from the hierarchical manager pattern?</li>
  <li>Design a 4-agent crew for a content marketing pipeline. What roles, goals, and backstories would you assign?</li>
  <li>Explain the trade-offs of enabling memory for a crew that runs thousands of times per day.</li>
  <li>You need to integrate a proprietary API into a CrewAI agent. Walk through the BaseTool implementation.</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/05/02/u6-rapid-agent-prototyping-phidata/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 6</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/16/u8-conversational-agent-networks-autogen/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 8 →</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
