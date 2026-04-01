---
layout: default
title: "Unit 8 — Conversational Agent Networks with AutoGen"
date: 2026-05-16
categories: [agentic-ai, specialized-agents]
permalink: /blog/2026/05/16/u8-conversational-agent-networks-autogen/
description: "Build multi-agent conversational systems with Microsoft AutoGen — define ConversableAgents, wire group chats with custom speaker selection, integrate code execution, and orchestrate complex discussions."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 8</span>
</nav>

<div class="mod-hero">
  <h1>Unit 8 — Conversational Agent Networks with AutoGen</h1>
  <p class="mod-hero-sub">Microsoft's AutoGen takes a fundamentally different approach to multi-agent systems: instead of task pipelines or manager delegation, agents communicate through <strong>conversations</strong>. Think of it as a group chat where each participant is an AI agent (or a human) with its own expertise. This unit teaches you to design, orchestrate, and control these conversational networks.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track C · Collaborative & Specialized Agents</span>
    <span class="mod-pill time">⏱ ~9 hrs across 5 days (Week 10)</span>
    <span class="mod-pill hands">🛠 1 hands-on project</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/05/09/u7-coordinated-agent-teams-crewai/" style="color:var(--gum);">Unit 7 — CrewAI</a>. Understanding task-based multi-agent systems will help you appreciate AutoGen's conversation-based paradigm.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Explain AutoGen's conversation-centric design versus task-centric frameworks (CrewAI, LangGraph)</li>
    <li>Create ConversableAgent, AssistantAgent, and UserProxyAgent instances</li>
    <li>Set up two-agent conversations with initiate_chat()</li>
    <li>Build group chats with GroupChat and GroupChatManager</li>
    <li>Implement custom speaker selection strategies (round_robin, random, LLM-based)</li>
    <li>Integrate code execution with DockerCommandLineCodeExecutor for safe sandboxed runs</li>
    <li>Add human-in-the-loop with UserProxyAgent and approval workflows</li>
    <li>Design termination conditions to prevent infinite agent loops</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">AutoGen Agents</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Group Chat & Speaker Selection</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Code Execution & Safety</span>
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
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>AutoGen fundamentals — agents and conversations</h4><p>Two topics · ~1.5 hours · Cover: AutoGen philosophy + two-agent chat</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>The Conversation-Centric Paradigm</h2><span class="topic-time">40 min</span></div>
<div class="topic-body">
<p>CrewAI thinks in <em>tasks</em>: define a task, assign an agent, execute. AutoGen thinks in <em>conversations</em>: agents talk to each other, and through dialogue, work emerges. This mirrors how real teams operate — through discussion rather than rigid task assignments.</p>

<table class="cmp-table">
  <thead><tr><th>Dimension</th><th>CrewAI</th><th>AutoGen</th></tr></thead>
  <tbody>
    <tr><td><strong>Unit of work</strong></td><td>Task (description + expected output)</td><td>Conversation (messages between agents)</td></tr>
    <tr><td><strong>Coordination</strong></td><td>Process (sequential/hierarchical)</td><td>Chat patterns (two-agent, group, nested)</td></tr>
    <tr><td><strong>Flow control</strong></td><td>Task ordering + manager delegation</td><td>Speaker selection + termination conditions</td></tr>
    <tr><td><strong>Human involvement</strong></td><td>Optional inputs via crew.kickoff(inputs={})</td><td>UserProxyAgent participates in conversation</td></tr>
    <tr><td><strong>Code execution</strong></td><td>Via tools (indirect)</td><td>First-class: DockerCodeExecutor, LocalCodeExecutor</td></tr>
    <tr><td><strong>Ideal for</strong></td><td>Structured workflows with clear outputs</td><td>Open-ended problem solving, code generation, research debates</td></tr>
  </tbody>
</table>

<div class="arch-diagram">
  <div class="title">AUTOGEN — AGENT TYPES</div>
  <div></div>
  <div><span class="highlight">ConversableAgent</span> <span class="dim">— base class for all agents</span></div>
  <div>  <span class="dim">├──</span> <span class="blue">AssistantAgent</span> <span class="dim">— LLM-powered, generates responses</span></div>
  <div>  <span class="dim">│     system_message, llm_config, tools</span></div>
  <div>  <span class="dim">└──</span> <span class="green">UserProxyAgent</span> <span class="dim">— represents a human or code executor</span></div>
  <div>        <span class="dim">human_input_mode: ALWAYS | TERMINATE | NEVER</span></div>
  <div>        <span class="dim">code_execution_config: executor settings</span></div>
</div>

