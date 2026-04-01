---
layout: default
title: "Unit 2 — Agent Blueprints & Reasoning Strategies"
date: 2026-03-28
categories: [agentic-ai, foundations]
permalink: /blog/2026/03/28/u2-agentic-ai-architecture-design-patterns/
description: "Deep dive into agentic AI architecture types, the six framework modules (perception, cognitive, action, learning, collaboration, security), and five core design patterns — Reflection, Tool Use, Planning, ReAct/ReWOO, and Multi-Agent."
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
  <span>Unit 2</span>
</nav>

<!-- Hero -->
<div class="mod-hero">
  <h1>Unit 2 — Agent Blueprints & Reasoning Strategies</h1>
  <p class="mod-hero-sub">How are autonomous AI systems actually wired? This unit opens up the black box — you'll learn the architecture types, the six core modules inside every agent framework, and the five design patterns that dictate <em>how</em> an agent thinks and acts.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Module A · Groundwork</span>
    <span class="mod-pill time">⏱ ~10 hrs across 5 days (weeks 2–3)</span>
    <span class="mod-pill hands">🛠 2 hands-on labs</span>
  </div>
</div>

<!-- Prerequisites -->
<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/03/21/m1-agentic-ai-essentials/" style="color: var(--gum);">Unit 1 — Agentic AI Essentials</a> first. You'll need the agent core loop, building blocks, and three-way AI comparison to follow along.
</div>

<!-- Objectives -->
<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Compare and select the right agent architecture type for a given problem</li>
    <li>Explain what each of the six framework modules does: Perception, Cognitive, Action, Learning, Collaboration, Security</li>
    <li>Implement the Reflection design pattern — agents that critique and improve their own output</li>
    <li>Implement the Tool Use pattern — agents that select and call external tools</li>
    <li>Implement the Planning pattern — agents that decompose goals before acting</li>
    <li>Differentiate and apply ReAct (interleaved reasoning + action) vs. ReWOO (plan-first reasoning)</li>
    <li>Design a multi-agent pattern with role assignment, delegation, and result merging</li>
    <li>Evaluate trade-offs: latency, cost, reliability, and security when choosing patterns</li>
  </ul>
</div>

<!-- Skills badge -->
<div style="display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 28px;">
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(84,100,20,0.1); color: var(--gum);">Understanding Agentic AI Frameworks</span>
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(172,100,46,0.1); color: var(--earth);">Implementing AI Design Patterns</span>
  <span style="padding: 5px 14px; border-radius: 20px; font-size: 12px; font-weight: 500; background: rgba(224,248,46,0.15); color: var(--gum-dark);">Designing Secure & Scalable AI Architectures</span>
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
     DAY 1 — Architecture Overview + Types
     ═══════════════════════════════════════════════ -->
<div id="day1" class="day-panel active">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d1prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 1 overview</div>
  <div class="sched-body">
    <h4>The big picture — how agent systems are structured</h4>
    <p>Two topics · ~2 hours · Cover: Why architecture matters + the five major architecture families</p>
  </div>
</div>

