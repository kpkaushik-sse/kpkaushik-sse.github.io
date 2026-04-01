---
layout: default
title: "Unit 10 — Visual & Low-Code Agent Builders"
date: 2026-05-23
categories: [agentic-ai, production]
permalink: /blog/2026/05/23/u10-visual-low-code-agent-builders/
description: "Build AI agents without writing code — explore Wordware for prompt engineering, Relevance AI for business automation, and Langflow for visual chain design with drag-and-drop components."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 10</span>
</nav>

<div class="mod-hero">
  <h1>Unit 10 — Visual & Low-Code Agent Builders</h1>
  <p class="mod-hero-sub">Not every agent needs 500 lines of Python. Visual builders let product managers, analysts, and rapid-prototypers create agents by connecting blocks on a canvas. This unit covers three platforms: <strong>Wordware</strong> for structured prompt engineering, <strong>Relevance AI</strong> for business automation, and <strong>Langflow</strong> for visual LangChain development.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track D · Production & Deployment</span>
    <span class="mod-pill time">⏱ ~8 hrs across 5 days (Week 11)</span>
    <span class="mod-pill hands">🛠 3 hands-on labs</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/" style="color:var(--gum);">Unit 9 — Tracing & Telemetry</a>. Understanding the code-first approach is essential to appreciating what low-code tools abstract away — and where they fall short.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Explain when to use visual/low-code builders vs. code-first frameworks</li>
    <li>Build structured prompt workflows in Wordware with variables, loops, and branching</li>
    <li>Create business automation agents in Relevance AI with built-in integrations</li>
    <li>Design visual LangChain flows in Langflow with drag-and-drop components</li>
    <li>Export Langflow flows as Python code for further customisation</li>
    <li>Compare the three platforms on flexibility, deployment options, and pricing</li>
    <li>Identify the sweet spot for each: when to use which tool</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">Wordware</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Relevance AI</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Langflow</span>
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
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>The low-code landscape — when visual beats code</h4><p>Two topics · ~1.5 hours · Cover: When to use low-code + platform overview</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>When Visual Beats Code</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>You've spent 8 units writing Python to build agents. That's the right approach when you need full control. But many real-world scenarios don't need that level of control — they need <strong>speed</strong>:</p>

<div class="blocks-grid">
  <div class="block-card"><h4>✅ Use low-code when</h4><p>Rapid prototyping, non-technical team members need to build, standard patterns (Q&A, summarise, extract), demo to stakeholders.</p></div>
  <div class="block-card"><h4>❌ Use code when</h4><p>Custom state management, complex multi-agent workflows, custom tools with business logic, production-scale with custom infrastructure.</p></div>
</div>

<h3>The three platforms</h3>
<table class="cmp-table">
  <thead><tr><th>Platform</th><th>Approach</th><th>Strength</th><th>Audience</th></tr></thead>
  <tbody>
    <tr><td><strong>Wordware</strong></td><td>Structured prompt IDE</td><td>Prompt engineering with variables, loops, conditionals</td><td>Prompt engineers, content teams</td></tr>
    <tr><td><strong>Relevance AI</strong></td><td>Business automation platform</td><td>Pre-built integrations (Slack, email, CRM), no-code agent builder</td><td>Business analysts, ops teams</td></tr>
    <tr><td><strong>Langflow</strong></td><td>Visual LangChain builder</td><td>Drag-and-drop LangChain components, export to Python</td><td>Developers who prefer visual design</td></tr>
  </tbody>
</table>

<div class="insight-box"><strong>The hybrid approach:</strong> Use Langflow to visually prototype a chain, export to Python for customisation, then instrument with Langfuse for monitoring. This combines the speed of visual design with the power of code.</div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>Platform Setup & First Impressions</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">