<div class="insight-box"><strong>The key insight:</strong> In AutoGen, a UserProxyAgent doesn't have to be a human. It can be a code executor that runs Python scripts generated by the AssistantAgent. This "assistant generates code, proxy executes it" pattern is AutoGen's signature workflow.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Install AutoGen: <code>pip install autogen-agentchat autogen-ext[openai,docker]</code></li>
  <li>Read the AutoGen docs overview. Identify the three agent types and their purposes.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>Two-Agent Conversations</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>The simplest AutoGen pattern: an AssistantAgent and a UserProxyAgent chat back and forth. The assistant generates solutions (often code), and the proxy executes them and reports results.</p>

<div class="arch-diagram">
  <div class="title">TWO-AGENT CHAT — CODE GENERATION</div>
  <div><span class="purple">from</span> autogen <span class="purple">import</span> AssistantAgent, UserProxyAgent</div>
  <div></div>
  <div>llm_config = {<span class="green">"model"</span>: <span class="green">"gpt-4o-mini"</span>}</div>
  <div></div>
  <div>assistant = AssistantAgent(</div>
  <div>    name=<span class="green">"Coder"</span>,</div>
  <div>    system_message=<span class="green">"You write Python code to solve problems. "</span></div>
  <div>                   <span class="green">"Always include print statements to show results."</span>,</div>
  <div>    llm_config=llm_config,</div>
  <div>)</div>
  <div></div>
  <div>executor = UserProxyAgent(</div>
  <div>    name=<span class="green">"Executor"</span>,</div>
  <div>    human_input_mode=<span class="green">"NEVER"</span>,  <span class="dim"># no human intervention</span></div>
  <div>    code_execution_config={<span class="green">"use_docker"</span>: <span class="yellow">True</span>},</div>
  <div>    max_consecutive_auto_reply=<span class="yellow">5</span>,</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># Start the conversation</span></div>
  <div>executor.initiate_chat(</div>
  <div>    assistant,</div>
  <div>    message=<span class="green">"Calculate the first 20 Fibonacci numbers and plot them."</span>,</div>
  <div>)</div>
</div>

<p>The conversation flows: Executor sends the request → Coder writes Python code → Executor runs it in Docker → if there's an error, Executor sends the error back → Coder fixes the code → repeat until success or max_consecutive_auto_reply is reached.</p>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build the two-agent coding chat above. Ask it to solve 3 different problems.</li>
  <li>Change <code>human_input_mode</code> to "TERMINATE" — now you approve each code execution. Try it.</li>
  <li>Introduce a deliberate error in the system_message and watch the self-correction loop.</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Group chats — multiple agents in conversation</h4><p>Two topics · ~2 hours · Cover: GroupChat + speaker selection strategies</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Group Chat — N Agents, One Conversation</h2><span class="topic-time">55 min</span></div>
<div class="topic-body">
<p>Real problem-solving often needs more than two agents. AutoGen's GroupChat puts N agents in a shared conversation. A GroupChatManager decides who speaks next based on a speaker selection strategy.</p>

<div class="arch-diagram">
  <div class="title">GROUP CHAT SETUP</div>
  <div><span class="purple">from</span> autogen <span class="purple">import</span> GroupChat, GroupChatManager</div>
  <div></div>
  <div>planner = AssistantAgent(name=<span class="green">"Planner"</span>, ...)</div>
  <div>coder = AssistantAgent(name=<span class="green">"Coder"</span>, ...)</div>
  <div>reviewer = AssistantAgent(name=<span class="green">"Reviewer"</span>, ...)</div>
  <div>executor = UserProxyAgent(name=<span class="green">"Executor"</span>, ...)</div>
  <div></div>
  <div>group = GroupChat(</div>
  <div>    agents=[planner, coder, reviewer, executor],</div>
  <div>    messages=[],</div>
  <div>    max_round=<span class="yellow">15</span>,</div>
  <div>    <span class="highlight">speaker_selection_method="auto"</span>,  <span class="dim"># LLM picks next speaker</span></div>
  <div>)</div>
  <div></div>
  <div>manager = GroupChatManager(groupchat=group, llm_config=llm_config)</div>
  <div></div>
  <div>executor.initiate_chat(</div>
  <div>    manager,</div>
  <div>    message=<span class="green">"Build a data pipeline that fetches weather data and stores it in SQLite."</span>,</div>
  <div>)</div>
</div>

<p>The conversation might flow: Planner breaks down the task → Coder writes the data-fetching code → Executor runs it → Reviewer checks for issues → Coder fixes → Executor runs again → Planner confirms completion.</p>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build the 4-agent group chat above. Watch the conversation unfold with verbose=True.</li>
  <li>Track who speaks and in what order. Does the LLM-based selection make good choices?</li>
  <li>Set max_round=5 and observe how the conversation changes when severely constrained.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">4</div><h2>Speaker Selection Strategies</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>Who speaks next is the critical control mechanism in AutoGen group chats. The framework provides several strategies:</p>

<table class="cmp-table">
  <thead><tr><th>Strategy</th><th>How It Works</th><th>Best For</th></tr></thead>
  <tbody>
    <tr><td><strong>auto</strong></td><td>LLM reads conversation and picks the best next speaker</td><td>Complex, dynamic conversations</td></tr>
    <tr><td><strong>round_robin</strong></td><td>Agents take turns in a fixed order</td><td>Predictable review pipelines</td></tr>
    <tr><td><strong>random</strong></td><td>Random agent speaks next</td><td>Brainstorming, diverse perspectives</td></tr>
    <tr><td><strong>manual</strong></td><td>Human picks the next speaker</td><td>Debugging, controlled experiments</td></tr>
    <tr><td><strong>custom function</strong></td><td>Your function decides based on conversation state</td><td>Domain-specific routing logic</td></tr>
  </tbody>
</table>

<div class="arch-diagram">
  <div class="title">CUSTOM SPEAKER SELECTION</div>
  <div><span class="blue">def</span> <span class="yellow">custom_speaker</span>(last_speaker, groupchat):</div>
  <div>    <span class="green">"""Route based on the last message content."""</span></div>
  <div>    last_msg = groupchat.messages[-1][<span class="green">"content"</span>]</div>
  <div>    </div>
  <div>    <span class="purple">if</span> <span class="green">"error"</span> <span class="purple">in</span> last_msg.lower():</div>
  <div>        <span class="purple">return</span> coder  <span class="dim"># errors go back to coder</span></div>
  <div>    <span class="purple">elif</span> <span class="green">"```python"</span> <span class="purple">in</span> last_msg:</div>
  <div>        <span class="purple">return</span> executor  <span class="dim"># code blocks go to executor</span></div>
  <div>    <span class="purple">elif</span> <span class="green">"APPROVE"</span> <span class="purple">in</span> last_msg:</div>
  <div>        <span class="purple">return</span> <span class="yellow">None</span>  <span class="dim"># terminate</span></div>
  <div>    <span class="purple">else</span>:</div>
  <div>        <span class="purple">return</span> reviewer  <span class="dim"># default to reviewer</span></div>
  <div></div>
  <div>group = GroupChat(</div>
  <div>    agents=[coder, executor, reviewer],</div>
  <div>    speaker_selection_method=custom_speaker,</div>
  <div>)</div>
</div>

<div class="insight-box"><strong>Speaker selection is your steering wheel:</strong> The conversation pattern (and therefore the quality of results) depends heavily on who speaks when. LLM-based selection is flexible but unpredictable. Custom functions give you full control. Start with "auto" for prototyping, then move to custom functions for production.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Try all four built-in strategies on the same problem. Compare the conversation flow and final output.</li>
  <li>Write a custom speaker selection function that always routes code-containing messages to the executor.</li>
  <li>Add logging to your custom function to track the decision-making process.</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>Code execution, tools, and safety</h4><p>Two topics · ~1.5 hours · Cover: Code executors + custom tools + termination</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">5</div><h2>Safe Code Execution</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">
<p>AutoGen's killer feature: agents can generate <em>and execute</em> code. This is powerful but dangerous. The framework provides sandboxed execution through Docker containers.</p>

<div class="blocks-grid">
  <div class="block-card"><h4>🐳 DockerCommandLineCodeExecutor</h4><p>Executes code in an isolated Docker container. Safest option — no access to host filesystem or network (unless configured).</p></div>
  <div class="block-card"><h4>💻 LocalCommandLineCodeExecutor</h4><p>Runs code directly on the host machine. Fast but risky — use only in development.</p></div>
</div>

<div class="arch-diagram">
  <div class="title">DOCKER CODE EXECUTOR</div>
  <div><span class="purple">from</span> autogen.coding <span class="purple">import</span> DockerCommandLineCodeExecutor</div>
  <div></div>
  <div>executor_config = {</div>
  <div>    <span class="green">"executor"</span>: DockerCommandLineCodeExecutor(</div>
  <div>        image=<span class="green">"python:3.12-slim"</span>,</div>
  <div>        timeout=<span class="yellow">60</span>,  <span class="dim"># kill after 60 seconds</span></div>
  <div>        work_dir=<span class="green">"./output"</span>,</div>
  <div>    ),</div>
  <div>}</div>
  <div></div>
  <div>proxy = UserProxyAgent(</div>
  <div>    name=<span class="green">"CodeRunner"</span>,</div>
  <div>    code_execution_config=executor_config,</div>
  <div>    human_input_mode=<span class="green">"NEVER"</span>,</div>
  <div>)</div>
</div>

<div class="insight-box"><strong>Security principle:</strong> Never use LocalCommandLineCodeExecutor in production. Docker containers isolate the execution environment — even if the agent generates malicious code, it can't escape the container. Always set a timeout to prevent infinite loops.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Set up DockerCommandLineCodeExecutor. Have the assistant generate and run a Python script.</li>
  <li>Intentionally ask for code with an infinite loop. Verify the timeout catches it.</li>
  <li>Compare execution times between Docker and Local executors for numerical computations.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">6</div><h2>Termination Conditions & Tool Registration</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">
<p>Without termination conditions, agents will chat forever. AutoGen provides several ways to stop conversations:</p>

<div class="blocks-grid">
  <div class="block-card"><h4>🔢 max_consecutive_auto_reply</h4><p>Stop after N consecutive automated replies. Prevents runaway conversations.</p></div>
  <div class="block-card"><h4>🏁 is_termination_msg</h4><p>A function that checks each message. Returns True when done (e.g., message contains "TERMINATE").</p></div>
  <div class="block-card"><h4>🔄 max_round</h4><p>GroupChat parameter — stop after N total messages across all agents.</p></div>
  <div class="block-card"><h4>👤 human_input_mode="TERMINATE"</h4><p>Agent pauses for human approval before each reply. Human can type "exit" to stop.</p></div>
</div>

<h3>Registering custom tools</h3>
<div class="arch-diagram">
  <div class="title">TOOL REGISTRATION</div>
  <div><span class="purple">from</span> autogen <span class="purple">import</span> register_function</div>
  <div></div>
  <div><span class="blue">def</span> <span class="yellow">get_weather</span>(city: str) -> str:</div>
  <div>    <span class="green">"""Get current weather for a city."""</span></div>
  <div>    <span class="purple">return</span> f<span class="green">"Weather in {city}: 22°C, Partly Cloudy"</span></div>
  <div></div>
  <div><span class="dim"># Register tool with both agents</span></div>
  <div>register_function(</div>
  <div>    get_weather,</div>
  <div>    caller=assistant,   <span class="dim"># who can suggest calling this tool</span></div>
  <div>    executor=executor,  <span class="dim"># who actually executes it</span></div>
  <div>    description=<span class="green">"Get weather for a city"</span>,</div>
  <div>)</div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Add <code>is_termination_msg</code> that stops when the message contains "TASK COMPLETE".</li>
  <li>Register a custom tool (e.g., a calculator). Verify the assistant can call it.</li>
  <li>Combine termination conditions: max_round=10 AND termination message. Which fires first?</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Advanced patterns — nested chats and human-in-the-loop</h4><p>Two topics · ~2 hours · Cover: Nested conversations + human approval workflows</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">7</div><h2>Nested Conversations</h2><span class="topic-time">55 min</span></div>
<div class="topic-body">
<p>AutoGen supports <strong>nested chats</strong>: an agent in one conversation can start a separate side conversation with another agent to get help with a sub-problem, then bring the result back to the main conversation.</p>

<div class="arch-diagram">
  <div class="title">NESTED CHAT PATTERN</div>
  <div><span class="green">Main Group Chat</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  Planner: <span class="green">"We need financial analysis of MSFT"</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  Analyst <span class="dim">→ starts nested chat with</span> <span class="blue">FinanceBot</span></div>
  <div>  <span class="dim">│        ├──</span> Analyst: <span class="green">"Analyse MSFT P/E ratio"</span></div>
  <div>  <span class="dim">│        └──</span> FinanceBot: <span class="green">"MSFT P/E: 35.2, above sector avg"</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  Analyst <span class="dim">← brings result back to main chat</span></div>
  <div>  <span class="dim">│</span></div>
  <div>  Analyst: <span class="green">"MSFT P/E is 35.2, above sector average..."</span></div>
</div>

<div class="insight-box"><strong>When to nest:</strong> Nested chats are useful when a sub-problem is complex enough to warrant its own multi-turn conversation, but the result should be summarised before returning to the main group. Think of it as a "breakout room" in a meeting.</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Set up a main chat with Planner + Analyst + Coder. Configure Analyst to start a nested chat with a FinanceBot when financial questions arise.</li>
  <li>Run a task that requires both coding and financial analysis. Verify the nested chat fires correctly.</li>
</ol></div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">8</div><h2>Human-in-the-Loop Workflows</h2><span class="topic-time">50 min</span></div>
<div class="topic-body">
<p>AutoGen makes human participation natural: a UserProxyAgent in <code>human_input_mode="ALWAYS"</code> pauses for input at every turn. This is powerful for approval workflows, debugging, and collaborative problem-solving.</p>

<div class="arch-diagram">
  <div class="title">HUMAN APPROVAL WORKFLOW</div>
  <div>human = UserProxyAgent(</div>
  <div>    name=<span class="green">"Human"</span>,</div>
  <div>    human_input_mode=<span class="green">"ALWAYS"</span>,  <span class="dim"># pause every time</span></div>
  <div>    code_execution_config=<span class="yellow">False</span>,</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># In a group chat, the human agent appears alongside AI agents.</span></div>
  <div><span class="dim"># When it's the human's turn, the program pauses for terminal input.</span></div>
  <div><span class="dim"># The human can provide feedback, redirect, or approve.</span></div>
</div>

<div class="lab-box"><h4>✏️ Mini-exercise</h4><ol>
  <li>Build a code review workflow: Coder generates code, Human approves or requests changes.</li>
  <li>Add a Reviewer agent that checks code quality before showing it to the Human.</li>
  <li>Test with a complex task. How many rounds of feedback does it take?</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Project — Literature Review Assistant</h4><p>One project · ~2.5 hours · Build a multi-agent research crew</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">P</div><h2>Project — Literature Review Assistant</h2><span class="topic-time">2.5 hrs</span></div>
<div class="topic-body">
<p>Build a multi-agent conversation that conducts a literature review. Given a research topic, agents search for papers, summarise key findings, identify gaps, and produce a structured review document — all through conversation.</p>

<div class="lab-box"><h4>✏️ Phase 1 — Define Agents (30 min)</h4><ol>
  <li>Create a <strong>SearchAgent</strong> (AssistantAgent) with web search tools for finding papers and articles.</li>
  <li>Create a <strong>SummariserAgent</strong> (AssistantAgent) that reads articles and extracts key findings.</li>
  <li>Create a <strong>CriticAgent</strong> (AssistantAgent) that identifies gaps, contradictions, and areas for further research.</li>
  <li>Create a <strong>WriterAgent</strong> (AssistantAgent) that compiles everything into a structured literature review.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 2 — Group Chat Setup (30 min)</h4><ol>
  <li>Wire all agents into a GroupChat with max_round=20.</li>
  <li>Implement a custom speaker selection function: SearchAgent goes first, then Summariser, then Critic, then Writer — but allow Critic to send it back to SearchAgent if gaps are found.</li>
  <li>Add termination: stop when WriterAgent produces a message containing "## Literature Review".</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 3 — Execute & Iterate (40 min)</h4><ol>
  <li>Run with topic: "Recent advances in retrieval-augmented generation for enterprise applications."</li>
  <li>Run with topic: "Multi-agent systems for software engineering tasks."</li>
  <li>Compare the outputs. Does the Critic actually improve the final review?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 4 — Add Human & Code Execution (30 min)</h4><ol>
  <li>Add a Human proxy that approves the final review before it's saved.</li>
  <li>Add a CodeAgent that generates a bibliography in BibTeX format using Python code execution.</li>
  <li>Save the final review and bibliography to files.</li>
</ol></div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 8 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Conversation-centric paradigm</strong> — agents collaborate through dialogue, not task pipelines</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agent types</strong> — ConversableAgent, AssistantAgent, UserProxyAgent</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Two-agent chat</strong> — initiate_chat() for simple assistant + executor patterns</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Group chat</strong> — N agents with GroupChatManager and speaker selection</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Speaker selection</strong> — auto, round_robin, random, manual, custom function</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Code execution</strong> — DockerCommandLineCodeExecutor for safe sandboxed runs</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Nested conversations</strong> — breakout chats for complex sub-problems</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Termination</strong> — max_round, max_consecutive_auto_reply, is_termination_msg</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>When would you choose AutoGen over CrewAI? Give a scenario for each.</li>
  <li>Design a custom speaker selection function for a 5-agent software development team.</li>
  <li>Explain why Docker-based code execution is critical for production deployments.</li>
  <li>How would you handle a conversation where agents get stuck in a loop? List three strategies.</li>
  <li>Compare the human-in-the-loop patterns in AutoGen vs. LangGraph. Which gives the human more control?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/05/09/u7-coordinated-agent-teams-crewai/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 7</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 9 →</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