<!-- ── TOPIC 1 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">1</div>
    <h2>Agentic AI Architecture — Why It Matters</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>In Unit 1 you learned <em>what</em> an AI agent does — perceive, plan, act, learn. Now the question becomes: <strong>how do you actually wire all the pieces together?</strong> That's architecture.</p>

    <p>Architecture is the structural blueprint that dictates how data flows between the LLM, tools, memory, and the outside world. Get the architecture right, and your agent is fast, reliable, and easy to debug. Get it wrong, and you end up with a tangled mess that hallucinates, loops forever, or costs a fortune in API calls.</p>

    <div class="insight-box">
      <strong>Analogy:</strong> Think of architecture like the floor plan of a restaurant. The menu (LLM) decides what to cook, but the layout of the kitchen (architecture) determines whether orders get to tables quickly or everything crashes during the dinner rush.
    </div>

    <h3>What an agent architecture must specify</h3>
    <p>Every agent architecture — whether you're using LangGraph, CrewAI, or building from scratch — must answer five questions:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>1. Input handling</h4>
        <p>How does the agent receive and parse user goals? Text, voice, API webhook, upstream agent message?</p>
      </div>
      <div class="block-card">
        <h4>2. Reasoning strategy</h4>
        <p>How does the agent decide what to do next? Single LLM call? Chain-of-thought? Multi-step planner? Ensemble vote?</p>
      </div>
      <div class="block-card">
        <h4>3. Tool orchestration</h4>
        <p>How are tools registered, selected, called, and how are their results fed back? Parallel or sequential?</p>
      </div>
      <div class="block-card">
        <h4>4. Memory scope</h4>
        <p>What does the agent remember within a task? Across tasks? Does it share memory with other agents?</p>
      </div>
      <div class="block-card">
        <h4>5. Control flow</h4>
        <p>What triggers the loop to repeat? What conditions cause it to stop, escalate, or hand off to a human?</p>
      </div>
    </div>

    <!-- High-level architecture diagram -->
    <div class="arch-diagram">
      <div class="title">HIGH-LEVEL AGENT ARCHITECTURE</div>
      <div><span class="yellow">┌─────────────────────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="highlight">USER / UPSTREAM SYSTEM</span>                            <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬─────────────────────────────────────┘</span></div>
      <div><span class="dim">                │  goal / message</span></div>
      <div><span class="yellow">┌───────────────▼─────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="green">PERCEPTION MODULE</span>  — parse, classify, extract    <span class="yellow">│</span></div>
      <div><span class="yellow">└───────────────┬─────────────────────────────────────┘</span></div>
      <div><span class="dim">                │  structured context</span></div>
      <div><span class="yellow">┌───────────────▼─────────────────────────────────────┐</span></div>
      <div><span class="yellow">│</span>  <span class="blue">COGNITIVE MODULE</span>  — reason, plan, decide          <span class="yellow">│</span></div>
      <div><span class="yellow">│</span>  <span class="dim">(LLM + chain-of-thought + strategy selection)</span>     <span class="yellow">│</span></div>
      <div><span class="yellow">└───────┬───────────────────────────┬───────────────┘</span></div>
      <div><span class="dim">        │ action plan               │ memory query</span></div>
      <div><span class="yellow">┌───────▼──────────┐</span>    <span class="yellow">┌──────────▼──────────────┐</span></div>
      <div><span class="yellow">│</span> <span class="purple">ACTION MODULE</span>    <span class="yellow">│</span>    <span class="yellow">│</span> <span class="orange">LEARNING MODULE</span>        <span class="yellow">│</span></div>
      <div><span class="yellow">│</span> <span class="dim">tools, APIs,</span>    <span class="yellow">│</span>    <span class="yellow">│</span> <span class="dim">short-term + long-term</span> <span class="yellow">│</span></div>
      <div><span class="yellow">│</span> <span class="dim">side effects</span>    <span class="yellow">│</span>    <span class="yellow">│</span> <span class="dim">experience + feedback</span>  <span class="yellow">│</span></div>
      <div><span class="yellow">└───────┬──────────┘</span>    <span class="yellow">└─────────────────────────┘</span></div>
      <div><span class="dim">        │ observation</span></div>
      <div><span class="dim">        └──► feeds back to Cognitive Module (loop)</span></div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Open your Module 1 notes and add a new section: <strong>"Unit 2 — Architecture"</strong></li>
        <li>In your own words, write why architecture matters (hint: what fails first in a poorly-designed agent?)</li>
        <li>Draw the high-level diagram above by hand — label each module</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 2 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">2</div>
    <h2>Architecture Types — Five Families</h2>
    <span class="topic-time">75 min</span>
  </div>
  <div class="topic-body">
    <p>Not all agents are wired the same way. The architecture you choose depends on the task's complexity, latency requirements, and how much reasoning the agent needs to do before acting.</p>

    <!-- 1. Reactive -->
    <h3>1. Reactive Architecture</h3>
    <p>The simplest form. The agent maps inputs directly to actions — no planning, no memory. Think of a thermostat: temperature drops below threshold → turn on heating. That's it.</p>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ When to use</h4>
        <p>Simple, well-defined tasks. Low latency required. No ambiguity in the mapping between observation and action.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>❌ Limitations</h4>
        <p>Cannot handle multi-step goals. No memory of past interactions. Fails when the situation changes unexpectedly.</p>
      </div>
    </div>

    <div class="arch-diagram" style="text-align:center;">
      <span class="green">Input</span> <span class="dim">──►</span> <span class="blue">IF-THEN Rules</span> <span class="dim">──►</span> <span class="purple">Action</span>
      <div style="color: #64748b; font-size: 11px; margin-top: 4px;">No planning. No memory. Direct mapping.</div>
    </div>

    <!-- 2. Deliberative -->
    <h3>2. Deliberative Architecture</h3>
    <p>The agent maintains an internal model of the world, reasons about possible futures, and plans a sequence of actions before executing anything. This is the "thinking before acting" approach.</p>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ When to use</h4>
        <p>Complex goals that require multi-step plans. When the agent must consider trade-offs, constraints, and dependencies.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>❌ Limitations</h4>
        <p>Slower — the planning step adds latency. The internal world model can become stale. Expensive in LLM tokens.</p>
      </div>
    </div>

    <div class="arch-diagram" style="text-align:center;">
      <span class="green">Goal</span> <span class="dim">──►</span> <span class="blue">World Model</span> <span class="dim">──►</span> <span class="purple">Planner</span> <span class="dim">──►</span> <span class="yellow">Action 1 → Action 2 → ... → Action N</span>
      <div style="color: #64748b; font-size: 11px; margin-top: 4px;">Full plan generated before any action is taken. Think ReWOO.</div>
    </div>

    <!-- 3. Hybrid (BDI) -->
    <h3>3. Hybrid Architecture (Belief-Desire-Intention)</h3>
    <p>The best of both worlds: a reactive layer for urgent, time-sensitive responses combined with a deliberative layer for complex planning. Most production agent systems are hybrids.</p>

    <div class="arch-diagram">
      <div class="title">HYBRID ARCHITECTURE (BDI MODEL)</div>
      <div><span class="green">Beliefs</span>  <span class="dim">— what the agent knows about the world right now</span></div>
      <div><span class="yellow">Desires</span>  <span class="dim">— the goals the agent wants to achieve</span></div>
      <div><span class="purple">Intentions</span> <span class="dim">— the plan the agent has committed to executing</span></div>
      <div style="margin-top:12px;">
        <span class="dim">┌──────────────────────────────────────────┐</span>
      </div>
      <div><span class="dim">│</span>  <span class="red">Reactive Layer</span> <span class="dim">— handles urgent signals   │</span></div>
      <div><span class="dim">│</span>       <span class="dim">▲ interrupts when needed</span>             <span class="dim">│</span></div>
      <div><span class="dim">│</span>  <span class="blue">Deliberative Layer</span> <span class="dim">— plans multi-step  │</span></div>
      <div><span class="dim">│</span>       <span class="dim">▲ updates beliefs after each action</span>  <span class="dim">│</span></div>
      <div><span class="dim">│</span>  <span class="orange">Learning Layer</span> <span class="dim">— improves over time      │</span></div>
      <div>
        <span class="dim">└──────────────────────────────────────────┘</span>
      </div>
    </div>

    <div class="insight-box">
      <strong>Real-world example:</strong> A customer support agent. The reactive layer catches phrases like "cancel my account" and immediately routes to retention. The deliberative layer investigates the full context — order history, past complaints, loyalty status — and plans a personalised retention strategy.
    </div>

    <!-- 4. Layered -->
    <h3>4. Layered Architecture</h3>
    <p>The system is organised into distinct horizontal layers, each with a specific responsibility. Lower layers handle fast, routine operations; upper layers handle abstract reasoning and goal management.</p>

    <div class="arch-diagram" style="text-align:center;">
      <div class="title">LAYERED ARCHITECTURE</div>
      <div><span class="purple">┌────────────────────────────────┐</span></div>
      <div><span class="purple">│  Layer 4 — Goal Management     │</span>  <span class="dim">What to achieve</span></div>
      <div><span class="blue">├────────────────────────────────┤</span></div>
      <div><span class="blue">│  Layer 3 — Planning            │</span>  <span class="dim">How to achieve it</span></div>
      <div><span class="green">├────────────────────────────────┤</span></div>
      <div><span class="green">│  Layer 2 — Execution           │</span>  <span class="dim">Tool calls, API invocations</span></div>
      <div><span class="yellow">├────────────────────────────────┤</span></div>
      <div><span class="yellow">│  Layer 1 — Environment I/O     │</span>  <span class="dim">Raw inputs & outputs</span></div>
      <div><span class="yellow">└────────────────────────────────┘</span></div>
    </div>

    <p>This is how frameworks like LangGraph structure their state machines — each node in the graph corresponds to a layer or stage, and edges define transitions.</p>

    <!-- 5. Event-driven -->
    <h3>5. Event-Driven Architecture</h3>
    <p>Instead of a sequential loop, the agent responds to <strong>events</strong> — messages, webhooks, database changes, timers. Each event triggers a handler that might invoke tools, update state, or spawn sub-agents. Ideal for long-running workflows that span hours or days.</p>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ When to use</h4>
        <p>Workflows that wait for external signals (payment confirmation, user response, data pipeline completion). Multi-day processes.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>❌ Limitations</h4>
        <p>Harder to debug — non-linear execution. State management is critical. Requires persistent storage for in-flight tasks.</p>
      </div>
    </div>

    <!-- Architecture comparison table -->
    <h3>Quick comparison</h3>
    <table class="cmp-table">
      <thead>
        <tr><th>Architecture</th><th>Planning</th><th>Memory</th><th>Latency</th><th>Best For</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>Reactive</strong></td><td>None</td><td>None</td><td>Very low</td><td>Simple triggers, quick responses</td></tr>
        <tr><td><strong>Deliberative</strong></td><td>Full upfront plan</td><td>World model</td><td>High</td><td>Complex multi-step tasks</td></tr>
        <tr><td><strong>Hybrid (BDI)</strong></td><td>Both reactive + plan</td><td>Beliefs + logs</td><td>Medium</td><td>Production systems</td></tr>
        <tr><td><strong>Layered</strong></td><td>Per-layer</td><td>Shared state</td><td>Medium</td><td>Well-structured workflows</td></tr>
        <tr><td><strong>Event-driven</strong></td><td>Per-event handler</td><td>Persistent store</td><td>Variable</td><td>Long-running async workflows</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>Rule of thumb:</strong> Start with a simple reactive or deliberative architecture. Move to hybrid when you need both speed and planning. Use event-driven only when the workflow naturally spans multiple asynchronous triggers.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>For each of the five architectures, write one real-world use case in your notes</li>
        <li>Which architecture would you pick for the flight booking agent from Unit 1? Why?</li>
        <li>Which architecture fits a "weekly expense report generator" that waits for receipts to arrive over email?</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day1 -->