<div class="lab-box"><h4>✏️ Mini-exercise — Set Up All Three</h4><ol>
  <li><strong>Wordware:</strong> Go to wordware.ai and create a free account. Create your first "Word" (prompt program). Note how it feels like writing a document, not code.</li>
  <li><strong>Relevance AI:</strong> Go to relevanceai.com and create a free account. Explore the template gallery. Note the focus on business use cases.</li>
  <li><strong>Langflow:</strong> Install locally: <code>pip install langflow</code>, then <code>langflow run</code>. Open the canvas in your browser. Note the visual similarity to node-based tools like Unreal Blueprints or Node-RED.</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Lab 1 — Wordware: structured prompt engineering</h4><p>One full lab · ~1.5 hours · Cover: Variables, loops, branching in prompts</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">L1</div><h2>Lab — Wordware: From Prompts to Programs</h2><span class="topic-time">1.5 hrs</span></div>
<div class="topic-body">
<p>Wordware treats prompts like programs: you write natural language instructions augmented with variables, conditionals, and loops. It's prompt engineering with the rigour of programming.</p>

<div class="arch-diagram">
  <div class="title">WORDWARE PROMPT PROGRAM (PSEUDOCODE)</div>
  <div></div>
  <div><span class="highlight">Input:</span> <span class="green">company_name</span> (text), <span class="green">report_type</span> (dropdown: summary|detailed)</div>
  <div></div>
  <div><span class="blue">Step 1:</span> Research {{company_name}} and gather key facts.</div>
  <div></div>
  <div><span class="blue">Step 2:</span> <span class="yellow">IF</span> report_type == "detailed":</div>
  <div>    Include financial metrics, competitor analysis, and SWOT.</div>
  <div>  <span class="yellow">ELSE</span>:</div>
  <div>    Include only a 3-paragraph executive summary.</div>
  <div></div>
  <div><span class="blue">Step 3:</span> Format as markdown with headers and bullet points.</div>
  <div></div>
  <div><span class="highlight">Output:</span> The generated report.</div>
</div>

<div class="lab-box"><h4>✏️ Step 1 — Basic Prompt Programs (30 min)</h4><ol>
  <li>Create a Wordware "Word" that takes a product name and generates a marketing tagline.</li>
  <li>Add a variable for tone (professional, playful, urgent). Test with different combinations.</li>
  <li>Add a loop: generate 5 tagline variations and let the user pick the best one.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 2 — Advanced: Multi-Step with Branching (30 min)</h4><ol>
  <li>Create a customer email generator that branches based on email type (complaint, inquiry, thankyou).</li>
  <li>Each branch should have different instructions, tone, and output format.</li>
  <li>Add error handling: if the input is unclear, ask for clarification instead of guessing.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 3 — API Deployment (30 min)</h4><ol>
  <li>Deploy your Word as an API endpoint (Wordware provides this automatically).</li>
  <li>Call the API from Python and verify the output matches the UI preview.</li>
  <li>Measure latency: UI vs. API. How much overhead does Wordware add?</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>Lab 2 — Relevance AI: business automation agents</h4><p>One full lab · ~1.5 hours · Cover: No-code agents with integrations</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">L2</div><h2>Lab — Relevance AI: Agents for Business Teams</h2><span class="topic-time">1.5 hrs</span></div>
<div class="topic-body">
<p>Relevance AI targets business users who need AI automation without writing code. It provides pre-built integrations (Slack, Gmail, CRMs, spreadsheets) and a visual agent builder.</p>

<div class="blocks-grid">
  <div class="block-card"><h4>📧 Email tools</h4><p>Read, draft, and send emails. Classify incoming emails. Extract structured data from email bodies.</p></div>
  <div class="block-card"><h4>💬 Chat integrations</h4><p>Slack bots, website chat widgets, WhatsApp. Deploy agents on any messaging platform.</p></div>
  <div class="block-card"><h4>📊 Data tools</h4><p>Read/write spreadsheets, query databases, transform data. Agents can process CSV files and generate reports.</p></div>
  <div class="block-card"><h4>🔗 API connections</h4><p>Connect to any REST API. Pre-built connectors for popular tools (HubSpot, Salesforce, Notion).</p></div>
</div>

<div class="lab-box"><h4>✏️ Step 1 — Create a Support Agent (30 min)</h4><ol>
  <li>Use the Relevance AI agent builder to create a customer support agent.</li>
  <li>Give it a knowledge base: upload a FAQ document (PDF or text).</li>
  <li>Test with 5 sample questions. How well does it answer from the knowledge base?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 2 — Add Integrations (30 min)</h4><ol>
  <li>Connect the agent to a spreadsheet (Google Sheets or uploaded CSV).</li>
  <li>Ask the agent questions about the data: "What's the total revenue for Q3?"</li>
  <li>Have the agent write a summary email based on spreadsheet analysis.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 3 — Multi-Step Workflows (30 min)</h4><ol>
  <li>Create a workflow: when a new email arrives → classify it → if complaint, draft response → send for approval.</li>
  <li>Test the workflow end to end. Measure how long each step takes.</li>
  <li>Compare: how many lines of Python would this take with LangChain? Relevance AI does it in clicks.</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Lab 3 — Langflow: visual LangChain development</h4><p>One full lab · ~2 hours · Cover: Canvas design + Python export</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">L3</div><h2>Lab — Langflow: Drag-and-Drop Agent Design</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">
<p>Langflow translates LangChain components into visual blocks on a canvas. You drag-and-drop LLMs, prompts, tools, retrievers, and memory — then connect them with wires. The result is a working LangChain application that you can also export as Python code.</p>

<div class="arch-diagram">
  <div class="title">LANGFLOW — VISUAL CHAIN</div>
  <div></div>
  <div>  ┌──────────────┐     ┌───────────────┐     ┌──────────────┐</div>
  <div>  │ <span class="blue">Prompt</span>       │────▶│ <span class="green">ChatOpenAI</span>    │────▶│ <span class="purple">Output</span>       │</div>
  <div>  │ Template     │     │ gpt-4o-mini   │     │ Parser       │</div>
  <div>  └──────────────┘     └───────────────┘     └──────────────┘</div>
  <div>         <span class="dim">▲</span></div>
  <div>  ┌──────────────┐</div>
  <div>  │ <span class="orange">Retriever</span>    │</div>
  <div>  │ FAISS + docs │</div>
  <div>  └──────────────┘</div>
  <div></div>
  <div><span class="dim">Each box is a LangChain component. Wires pass data between them.</span></div>
</div>

<div class="lab-box"><h4>✏️ Step 1 — Simple Q&A Chain (30 min)</h4><ol>
  <li>Open Langflow canvas. Drag an OpenAI LLM node and a Prompt Template node.</li>
  <li>Connect them: Prompt → LLM → Output. Set the template to "Answer the following question: {question}".</li>
  <li>Test with the built-in playground. Verify the chain works.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 2 — RAG Chain (30 min)</h4><ol>
  <li>Add a FAISS VectorStore node and a Document Loader (upload a PDF).</li>
  <li>Wire: Documents → VectorStore → Retriever → Prompt (as context) → LLM → Output.</li>
  <li>Test: ask a question that requires information from the PDF.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 3 — Agent with Tools (30 min)</h4><ol>
  <li>Switch from a chain to an agent: add a Tool node (DuckDuckGo or Calculator).</li>
  <li>Wire: Tools → Agent → Output. Set the agent type to ReAct.</li>
  <li>Test with questions that require tool use. Observe the agent's reasoning in the logs.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Step 4 — Export to Python (30 min)</h4><ol>
  <li>Export the RAG chain as Python code using Langflow's export feature.</li>
  <li>Run the exported code locally. Does it produce the same output?</li>
  <li>Modify the Python code to add Langfuse tracing (from Unit 9). This is the hybrid workflow in action.</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Comparison & decision framework</h4><p>One topic · ~1.5 hours · Cover: When to use which tool + capstone prep</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Platform Comparison & Decision Framework</h2><span class="topic-time">75 min</span></div>