<!-- ═══════════════════════════════════════════════
     DAY 2 — Framework Modules Part 1 (Perception, Cognitive, Action)
     ═══════════════════════════════════════════════ -->
<div id="day2" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d2prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 2 overview</div>
  <div class="sched-body">
    <h4>Inside the framework — Perception, Cognition, Action</h4>
    <p>Three modules · ~2 hours · The core input → thinking → output pipeline of every agent</p>
  </div>
</div>

<!-- ── TOPIC 3: Perception Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">3</div>
    <h2>The Perception Module — How Agents Sense Their World</h2>
    <span class="topic-time">40 min</span>
  </div>
  <div class="topic-body">
    <p>Before an agent can think or act, it must <strong>understand what it's looking at</strong>. The Perception Module is the agent's eyes and ears — it takes raw input and converts it into structured, actionable context.</p>

    <h3>What the Perception Module handles</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>📝 Input parsing</h4>
        <p>Understand the user's message — extract the goal, constraints, entities, and intent. "Book a flight under ₹5000" → {action: book, type: flight, budget: 5000}.</p>
      </div>
      <div class="block-card">
        <h4>📄 Document ingestion</h4>
        <p>Read PDFs, web pages, emails, database rows. Convert unstructured content into chunks the LLM can reason over.</p>
      </div>
      <div class="block-card">
        <h4>👁 Multimodal input</h4>
        <p>Process images, screenshots, audio, or video. Vision models extract text from UIs; speech-to-text converts audio to text.</p>
      </div>
      <div class="block-card">
        <h4>🔔 Event detection</h4>
        <p>Monitor for triggers: new email arrived, webhook fired, database row changed, time-based cron tick.</p>
      </div>
    </div>

    <div class="arch-diagram" style="text-align: center;">
      <div class="title">PERCEPTION PIPELINE</div>
      <div><span class="green">Raw Input</span> <span class="dim">──►</span> <span class="blue">Classifier</span> <span class="dim">──►</span> <span class="purple">Entity Extractor</span> <span class="dim">──►</span> <span class="yellow">Context Builder</span> <span class="dim">──►</span> <span class="highlight">Structured Goal</span></div>
      <div style="color: #64748b; font-size: 11px; margin-top: 6px;">"Send the Q3 report to my manager" → {action: send, object: Q3_report, recipient: manager, channel: email}</div>
    </div>

    <div class="insight-box">
      <strong>Key insight:</strong> The quality of perception directly determines the quality of everything downstream. If the Perception Module misunderstands the goal, even the best planner and the best tools will produce the wrong result. Garbage in, garbage out — at agent scale.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 4: Cognitive Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">4</div>
    <h2>The Cognitive Module — How Agents Think and Decide</h2>
    <span class="topic-time">50 min</span>
  </div>
  <div class="topic-body">
    <p>The Cognitive Module is the agent's brain. It receives the structured context from Perception and decides <strong>what to do next</strong>. This is where the LLM lives — but it's much more than just one API call.</p>

    <h3>Responsibilities of the Cognitive Module</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>🧠 Reasoning</h4>
        <p>Chain-of-thought, tree-of-thought, or step-by-step analysis. The agent "thinks out loud" before committing to a decision.</p>
      </div>
      <div class="block-card">
        <h4>📋 Planning</h4>
        <p>Break the high-level goal into an ordered sequence of sub-tasks. Decide which tools to call and in what order.</p>
      </div>
      <div class="block-card">
        <h4>🎯 Decision making</h4>
        <p>Choose between alternatives: which flight is cheapest? Should I retry or escalate? Is this tool result good enough?</p>
      </div>
      <div class="block-card">
        <h4>🔄 Self-correction</h4>
        <p>Evaluate its own output. "Does this plan make sense? Did I miss a constraint? Is the tool result what I expected?" This is the Reflection pattern in action.</p>
      </div>
    </div>

    <h3>How the Cognitive Module interacts with the LLM</h3>
    <p>The LLM isn't called once — it's called repeatedly in a loop. Each call includes:</p>
    <ol style="padding-left: 20px; margin-bottom: 16px;">
      <li><strong>System prompt</strong> — the agent's identity, capabilities, rules, and constraints</li>
      <li><strong>Conversation history</strong> — what's happened so far in this task (short-term memory)</li>
      <li><strong>Current observation</strong> — the latest tool result or user message</li>
      <li><strong>Available tools</strong> — descriptions of what the agent can call right now</li>
    </ol>
    <p>The LLM responds with either a <strong>thought</strong> (internal reasoning), a <strong>tool call</strong> (action), or a <strong>final answer</strong> (task complete).</p>

    <div class="arch-diagram" style="text-align: center;">
      <div class="title">COGNITIVE LOOP (SINGLE ITERATION)</div>
      <div><span class="green">Context</span> <span class="dim">+</span> <span class="blue">Memory</span> <span class="dim">+</span> <span class="purple">Tools</span></div>
      <div><span class="dim">         │</span></div>
      <div><span class="dim">    ┌────▼─────┐</span></div>
      <div><span class="dim">    │</span> <span class="highlight">LLM Call</span> <span class="dim">│</span></div>
      <div><span class="dim">    └────┬─────┘</span></div>
      <div><span class="dim">         │</span></div>
      <div><span class="dim">    ┌────▼─────────────────────────────┐</span></div>
      <div><span class="yellow">    │ Thought │ Tool Call │ Final Answer │</span></div>
      <div><span class="dim">    └──────────────────────────────────┘</span></div>
    </div>

    <div class="insight-box">
      <strong>Common mistake:</strong> Treating the LLM as the entire agent. The LLM is just the reasoning engine inside the Cognitive Module. The module also includes the prompt engineering, the routing logic, the retry strategy, and the decision of when to stop.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 5: Action Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">5</div>
    <h2>The Action Module — How Agents Affect the World</h2>
    <span class="topic-time">40 min</span>
  </div>
  <div class="topic-body">
    <p>The Action Module is the agent's hands. It takes a tool-call decision from the Cognitive Module and <strong>actually executes it</strong> — calling an API, running code, navigating a browser, writing a file, or sending an email.</p>

    <h3>Components of the Action Module</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>🔧 Tool registry</h4>
        <p>A catalog of all tools the agent has access to: name, description, parameters, required permissions. The LLM reads this to decide which tool to call.</p>
      </div>
      <div class="block-card">
        <h4>⚡ Tool executor</h4>
        <p>Receives the LLM's tool-call request, validates the parameters, calls the actual function/API, and returns the result.</p>
      </div>
      <div class="block-card">
        <h4>🛡 Validation layer</h4>
        <p>Checks that tool-call parameters are correct before execution. Catches hallucinated endpoints, invalid data types, missing required fields.</p>
      </div>
      <div class="block-card">
        <h4>📊 Observation formatter</h4>
        <p>Takes the raw tool output and formats it for the LLM. Truncates long responses, highlights key data, strips noise.</p>
      </div>
    </div>

    <h3>Tool call lifecycle</h3>
    <div class="step-flow">
      <div class="step-card">
        <div class="step-num act">1</div>
        <div class="step-body">
          <div class="step-label act">COGNITIVE → ACTION</div>
          <div class="step-title">LLM emits a structured tool call</div>
          <div class="step-desc">The LLM outputs: {"tool": "search_flights", "params": {"from": "DEL", "to": "BOM", "date": "2026-04-04", "max_price": 5000}}</div>
          <div class="step-tools">
            <span class="tool-badge blue">Structured output</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">2</div>
        <div class="step-body">
          <div class="step-label act">VALIDATE</div>
          <div class="step-title">Action Module validates parameters</div>
          <div class="step-desc">Checks: Does "search_flights" exist in the registry? Are all required params present? Is "max_price" a number? Date in valid format? If validation fails → return error to Cognitive Module for retry.</div>
          <div class="step-tools">
            <span class="tool-badge red">Schema validation</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">3</div>
        <div class="step-body">
          <div class="step-label act">EXECUTE</div>
          <div class="step-title">Call the actual API / function</div>
          <div class="step-desc">The tool executor makes the real HTTP request to the flight search API. Handles timeouts, rate limits, authentication. Returns raw response.</div>
          <div class="step-tools">
            <span class="tool-badge green">API call</span>
            <span class="tool-badge amber">Error handling</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">4</div>
        <div class="step-body">
          <div class="step-label plan">ACTION → COGNITIVE</div>
          <div class="step-title">Format observation and feed back</div>
          <div class="step-desc">Raw API response (potentially huge JSON) → formatted observation: "Found 3 flights: IndiGo ₹4,200, Air India ₹4,800, SpiceJet ₹5,400 (over budget)." This becomes the next input to the Cognitive Module.</div>
          <div class="step-tools">
            <span class="tool-badge purple">Observation formatting</span>
          </div>
        </div>
      </div>
    </div>

    <div class="insight-box">
      <strong>Design principle:</strong> Never trust LLM-generated parameters blindly. The validation layer is your defence against hallucinated tool calls — the most common failure mode in production agents. Always validate against a strict schema before executing.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Pick any tool (web search, email sender, code executor). Write out its tool registry entry: name, description, parameters with types, and required permissions.</li>
        <li>What would happen if the validation layer didn't exist? List 3 things that could go wrong.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day2 -->

<!-- ═══════════════════════════════════════════════
     DAY 3 — Framework Modules Part 2 (Learning, Collaboration, Security)
     ═══════════════════════════════════════════════ -->
<div id="day3" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d3prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 3 overview</div>
  <div class="sched-body">
    <h4>Memory, teamwork, and safety — the invisible foundations</h4>
    <p>Three modules · ~2 hours · Cover: Learning, Collaboration, and Security modules</p>
  </div>
</div>

<!-- ── TOPIC 6: Learning Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">6</div>
    <h2>The Learning Module — How Agents Remember and Improve</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>Without memory, every task starts from zero. The Learning Module gives the agent the ability to <strong>remember past actions</strong>, <strong>learn from outcomes</strong>, and <strong>improve over time</strong>.</p>

    <h3>Four types of agent memory</h3>
    <table class="cmp-table">
      <thead><tr><th>Memory Type</th><th>Scope</th><th>Duration</th><th>Example</th></tr></thead>
      <tbody>
        <tr><td><strong>Working memory</strong></td><td>Current task</td><td>Current conversation</td><td>Steps completed so far, intermediate results, current plan</td></tr>
        <tr><td><strong>Episodic memory</strong></td><td>Past tasks</td><td>Across sessions</td><td>"Last time user asked for flights, they preferred morning departures"</td></tr>
        <tr><td><strong>Semantic memory</strong></td><td>General knowledge</td><td>Permanent</td><td>Domain facts stored in a vector database — company policies, product specs</td></tr>
        <tr><td><strong>Procedural memory</strong></td><td>How-to</td><td>Permanent</td><td>Learned strategies: "When API fails, retry 3x then switch to backup provider"</td></tr>
      </tbody>
    </table>

    <h3>How learning happens</h3>
    <div class="step-flow">
      <div class="step-card">
        <div class="step-num learn">1</div>
        <div class="step-body">
          <div class="step-label learn">OBSERVE</div>
          <div class="step-title">Record outcome of each action</div>
          <div class="step-desc">After every tool call, the agent logs: what was attempted, what was returned, whether it matched expectations, and how long it took.</div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num learn">2</div>
        <div class="step-body">
          <div class="step-label learn">EVALUATE</div>
          <div class="step-title">Score the outcome</div>
          <div class="step-desc">Did the action move us closer to the goal? Was the tool output useful? Did the user provide positive or negative feedback? This scoring can be automated (heuristic) or human-provided.</div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num learn">3</div>
        <div class="step-body">
          <div class="step-label learn">STORE</div>
          <div class="step-title">Persist the lesson</div>
          <div class="step-desc">Successful strategies → procedural memory. User preferences → episodic memory. New domain facts → semantic memory (vector DB). Failed approaches → negative examples for future prompts.</div>
        </div>
      </div>
    </div>

    <div class="insight-box">
      <strong>Key insight:</strong> Memory is what separates a demo agent from a production agent. A demo agent works once. A production agent works better the hundredth time because it remembers what succeeded and what failed.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 7: Collaboration Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">7</div>
    <h2>The Collaboration Module — How Agents Work Together</h2>
    <span class="topic-time">40 min</span>
  </div>
  <div class="topic-body">
    <p>In Unit 1 you learned the difference between a single agent and a multi-agent system. The Collaboration Module is what makes multi-agent systems actually work — it handles <strong>communication, delegation, and result synthesis</strong> between agents.</p>

    <h3>Communication patterns</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>📢 Broadcast</h4>
        <p>One agent sends a message to all other agents. Used for status updates, shared context, or emergency signals ("user changed the goal").</p>
      </div>
      <div class="block-card">
        <h4>🎯 Direct messaging</h4>
        <p>Agent A sends a specific request to Agent B. "Hey ResearchAgent, find me the top 5 competitors." Most common pattern.</p>
      </div>
      <div class="block-card">
        <h4>📋 Shared blackboard</h4>
        <p>All agents read from and write to a shared state store. Each agent picks up tasks it's equipped to handle. No direct messaging needed.</p>
      </div>
      <div class="block-card">
        <h4>🔄 Sequential pipeline</h4>
        <p>Agent A's output becomes Agent B's input, B's output becomes C's input. Like an assembly line: research → write → review → publish.</p>
      </div>
    </div>

    <h3>Delegation strategies</h3>
    <div class="arch-diagram">
      <div class="title">DELEGATION MODELS</div>
      <div style="margin-top: 8px;"><span class="yellow">1. Orchestrator model</span></div>
      <div><span class="dim">   A central "manager" agent assigns tasks, collects results, and makes final decisions.</span></div>
      <div><span class="dim">   Best for: well-defined workflows with clear subtask boundaries.</span></div>
      <div style="margin-top: 8px;"><span class="green">2. Peer-to-peer model</span></div>
      <div><span class="dim">   Agents negotiate directly with each other. No central coordinator.</span></div>
      <div><span class="dim">   Best for: decentralised systems where agents have equal authority.</span></div>
      <div style="margin-top: 8px;"><span class="purple">3. Hierarchical model</span></div>
      <div><span class="dim">   Multiple layers of delegation: top-level strategist → mid-level planners → worker agents.</span></div>
      <div><span class="dim">   Best for: large-scale systems with dozens of specialised agents.</span></div>
    </div>

    <div class="insight-box">
      <strong>Production advice:</strong> The orchestrator model covers 90% of real-world multi-agent use cases. Don't jump to peer-to-peer or hierarchical unless you genuinely have autonomous agents that need to negotiate. Start simple.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 8: Security Module ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">8</div>
    <h2>The Security Module — How Agents Stay Safe</h2>
    <span class="topic-time">40 min</span>
  </div>
  <div class="topic-body">
    <p>In Unit 1 you learned about the six risks of autonomous agents. The Security Module is where you <strong>engineer the defences</strong>. It's not optional — any agent that touches real data, real APIs, or real money needs security built into its architecture.</p>

    <h3>The five layers of agent security</h3>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num" style="background: #ef4444;">1</div>
        <div class="step-body">
          <div class="step-label" style="color: #fca5a5;">INPUT GUARD</div>
          <div class="step-title">Protect against prompt injection</div>
          <div class="step-desc">Sanitise all inputs before they reach the LLM. Detect and strip instruction-override patterns. Separate system instructions from user data. Use delimiters and instruction hierarchy.</div>
          <div class="step-tools">
            <span class="tool-badge red">Input sanitisation</span>
            <span class="tool-badge red">Prompt isolation</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num" style="background: #f59e0b;">2</div>
        <div class="step-body">
          <div class="step-label" style="color: #fcd34d;">PERMISSION SCOPING</div>
          <div class="step-title">Minimal privilege for every tool</div>
          <div class="step-desc">Each tool should have the minimum permissions needed. A flight search tool should not have access to the payment API. A reporting agent should have read-only database access.</div>
          <div class="step-tools">
            <span class="tool-badge amber">Least privilege</span>
            <span class="tool-badge amber">Role-based access</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num" style="background: #8b5cf6;">3</div>
        <div class="step-body">
          <div class="step-label" style="color: #c4b5fd;">OUTPUT VALIDATION</div>
          <div class="step-title">Verify before executing</div>
          <div class="step-desc">Never execute a tool call without validating the parameters against a strict schema. Check for SQL injection in database queries. Validate URLs before fetching. Verify file paths are within allowed directories.</div>
          <div class="step-tools">
            <span class="tool-badge purple">Schema enforcement</span>
            <span class="tool-badge purple">Injection detection</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num" style="background: #0ea5e9;">4</div>
        <div class="step-body">
          <div class="step-label" style="color: #7dd3fc;">ACTION BUDGETS</div>
          <div class="step-title">Cap the blast radius</div>
          <div class="step-desc">Set hard limits: max 20 tool calls per task, max 50K tokens per task, max $2 API spend per request. An unbounded agent can loop forever, send thousands of emails, or run up massive bills.</div>
          <div class="step-tools">
            <span class="tool-badge blue">Token budgets</span>
            <span class="tool-badge blue">Call limits</span>
          </div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num" style="background: #10b981;">5</div>
        <div class="step-body">
          <div class="step-label" style="color: #6ee7b7;">AUDIT TRAIL</div>
          <div class="step-title">Log everything for post-hoc review</div>
          <div class="step-desc">Every LLM call, every tool invocation, every parameter, every result — logged with timestamps. If something goes wrong, you need a complete trace to diagnose it. This is non-negotiable in production.</div>
          <div class="step-tools">
            <span class="tool-badge green">Structured logging</span>
            <span class="tool-badge green">Trace IDs</span>
          </div>
        </div>
      </div>
    </div>

    <div class="insight-box">
      <strong>The sandboxing principle:</strong> Run tool execution in isolated environments. Code execution in a sandboxed container (E2B, Docker). Browser automation in a disposable session. Database access through a read-only proxy. Never give the agent direct access to your production systems without guardrails.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Take the flight booking agent from Unit 1. List every tool it uses and what permissions each tool needs.</li>
        <li>Design a permission matrix: which tools can read user data? Which can write? Which can make payments?</li>
        <li>What action budget would you set? (max tool calls, max tokens, max spend)</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day3 -->