<div class="topic-body">
<p>You've now used all three platforms. Let's compare them systematically:</p>

<table class="cmp-table">
  <thead><tr><th>Feature</th><th>Wordware</th><th>Relevance AI</th><th>Langflow</th></tr></thead>
  <tbody>
    <tr><td><strong>Approach</strong></td><td>Prompt IDE</td><td>Business automation</td><td>Visual code builder</td></tr>
    <tr><td><strong>Learning curve</strong></td><td>Low (write prompts)</td><td>Low (click & configure)</td><td>Medium (need LangChain knowledge)</td></tr>
    <tr><td><strong>Flexibility</strong></td><td>Medium (prompt-level control)</td><td>Low (pre-built patterns)</td><td>High (full LangChain access)</td></tr>
    <tr><td><strong>Code export</strong></td><td>API only</td><td>API only</td><td>Full Python export</td></tr>
    <tr><td><strong>Self-hosting</strong></td><td>No</td><td>No</td><td>Yes (open source)</td></tr>
    <tr><td><strong>Best for</strong></td><td>Prompt engineering teams</td><td>Business ops automation</td><td>Dev teams wanting visual prototyping</td></tr>
    <tr><td><strong>Pricing</strong></td><td>Free tier + pay per run</td><td>Free tier + per agent</td><td>Free (open source)</td></tr>
  </tbody>
</table>

<h3>Decision flowchart</h3>
<div class="arch-diagram">
  <div class="title">WHICH TOOL SHOULD I USE?</div>
  <div></div>
  <div><span class="green">Q: Do you need code-level control?</span></div>
  <div>  <span class="yellow">YES</span> → Use LangChain/LangGraph <span class="dim">(Units 3–5)</span></div>
  <div>  <span class="yellow">NO</span> →</div>
  <div>    <span class="green">Q: Is this a business workflow with integrations?</span></div>
  <div>      <span class="yellow">YES</span> → <span class="highlight">Relevance AI</span></div>
  <div>      <span class="yellow">NO</span> →</div>
  <div>        <span class="green">Q: Is this mainly prompt engineering?</span></div>
  <div>          <span class="yellow">YES</span> → <span class="highlight">Wordware</span></div>
  <div>          <span class="yellow">NO</span> →</div>
  <div>            <span class="green">Q: Do you want visual design with code export?</span></div>
  <div>              <span class="yellow">YES</span> → <span class="highlight">Langflow</span></div>
  <div>              <span class="yellow">NO</span> → Use Phidata <span class="dim">(Unit 6)</span> for rapid code-first prototyping</div>
</div>

<div class="lab-box"><h4>✏️ Final exercise — Comparison Report</h4><ol>
  <li>Pick a scenario: "Build a customer support bot that answers from a FAQ and escalates complex issues."</li>
  <li>Build the same bot in all three platforms (or at least plan how you would).</li>
  <li>Write a comparison: time to build, quality of output, ease of iteration, deployment options.</li>
  <li>Make a recommendation: which platform would you use for this specific scenario?</li>
</ol></div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 10 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Low-code vs. code</strong> — speed vs. flexibility trade-off</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Wordware</strong> — structured prompt IDE with variables, loops, branching</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Relevance AI</strong> — business automation with pre-built integrations</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Langflow</strong> — visual LangChain builder with Python export</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Hybrid workflow</strong> — visual prototype → export to code → instrument with tracing</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Decision framework</strong> — when to use which tool based on requirements</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>A marketing team wants to build an agent that generates social media posts. Which platform would you recommend and why?</li>
  <li>What are the limitations of Langflow compared to writing LangChain code directly?</li>
  <li>Can Relevance AI handle complex multi-agent orchestration like CrewAI? Why or why not?</li>
  <li>You prototyped in Langflow and need to add custom authentication. What's your migration path?</li>
  <li>Design a hybrid workflow that uses two of these platforms together.</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 9</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/30/u11-capstone-deploying-autonomous-ai-cloud/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 11 ★ →</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