<!-- ═══════════════════════════════════════════════
     DAY 4 — Design Patterns
     ═══════════════════════════════════════════════ -->
<div id="day4" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d4prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 4 overview</div>
  <div class="sched-body">
    <h4>The five reasoning patterns every agent engineer must know</h4>
    <p>Five patterns · ~3 hours · The most important day in this unit — these patterns are the playbook</p>
  </div>
</div>

<!-- ── TOPIC 9: Reflection Pattern ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">9</div>
    <h2>Pattern 1 — Reflection</h2>
    <span class="topic-time">30 min</span>
  </div>
  <div class="topic-body">
    <p>The Reflection pattern makes an agent <strong>critique and improve its own output</strong> before delivering the final result. Instead of generating once and shipping, the agent generates → reviews → revises → ships.</p>

    <div class="loop-box">
      <span class="green">Generate</span> <span class="dim">──►</span> <span class="blue">Self-Critique</span> <span class="dim">──►</span> <span class="purple">Revise</span> <span class="dim">──►</span> <span class="yellow">Output</span>
      <div style="color: #64748b; font-size: 11px; margin-top: 6px;">Repeat critique→revise until quality threshold is met or max iterations reached</div>
    </div>

    <h3>How it works in practice</h3>
    <div class="step-flow">
      <div class="step-card">
        <div class="step-num act">1</div>
        <div class="step-body">
          <div class="step-label act">GENERATE</div>
          <div class="step-title">Produce an initial output</div>
          <div class="step-desc">The agent writes a first draft — could be code, an email, a research summary, a plan. This is the raw output before any quality check.</div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num perceive">2</div>
        <div class="step-body">
          <div class="step-label perceive">CRITIQUE</div>
          <div class="step-title">Evaluate against criteria</div>
          <div class="step-desc">A second LLM call (or the same LLM with a critic prompt) reviews the output: "Is this accurate? Does it meet the user's constraints? Are there logical errors? What's missing?" The critic returns a structured list of issues.</div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">3</div>
        <div class="step-body">
          <div class="step-label plan">REVISE</div>
          <div class="step-title">Fix the identified issues</div>
          <div class="step-desc">The agent takes the original output + the critique and produces an improved version. This loop can repeat 2–3 times until quality is acceptable.</div>
        </div>
      </div>
    </div>

    <div class="blocks-grid" style="grid-template-columns: 1fr 1fr;">
      <div class="block-card" style="border-left: 3px solid #6ee7b7;">
        <h4>✅ When to use</h4>
        <p>Content generation, code writing, report drafting — any task where quality matters and a wrong first attempt is tolerable.</p>
      </div>
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>⚠️ Watch out for</h4>
        <p>Over-reflection — the agent enters an infinite critique loop. Always set a max iteration count (2–3 is usually enough).</p>
      </div>
    </div>

    <div class="insight-box">
      <strong>Real example:</strong> A code-writing agent generates a function → runs it against test cases → sees 2 failing tests → analyses the failures → rewrites the function → all tests pass → ships the code. This is Reflection in action.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 10: Tool Use Pattern ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">10</div>
    <h2>Pattern 2 — Tool Use</h2>
    <span class="topic-time">30 min</span>
  </div>
  <div class="topic-body">
    <p>The Tool Use pattern gives the agent the ability to <strong>call external functions</strong> when the LLM's built-in knowledge isn't sufficient. This is what transforms a chatbot into an agent — the ability to reach out and affect the real world.</p>

    <div class="loop-box">
      <span class="green">Need info/action</span> <span class="dim">──►</span> <span class="blue">Select tool</span> <span class="dim">──►</span> <span class="purple">Call tool</span> <span class="dim">──►</span> <span class="yellow">Observe result</span> <span class="dim">──►</span> <span class="green">Continue reasoning</span>
    </div>

    <h3>Tool selection strategies</h3>
    <table class="cmp-table">
      <thead><tr><th>Strategy</th><th>How It Works</th><th>Pros</th><th>Cons</th></tr></thead>
      <tbody>
        <tr><td><strong>LLM-driven</strong></td><td>LLM reads tool descriptions and picks the best one</td><td>Flexible, handles novel situations</td><td>Can hallucinate tools or pick wrong one</td></tr>
        <tr><td><strong>Rule-based routing</strong></td><td>Keywords or intent triggers specific tools</td><td>Deterministic, predictable</td><td>Brittle, can't handle ambiguity</td></tr>
        <tr><td><strong>Hybrid</strong></td><td>Rules handle common cases, LLM handles edge cases</td><td>Best balance</td><td>More complex to implement</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>Production tip:</strong> Write tool descriptions as if they're API docs for a junior developer. The LLM decides which tool to call based almost entirely on the description. Vague descriptions → wrong tool selections → failed tasks. Be specific about what the tool does, what it needs, and what it returns.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 11: Planning Pattern ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">11</div>
    <h2>Pattern 3 — Planning</h2>
    <span class="topic-time">30 min</span>
  </div>
  <div class="topic-body">
    <p>The Planning pattern has the agent <strong>decompose a complex goal into an ordered sequence of steps before executing any of them</strong>. Think before you do — the opposite of the reactive approach.</p>

    <div class="loop-box">
      <span class="green">Complex Goal</span> <span class="dim">──►</span> <span class="blue">Decompose into Sub-tasks</span> <span class="dim">──►</span> <span class="purple">Order & Prioritise</span> <span class="dim">──►</span> <span class="yellow">Execute Step-by-Step</span>
    </div>

    <h3>Planning strategies</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>📝 Linear planning</h4>
        <p>Simple ordered list: Step 1 → Step 2 → Step 3. Works when subtasks have clear dependencies and no parallelism.</p>
      </div>
      <div class="block-card">
        <h4>🌳 Tree-of-thought</h4>
        <p>Explore multiple possible plans simultaneously, score each branch, and commit to the best one. Higher quality, much higher cost.</p>
      </div>
      <div class="block-card">
        <h4>🔄 Adaptive re-planning</h4>
        <p>Start with a plan, but re-plan after each step based on what's observed. Handles uncertainty well. This is how most production agents work.</p>
      </div>
      <div class="block-card">
        <h4>📊 DAG planning</h4>
        <p>Represent subtasks as a directed acyclic graph. Independent tasks run in parallel. Dependent tasks wait. Maximises throughput.</p>
      </div>
    </div>

    <div class="insight-box">
      <strong>When planning hurts:</strong> If the task is simple enough to solve in 1–2 tool calls, planning adds unnecessary latency and cost. Use planning only when the goal genuinely requires 3+ steps with dependencies between them.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 12: ReAct & ReWOO ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">12</div>
    <h2>Pattern 4 — ReAct and ReWOO</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>These are the two most influential reasoning-and-action paradigms in agentic AI. They represent fundamentally different philosophies about <em>when</em> to think and <em>when</em> to act.</p>

    <h3>ReAct — Reasoning and Acting (interleaved)</h3>
    <p>The agent <strong>alternates between thinking and doing</strong>. After each action, it observes the result, reasons about it, then decides the next action. Think one step → do one step → observe → repeat.</p>

    <div class="arch-diagram">
      <div class="title">ReAct LOOP</div>
      <div style="margin-top: 8px;"><span class="blue">Thought 1:</span> <span class="dim">"I need to search for flights from DEL to BOM"</span></div>
      <div><span class="green">Action 1:</span> <span class="dim">search_flights(from="DEL", to="BOM", date="2026-04-04")</span></div>
      <div><span class="yellow">Observation 1:</span> <span class="dim">[IndiGo ₹4200, Air India ₹4800, SpiceJet ₹5400]</span></div>
      <div style="margin-top: 6px;"><span class="blue">Thought 2:</span> <span class="dim">"SpiceJet is over budget. IndiGo is cheapest. Let me book IndiGo."</span></div>
      <div><span class="green">Action 2:</span> <span class="dim">book_flight(airline="IndiGo", flight_id="6E-2431", ...)</span></div>
      <div><span class="yellow">Observation 2:</span> <span class="dim">"Error: fare no longer available"</span></div>
      <div style="margin-top: 6px;"><span class="blue">Thought 3:</span> <span class="dim">"IndiGo sold out. Air India ₹4800 is still within budget. Switching."</span></div>
      <div><span class="green">Action 3:</span> <span class="dim">book_flight(airline="Air India", flight_id="AI-680", ...)</span></div>
      <div><span class="yellow">Observation 3:</span> <span class="dim">"Booking confirmed. PNR: ABC123"</span></div>
      <div style="margin-top: 6px;"><span class="blue">Thought 4:</span> <span class="dim">"Booking done. Now send confirmation email."</span></div>
      <div><span class="green">Action 4:</span> <span class="dim">send_email(to="user@example.com", subject="Flight booked", ...)</span></div>
      <div><span class="purple">Final:</span> <span class="dim">"Done. Air India flight AI-680 booked for ₹4,800. Confirmation sent."</span></div>
    </div>

    <h3>ReWOO — Reasoning Without Observation (plan-first)</h3>
    <p>The agent <strong>plans all steps upfront before executing any of them</strong>. It generates the entire plan, then executes sequentially, substituting results as they come in. Think all steps → do all steps.</p>

    <div class="arch-diagram">
      <div class="title">ReWOO APPROACH</div>
      <div style="margin-top: 8px;"><span class="purple">Plan:</span></div>
      <div><span class="dim">  #E1 = search_flights(from="DEL", to="BOM", date="2026-04-04")</span></div>
      <div><span class="dim">  #E2 = filter_by_budget(results=#E1, max_price=5000)</span></div>
      <div><span class="dim">  #E3 = pick_cheapest(flights=#E2)</span></div>
      <div><span class="dim">  #E4 = book_flight(flight=#E3, passenger=user_profile)</span></div>
      <div><span class="dim">  #E5 = send_email(to=user_email, booking=#E4)</span></div>
      <div style="margin-top: 8px;"><span class="green">Execute:</span> <span class="dim">Run #E1 → substitute into #E2 → run #E2 → ... → #E5</span></div>
      <div><span class="yellow">Solve:</span> <span class="dim">Combine all results into final answer</span></div>
    </div>

    <h3>Head-to-head comparison</h3>
    <table class="cmp-table">
      <thead><tr><th></th><th>ReAct</th><th>ReWOO</th></tr></thead>
      <tbody>
        <tr><td><strong>Philosophy</strong></td><td>Think-act-observe in a tight loop</td><td>Plan everything, then execute</td></tr>
        <tr><td><strong>LLM calls</strong></td><td>Many — one per step (expensive)</td><td>Few — one planning call + one solving call (cheaper)</td></tr>
        <tr><td><strong>Adaptability</strong></td><td>Excellent — adapts after every observation</td><td>Limited — plan can break if an early step fails</td></tr>
        <tr><td><strong>Error handling</strong></td><td>Graceful — re-plans mid-task</td><td>Brittle — needs fallback strategy for failed steps</td></tr>
        <tr><td><strong>Latency</strong></td><td>Higher (many LLM round trips)</td><td>Lower (fewer LLM calls, can parallelize tools)</td></tr>
        <tr><td><strong>Best for</strong></td><td>Dynamic tasks with uncertainty</td><td>Predictable tasks with clear step order</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>Practical guidance:</strong> Use <strong>ReAct</strong> when the task involves uncertainty, external APIs that might fail, or user-dependent decisions. Use <strong>ReWOO</strong> when the task is predictable, cost matters, and you want parallelisable execution. Many production systems use a <strong>hybrid</strong>: plan with ReWOO, but switch to ReAct-style re-planning when a step fails.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 13: Multi-Agent Pattern ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">13</div>
    <h2>Pattern 5 — Multi-Agent Coordination</h2>
    <span class="topic-time">30 min</span>
  </div>
  <div class="topic-body">
    <p>The Multi-Agent pattern splits a complex task across multiple specialised agents, each with its own system prompt, tools, and expertise. An orchestrator coordinates them.</p>

    <div class="arch-diagram">
      <div class="title">MULTI-AGENT COORDINATION PATTERN</div>
      <div style="margin-top:8px;"><span class="yellow">┌─────────────────────────────────────────────────┐</span></div>
      <div><span class="yellow">│         ORCHESTRATOR AGENT                      │</span></div>
      <div><span class="yellow">│</span>  <span class="dim">Receives goal → delegates → merges results</span>    <span class="yellow">│</span></div>
      <div><span class="yellow">└───────┬──────────┬──────────┬──────────┬────────┘</span></div>
      <div><span class="dim">        │          │          │          │</span></div>
      <div><span class="dim">   ┌────▼────┐ ┌───▼────┐ ┌──▼───┐ ┌───▼────┐</span></div>
      <div><span class="dim">   │</span><span class="green">Research</span><span class="dim">│ │</span><span class="blue">Writer</span> <span class="dim">│ │</span><span class="purple">Critic</span><span class="dim">│ │</span><span class="orange">Editor</span> <span class="dim">│</span></div>
      <div><span class="dim">   │</span><span class="green"> Agent  </span><span class="dim">│ │</span><span class="blue">Agent</span>  <span class="dim">│ │</span><span class="purple">Agent</span> <span class="dim">│ │</span><span class="orange">Agent</span>  <span class="dim">│</span></div>
      <div><span class="dim">   └─────────┘ └────────┘ └──────┘ └────────┘</span></div>
      <div style="color: #64748b; font-size: 11px; margin-top: 8px;">Each agent: own system prompt + own tools + own memory scope</div>
    </div>

    <h3>When to use multi-agent</h3>
    <ul style="padding-left: 20px; margin-bottom: 16px;">
      <li><strong>Diverse expertise needed</strong> — the task requires knowledge/tools that don't fit in one prompt</li>
      <li><strong>Quality through adversarial review</strong> — one agent writes, another critiques (Reflection + Multi-Agent combined)</li>
      <li><strong>Parallel execution</strong> — independent subtasks can run simultaneously</li>
      <li><strong>Separation of concerns</strong> — each agent has a clear, bounded responsibility</li>
    </ul>

    <h3>Common pitfalls</h3>
    <div class="blocks-grid" style="grid-template-columns: 1fr;">
      <div class="block-card" style="border-left: 3px solid #fca5a5;">
        <h4>⚠️ Pitfalls to avoid</h4>
        <p><strong>1. Too many agents</strong> — every extra agent adds latency, cost, and debugging complexity. Start with 2–3 agents max.<br>
        <strong>2. Vague role boundaries</strong> — if two agents overlap in responsibility, they'll conflict or duplicate work.<br>
        <strong>3. No shared context</strong> — agents that can't see each other's intermediate results will produce disconnected outputs.<br>
        <strong>4. Missing error propagation</strong> — if one agent fails silently, the orchestrator keeps going with incomplete data.</p>
      </div>
    </div>

    <div class="insight-box">
      <strong>Pattern combinations:</strong> The five patterns aren't mutually exclusive. A production agent often combines them — e.g., ReAct for the main loop, Tool Use for each step, Reflection for quality gates, Planning for complex subtasks, and Multi-Agent when one role isn't enough. Master each one individually first.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>For each of the 5 patterns, write a one-line summary in your notes</li>
        <li>Draw a diagram showing how ReAct and ReWOO differ (side by side)</li>
        <li>Think of a task where you'd combine Reflection + Multi-Agent. Describe the agent roles.</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day4 -->

<!-- ═══════════════════════════════════════════════
     DAY 5 — Design Considerations + Hands-on Labs
     ═══════════════════════════════════════════════ -->
<div id="day5" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d5prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 5 overview</div>
  <div class="sched-body">
    <h4>Bring it all together — trade-offs and hands-on practice</h4>
    <p>Design considerations + 2 labs · ~3 hours · Apply architecture + patterns to real scenarios</p>
  </div>
</div>

<!-- ── TOPIC 14: Design Considerations ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">14</div>
    <h2>Design Considerations — Choosing the Right Architecture and Pattern</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>Now that you know the five architecture families and five design patterns, the practical question is: <strong>how do you choose?</strong> Here's a decision framework.</p>

    <h3>The four trade-off axes</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>⚡ Latency vs. Quality</h4>
        <p>More reasoning steps (Reflection, ReAct) → higher quality but slower response. Reactive / ReWOO → faster but less adaptive. Match to your user's tolerance — a customer chat needs seconds; a research report can take minutes.</p>
      </div>
      <div class="block-card">
        <h4>💰 Cost vs. Capability</h4>
        <p>Every LLM call costs money. ReAct with 10 loop iterations costs 10x more than ReWOO with 2 calls. Multi-agent systems multiply the cost by the number of agents. Budget early — a $0.50/task agent at 10K tasks/day = $5,000/day.</p>
      </div>
      <div class="block-card">
        <h4>🔧 Simplicity vs. Flexibility</h4>
        <p>Reactive architectures are dead simple but brittle. Hybrid architectures handle edge cases but require more engineering. Start simple and add complexity only when you've hit a wall.</p>
      </div>
      <div class="block-card">
        <h4>🛡 Autonomy vs. Safety</h4>
        <p>More autonomy = faster task completion but higher risk. Add HITL checkpoints proportional to the irreversibility and cost of the actions. The formula: (action cost × probability of error) = determines whether to pause for human review.</p>
      </div>
    </div>

    <h3>Decision matrix — quick reference</h3>
    <table class="fw-table">
      <thead><tr><th>Your Situation</th><th>Recommended Architecture</th><th>Recommended Pattern</th></tr></thead>
      <tbody>
        <tr><td>Simple task, fast response needed</td><td>Reactive</td><td>Tool Use</td></tr>
        <tr><td>Multi-step task, predictable flow</td><td>Deliberative / Layered</td><td>Planning + ReWOO</td></tr>
        <tr><td>Multi-step task, uncertain environment</td><td>Hybrid (BDI)</td><td>ReAct</td></tr>
        <tr><td>Quality-critical output (code, reports)</td><td>Hybrid</td><td>Reflection + Tool Use</td></tr>
        <tr><td>Complex task requiring diverse expertise</td><td>Layered / Event-driven</td><td>Multi-Agent + Planning</td></tr>
        <tr><td>Long-running workflow (hours/days)</td><td>Event-driven</td><td>Planning + Multi-Agent</td></tr>
        <tr><td>Cost-sensitive with many requests</td><td>Reactive or Deliberative</td><td>ReWOO</td></tr>
      </tbody>
    </table>

    <h3>Scalability considerations</h3>
    <ul style="padding-left: 20px; margin-bottom: 16px;">
      <li><strong>Stateless tools</strong> — tools should not maintain internal state. All state lives in the agent's memory. This makes tools reusable and agents restartable.</li>
      <li><strong>Horizontal scaling</strong> — in a multi-agent system, each agent can run on a separate node. Use message queues (Redis, Kafka) for inter-agent communication.</li>
      <li><strong>Caching</strong> — cache LLM responses for identical inputs. Cache tool results with appropriate TTLs. This can reduce costs by 30–50% in production.</li>
      <li><strong>Graceful degradation</strong> — if the LLM provider is down, fall back to a simpler model. If a tool is unavailable, skip that step and flag it for human follow-up.</li>
    </ul>

    <div class="insight-box">
      <strong>The golden rule of agent architecture:</strong> Build the simplest system that solves the problem reliably. Every added component (extra agent, extra pattern, extra tool) is both capability and liability. Measure twice, architect once.
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── HANDS-ON LAB 1 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background: var(--earth);">L1</div>
    <h2>Lab 1 — Designing an AI Agent Architecture</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <div class="lab-box">
      <h4>🛠 Hands-on Exercise — Architect an Agent System</h4>
      <p style="margin-bottom: 12px;">Choose <strong>one</strong> of the following scenarios and design a complete agent architecture:</p>

      <div class="blocks-grid" style="margin-bottom: 16px;">
        <div class="block-card" style="border-left: 3px solid var(--gum);">
          <h4>Scenario A: Automated Code Reviewer</h4>
          <p>An agent that reviews pull requests: reads the diff, identifies bugs, suggests improvements, checks test coverage, and posts comments on the PR.</p>
        </div>
        <div class="block-card" style="border-left: 3px solid var(--earth);">
          <h4>Scenario B: Personal Finance Advisor</h4>
          <p>An agent that monitors your bank transactions, categorises expenses, detects unusual spending, and generates a weekly summary with savings tips.</p>
        </div>
        <div class="block-card" style="border-left: 3px solid #6366f1;">
          <h4>Scenario C: Research Paper Summariser</h4>
          <p>An agent that takes an academic topic, finds relevant papers, reads them, extracts key findings, and generates a structured literature review.</p>
        </div>
        <div class="block-card" style="border-left: 3px solid #0ea5e9;">
          <h4>Scenario D: Customer Onboarding Agent</h4>
          <p>An agent that guides new customers through setup: collects info, creates accounts, configures preferences, and schedules a welcome call.</p>
        </div>
      </div>

      <p style="margin-bottom: 8px;">For your chosen scenario, produce these deliverables:</p>
      <ol>
        <li><strong>Architecture type:</strong> Which of the five architecture families fits best? Justify your choice.</li>
        <li><strong>Module diagram:</strong> Draw all six modules (Perception, Cognitive, Action, Learning, Collaboration, Security) and show how data flows between them.</li>
        <li><strong>Tool registry:</strong> List every tool the agent needs with: name, description, input params, output format, required permissions.</li>
        <li><strong>Memory design:</strong> What goes in working memory? Episodic? Semantic? How long is each retained?</li>
        <li><strong>Security plan:</strong> Define the permission matrix, action budgets, and HITL checkpoints.</li>
        <li><strong>Agent walkthrough:</strong> Step through a sample user request from start to finish — show the agent loop running.</li>
      </ol>
    </div>

  </div>
</div>

<hr class="section-divider">

<!-- ── HANDS-ON LAB 2 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background: var(--earth);">L2</div>
    <h2>Lab 2 — Implementing Design Patterns on Paper</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <div class="lab-box">
      <h4>🛠 Hands-on Exercise — Pattern Implementation</h4>
      <p style="margin-bottom: 12px;">Using the same scenario from Lab 1, implement each design pattern <strong>on paper</strong> (or in a doc/notebook):</p>
      <ol>
        <li>
          <strong>Reflection pattern:</strong> Show the generate → critique → revise loop for your agent.
          <ul>
            <li>What does the agent generate first?</li>
            <li>What criteria does the critic check?</li>
            <li>Show the before and after of a revision cycle.</li>
          </ul>
        </li>
        <li>
          <strong>Tool Use pattern:</strong> Write out 3 tool calls your agent would make.
          <ul>
            <li>For each: show the structured tool call JSON and the expected response.</li>
            <li>What happens if the tool returns an error?</li>
          </ul>
        </li>
        <li>
          <strong>ReAct vs. ReWOO:</strong> Trace the same 5-step task through both approaches.
          <ul>
            <li>ReAct: Write out Thought → Action → Observation for each step.</li>
            <li>ReWOO: Write the full plan with #E1, #E2, ... variable substitution.</li>
            <li>Count the number of LLM calls in each approach.</li>
          </ul>
        </li>
        <li>
          <strong>Multi-Agent pattern:</strong> If your scenario needed 3 specialised agents:
          <ul>
            <li>Define each agent's role, system prompt summary, and tools.</li>
            <li>Draw the communication flow between them.</li>
            <li>Show how the orchestrator merges their outputs.</li>
          </ul>
        </li>
      </ol>
    </div>

    <div class="insight-box">
      <strong>Why on paper?</strong> Coding comes in the next units (LangChain, LangGraph, CrewAI). Right now, the goal is to internalise the patterns so deeply that when you start coding, you already know <em>what</em> to build — you just need to learn the framework's syntax. This saves weeks of trial-and-error.
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
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Architecture matters</strong> — it determines how data flows between LLM, tools, memory, and the world</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Five architecture types</strong> — Reactive, Deliberative, Hybrid (BDI), Layered, Event-driven</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Perception Module</strong> — parses inputs into structured context the agent can reason over</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cognitive Module</strong> — the LLM-powered brain: reasoning, planning, decision-making, self-correction</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Action Module</strong> — tool registry, validation, execution, observation formatting</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Learning Module</strong> — working, episodic, semantic, and procedural memory</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Collaboration Module</strong> — broadcast, direct, blackboard, pipeline communication</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Security Module</strong> — input guards, permissions, validation, budgets, audit trails</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Reflection pattern</strong> — generate → self-critique → revise loop</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Tool Use pattern</strong> — select and call external functions based on need</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Planning pattern</strong> — decompose complex goals into ordered sub-tasks</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>ReAct vs ReWOO</strong> — interleaved think-act vs plan-first-then-execute</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Multi-Agent pattern</strong> — specialised agents + orchestrator coordination</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Trade-offs</strong> — latency vs quality, cost vs capability, simplicity vs flexibility, autonomy vs safety</span></div>
</div>

<h3 style="font-size: 17px; margin-top: 24px; margin-bottom: 12px;">Check Your Understanding</h3>
<p style="font-size: 14px; margin-bottom: 8px;">Before moving to Unit 3, make sure you can answer:</p>
<ol style="padding-left: 20px; font-size: 14px; line-height: 1.8;">
  <li>What are the five architecture types and when would you pick each one?</li>
  <li>Explain the six framework modules and how data flows through them.</li>
  <li>What is the Reflection pattern and when does it hurt more than it helps?</li>
  <li>Compare ReAct and ReWOO — when would you choose each? When would you combine them?</li>
  <li>Design a multi-agent system for ANY task — define roles, communication, and the orchestrator's logic.</li>
  <li>What are the five layers of agent security and why is each one non-negotiable?</li>
  <li>You have a task that costs $0.50 per execution and runs 10,000 times/day. How do you reduce the cost by 40%?</li>
</ol>

<div style="margin-top: 24px; display: flex; gap: 12px; flex-wrap: wrap; justify-content: center;">
  <a href="/blog/2026/03/21/m1-agentic-ai-essentials/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gray-200); color: var(--gray-700); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    ← Unit 1
  </a>
  <a href="/courses/agentic-ai-engineering/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gum); color: var(--white); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    Course Overview
  </a>
  <a href="/blog/2026/04/11/u3-chain-composition-langchain/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gray-200); color: var(--gray-700); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px;">
    Unit 3 &rarr;
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
