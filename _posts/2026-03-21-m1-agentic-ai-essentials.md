---
layout: default
title: "Unit 1 — Agentic AI Essentials"
date: 2026-03-21
categories: [agentic-ai, foundations]
permalink: /blog/2026/03/21/m1-agentic-ai-essentials/
description: "Your starting point for building autonomous AI systems. Covers core concepts, three-way AI comparison, the agent loop, building blocks, human-in-the-loop, multi-agent thinking, frameworks, ethics, and hands-on exercises."
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
.day-tabs { display: flex; gap: 4px; margin-bottom: 0; border-bottom: 2px solid var(--gray-200); }
.day-tab { padding: 10px 20px; font-size: 14px; font-weight: 500; cursor: pointer; border: none; background: none; color: var(--gray-500); border-bottom: 2px solid transparent; margin-bottom: -2px; transition: all var(--transition); }
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

/* ── Step cards (agent walkthrough) ── */
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

/* ── Comparison cards ── */
.compare-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin: 20px 0; }
@media (max-width: 640px) { .compare-grid { grid-template-columns: 1fr; } }
.compare-card { border-radius: var(--radius-md); padding: 18px; border: 1px solid var(--gray-200); background: var(--white); }
.compare-card.highlight { border-color: var(--gum); box-shadow: 0 0 0 1px var(--gum); }
.compare-card h4 { font-size: 14px; margin-bottom: 8px; font-weight: 600; }
.compare-card h4.trad { color: var(--gray-500); }
.compare-card h4.gen  { color: var(--earth); }
.compare-card h4.agent { color: var(--gum); }
.compare-card p { font-size: 13px; color: var(--gray-700); line-height: 1.6; }

/* ── Comparison table ── */
.cmp-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 13.5px; }
.cmp-table th { text-align: left; padding: 10px 12px; background: var(--gray-100); font-weight: 600; font-size: 12px; text-transform: uppercase; letter-spacing: 0.4px; }
.cmp-table td { padding: 10px 12px; border-bottom: 1px solid var(--gray-200); }
.cmp-table tr:last-child td { border-bottom: none; }
.cmp-table tr:hover td { background: rgba(84,100,20,0.03); }

/* ── Agent loop SVG area ── */
.loop-diagram { text-align: center; margin: 24px 0; }
.loop-diagram svg { max-width: 420px; width: 100%; }

/* ── Building blocks grid ── */
.blocks-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; margin: 16px 0; }
@media (max-width: 560px) { .blocks-grid { grid-template-columns: 1fr; } }
.block-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-sm); padding: 14px 16px; }
.block-card h4 { font-size: 14px; font-weight: 600; margin-bottom: 4px; display: flex; align-items: center; gap: 6px; }
.block-card p { font-size: 13px; color: var(--gray-700); line-height: 1.55; margin: 0; }

/* ── Framework landscape ── */
.fw-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 13.5px; }
.fw-table th { text-align: left; padding: 10px 12px; background: var(--gum); color: var(--white); font-weight: 600; font-size: 12px; text-transform: uppercase; letter-spacing: 0.4px; }
.fw-table td { padding: 10px 12px; border-bottom: 1px solid var(--gray-200); }

/* ── Day schedule cards ── */
.sched-card { background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-md); padding: 16px 20px; margin-bottom: 12px; display: flex; gap: 14px; align-items: flex-start; }
.sched-time { font-size: 12px; font-weight: 600; color: var(--gum); white-space: nowrap; min-width: 90px; padding-top: 2px; }
.sched-body h4 { font-size: 15px; font-weight: 600; margin-bottom: 4px; }
.sched-body p { font-size: 13px; color: var(--gray-700); line-height: 1.5; margin: 0; }
.sched-dur { margin-left: auto; font-size: 11px; color: var(--gray-500); background: var(--gray-100); padding: 2px 8px; border-radius: 10px; white-space: nowrap; align-self: flex-start; }

/* ── Lab / exercise ── */
.lab-box { background: linear-gradient(135deg, rgba(172,100,46,0.06), rgba(172,100,46,0.02)); border: 1px solid rgba(172,100,46,0.2); border-radius: var(--radius-md); padding: 20px 22px; margin: 20px 0; }
.lab-box h4 { font-size: 15px; font-weight: 600; color: var(--earth); margin-bottom: 8px; display: flex; align-items: center; gap: 6px; }
.lab-box ol, .lab-box ul { padding-left: 20px; }
.lab-box li { font-size: 14px; line-height: 1.7; margin-bottom: 4px; }

/* ── Ethics risk row ── */
.risk-cards { display: flex; flex-direction: column; gap: 10px; margin: 16px 0; }
.risk-row { display: flex; gap: 12px; background: var(--white); border: 1px solid var(--gray-200); border-radius: var(--radius-sm); padding: 14px 16px; align-items: flex-start; }
.risk-icon { font-size: 22px; flex-shrink: 0; }
.risk-row h5 { font-size: 14px; font-weight: 600; margin-bottom: 2px; }
.risk-row p { font-size: 13px; color: var(--gray-700); line-height: 1.5; margin: 0; }
.risk-chip { display: inline-block; font-size: 11px; padding: 2px 8px; border-radius: 4px; background: rgba(84,100,20,0.08); color: var(--gum); font-weight: 500; margin-top: 4px; }

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

/* ── Responsive ── */
@media (max-width: 768px) {
  .mod-hero h1 { font-size: 24px; }
  .topic-body { padding-left: 0; }
  .step-card { flex-direction: column; gap: 10px; }
  .sched-card { flex-direction: column; gap: 6px; }
  .sched-time { min-width: auto; }
  .sched-dur { margin-left: 0; }
}
</style>

<div class="mod-page">

<!-- Breadcrumb -->
<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 1</span>
</nav>

<!-- Hero -->
<div class="mod-hero">
  <h1>Unit 1 — Agentic AI Essentials</h1>
  <p class="mod-hero-sub">Your starting point. What makes AI <em>agentic</em>? How is it different from chatbots and traditional software? By the end of this module you'll think in agent loops, not chat prompts.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track A · Groundwork</span>
    <span class="mod-pill time">⏱ ~12 hrs across 5 days</span>
    <span class="mod-pill hands">🛠 2 hands-on labs</span>
  </div>
</div>

<!-- Objectives -->
<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Define Agentic AI and explain how it differs from Traditional AI and Generative AI</li>
    <li>Describe the agent core loop: perceive → plan → act → learn</li>
    <li>Identify the building blocks of any AI agent system</li>
    <li>Explain Human-in-the-Loop vs fully autonomous designs</li>
    <li>Compare single-agent and multi-agent architectures</li>
    <li>Map the current framework landscape (LangChain, CrewAI, Autogen …)</li>
    <li>Apply ethical and responsible AI principles to agent design</li>
    <li>Analyse real agent use cases end-to-end</li>
  </ul>
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
     DAY 1 — Topics 1, 2, 3
     ═══════════════════════════════════════════════ -->
<div id="day1" class="day-panel active">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d1prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 1 overview</div>
  <div class="sched-body">
    <h4>Set the foundation — what AI actually is today</h4>
    <p>Three topics · ~3 hours · Cover: Agentic AI definition, Agents vs Agentic AI, and the three-way comparison</p>
  </div>
</div>

<!-- ── TOPIC 1 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">1</div>
    <h2>Agentic AI — What It Is And Why It Matters Now</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p><strong>Traditional AI</strong> answers questions. <strong>Generative AI</strong> creates content. <strong>Agentic AI</strong> actually <em>does things</em> — it perceives a goal, plans steps, uses tools, takes actions, and learns from results — all autonomously.</p>

    <div class="insight-box">
      <strong>The one-liner:</strong> Agentic AI is AI that pursues goals autonomously over multiple steps — without a human guiding each one.
    </div>

    <h3>The Four Core Traits</h3>
    <p>Every agentic system shares four capabilities that separate it from simpler AI:</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>👁 Perception</h4>
        <p>Reads and understands the goal, the context, and real-time signals from its environment.</p>
      </div>
      <div class="block-card">
        <h4>🧠 Planning</h4>
        <p>Breaks a complex goal into an ordered set of sub-tasks. Decides which tools to call and in what order.</p>
      </div>
      <div class="block-card">
        <h4>⚡ Action</h4>
        <p>Executes steps by calling APIs, running code, controlling browsers, sending messages — it has <em>hands</em>.</p>
      </div>
      <div class="block-card">
        <h4>🔄 Learning</h4>
        <p>Observes the result of each action, updates its plan, and remembers outcomes across sessions.</p>
      </div>
    </div>

    <h3>Why a chatbot is <em>not</em> an agent</h3>
    <p>A chatbot reacts to one message. An agent pursues a multi-step goal without being hand-held. A chatbot doesn't remember yesterday's conversation; an agent tracks your preferences across sessions. A chatbot cannot open a website; an agent can browse, book, and pay.</p>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Open a notes doc and title it <strong>"Module 1 Notes"</strong></li>
        <li>Write your own definition of Agentic AI in 2 sentences</li>
        <li>Think of 1 boring repetitive task in your life that an agent could handle for you</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 2 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">2</div>
    <h2>AI Agents vs. Agentic AI — The Crucial Distinction</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>These two terms are often used interchangeably, but they mean different things:</p>
    <ul style="margin-bottom:16px; padding-left:20px;">
      <li><strong>AI Agent</strong> — a single autonomous unit that can perceive, reason, and act.</li>
      <li><strong>Agentic AI</strong> — the broader paradigm / system where multiple agents (or one agent with many capabilities) work together to achieve complex goals.</li>
    </ul>

    <div class="insight-box">
      <strong>Analogy:</strong> A soldier is an agent. An army is an agentic system. One soldier can complete a mission; but winning a campaign requires coordinated units with different specialisations — reconnaissance, logistics, communications.
    </div>

    <table class="cmp-table">
      <thead><tr><th></th><th>AI Agent (the unit)</th><th>Agentic AI (the system)</th></tr></thead>
      <tbody>
        <tr><td><strong>Scope</strong></td><td>Single task or workflow</td><td>Complex, multi-step campaigns</td></tr>
        <tr><td><strong>Components</strong></td><td>One LLM + tools + memory</td><td>Multiple agents + orchestrator + shared memory</td></tr>
        <tr><td><strong>Example</strong></td><td>A code-review agent</td><td>A dev team where agents write, test, review, and deploy code together</td></tr>
      </tbody>
    </table>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Draw a simple diagram in your notes: one box for "single agent" → a cluster of boxes for "agentic system"</li>
        <li>Label what each box would do in a customer-support scenario</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 3 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">3</div>
    <h2>The Three Eras of AI — Traditional → Generative → Agentic</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">

    <h3>Traditional AI — the rule-follower</h3>
    <p>Traditional AI is the oldest form — and simpler than people think. A human writes explicit rules, and the machine follows them exactly. No learning, no creativity, no surprises. Think of it as a very detailed instruction manual; the machine can only do what the manual says.</p>

    <div class="insight-box">
      <strong>Spam filter example:</strong> When you get an email, the filter runs a checklist a human wrote: Does the subject contain "FREE"? (+3 points). Unknown sender? (+2). More than 5 links? (+1). Score above 5 → spam folder. That's it. The moment a spammer writes "Fr33 m0ney," the old rule misses it — until a human manually writes a new rule.
    </div>

    <p><strong>Key insight:</strong> Traditional AI is a fast, tireless rule-checker. Its superpower is consistency and predictability — banks and medical devices still rely on it. Its weakness: the real world keeps changing, and someone must rewrite the rules every time.</p>

    <h3>Generative AI — the creator</h3>
    <p>The leap from "following rules" to "creating new things." Instead of a human writing every answer, the model learns patterns from massive data and generates original content — text, images, code, audio — that never existed before.</p>

    <div class="insight-box">
      <strong>ChatGPT example:</strong> When you type "Write an apology email to my manager for missing a deadline," the model doesn't look up a template. It has learned — from billions of examples — what patterns make a good apology: acknowledge the issue, take responsibility, offer a fix, keep a professional tone. It then predicts, word by word, the most likely fitting sequence. The result is genuinely original.
    </div>

    <p><strong>The crucial limitation:</strong> Generative AI only speaks — it never acts. Ask ChatGPT to book a flight and it'll write you the instructions. It cannot open a browser, compare prices, enter your card details, and confirm the booking. It has no hands. Every conversation starts fresh with no memory.</p>

    <h3>Agentic AI — the doer</h3>
    <p>Agentic AI takes the language understanding of Generative AI and adds three missing pieces: <strong>memory</strong>, <strong>tools</strong>, and <strong>autonomous multi-step action</strong>. It doesn't just respond — it pursues a goal until the job is done.</p>

    <!-- Step-by-step walkthrough -->
    <p style="color: var(--gray-500); font-size: 13px; margin-bottom: 8px;">
      <strong>Live example · Goal:</strong> "Book the cheapest DEL → BOM flight this Friday under ₹5,000 and email me the confirmation"
    </p>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num perceive">1</div>
        <div class="step-body">
          <div class="step-label perceive">PERCEIVE</div>
          <div class="step-title">Read and understand the goal</div>
          <div class="step-desc">The agent parses your request. It extracts: origin = Delhi, destination = Mumbai, date = this Friday, constraint = under ₹5,000, final action = send email. It now has a structured goal to work toward.</div>
        </div>
      </div>

      <div class="step-card">
        <div class="step-num plan">2</div>
        <div class="step-body">
          <div class="step-label plan">PLAN</div>
          <div class="step-title">Break the goal into sub-tasks</div>
          <div class="step-desc">It creates a step-by-step plan: (a) search flight APIs, (b) filter by price, (c) pick cheapest option, (d) fill booking form, (e) confirm payment, (f) send confirmation email. This planning step is powered by an LLM — the agent's reasons about what needs to happen.</div>
        </div>
      </div>

      <div class="step-card">
        <div class="step-num act">3</div>
        <div class="step-body">
          <div class="step-label act">ACT — step 1</div>
          <div class="step-title">Search flights using a tool</div>
          <div class="step-desc">It calls a flight search API and gets back results: Air India ₹4,800 · IndiGo ₹4,200 · SpiceJet ₹5,400. It filters out SpiceJet (over budget) and flags IndiGo as cheapest.</div>
          <div class="step-tools">
            <span class="tool-badge green">Flight search API</span>
            <span class="tool-badge blue">Web browser</span>
          </div>
        </div>
      </div>

      <div class="step-card">
        <div class="step-num act">4</div>
        <div class="step-body">
          <div class="step-label act">ACT — step 2</div>
          <div class="step-title">Fill the booking form autonomously</div>
          <div class="step-desc">It opens the IndiGo booking page, fills in passenger details from your profile, selects the seat, and proceeds to payment — all without you touching anything. It uses a browser-control tool to navigate the real website.</div>
          <div class="step-tools">
            <span class="tool-badge red">Browser control</span>
            <span class="tool-badge amber">User profile memory</span>
          </div>
        </div>
      </div>

      <div class="step-card">
        <div class="step-num learn">5</div>
        <div class="step-body">
          <div class="step-label learn">LEARN — adapt mid-task</div>
          <div class="step-title">Hit a problem — adapt without you</div>
          <div class="step-desc">The IndiGo ₹4,200 fare just sold out. The agent doesn't stop and ask you — it loops back, re-checks results, sees Air India ₹4,800 is still within budget, and switches. It logs the reason in memory.</div>
          <div class="step-tools">
            <span class="tool-badge amber">Memory</span>
            <span class="tool-badge blue">Re-planning</span>
          </div>
        </div>
      </div>

      <div class="step-card">
        <div class="step-num act">6</div>
        <div class="step-body">
          <div class="step-label act">ACT — final step</div>
          <div class="step-title">Email you the confirmation</div>
          <div class="step-desc">Booking confirmed. The agent calls your email tool, drafts a summary (flight details, PNR, check-in link), and sends it. Goal complete. You never opened a browser.</div>
          <div class="step-tools">
            <span class="tool-badge green">Email API</span>
            <span class="tool-badge blue">Calendar tool</span>
          </div>
        </div>
      </div>
    </div>

    <h3>The three pillars that make Agentic AI different</h3>
    <ol style="padding-left:20px; margin-bottom:16px;">
      <li><strong>Tools.</strong> An agent can call APIs, search the web, run code, control a browser, send emails. It has hands. Generative AI only has a mouth.</li>
      <li><strong>Memory.</strong> An agent remembers step 3 when it reaches step 6. It can also remember your name, preferences, and past interactions across sessions. Generative AI forgets everything when the chat ends.</li>
      <li><strong>Autonomous looping.</strong> When something goes wrong mid-task (fare sold out, website timed out), the agent replans and continues without asking for help — unless it truly cannot proceed. This is a <strong>Human-in-the-Loop</strong> system, which you'll study on Day 2.</li>
    </ol>

    <!-- Three-way comparison cards -->
    <h3>Same task — how each AI type handles it</h3>
    <div class="compare-grid">
      <div class="compare-card">
        <h4 class="trad">Traditional AI</h4>
        <p>Can only check if a flight exists in a predefined database. Cannot search, compare, book, or email. Completely stuck.</p>
      </div>
      <div class="compare-card">
        <h4 class="gen">Generative AI</h4>
        <p>Can write you the perfect step-by-step instructions for booking the flight. But <strong>you</strong> have to do every step yourself.</p>
      </div>
      <div class="compare-card highlight">
        <h4 class="agent">Agentic AI</h4>
        <p>Searches, compares, adapts when a fare sells out, books, and emails you — all on its own. Goal done.</p>
      </div>
    </div>

    <!-- Full comparison table -->
    <table class="cmp-table">
      <thead>
        <tr><th></th><th>Traditional AI</th><th>Generative AI</th><th>Agentic AI</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>How it works</strong></td><td>Human writes rules</td><td>Learns from data</td><td>Perceive → Plan → Act → Learn loop</td></tr>
        <tr><td><strong>What it produces</strong></td><td>Fixed decisions</td><td>Original content</td><td>Completed real-world tasks</td></tr>
        <tr><td><strong>Can it learn?</strong></td><td>No — rules are static</td><td>Yes — from training</td><td>Yes — during and across tasks</td></tr>
        <tr><td><strong>Can it take actions?</strong></td><td>Only predefined ones</td><td>No — only generates text</td><td>Yes — APIs, browsers, code, email</td></tr>
        <tr><td><strong>Memory</strong></td><td>None</td><td>Per-session only</td><td>Short-term + long-term</td></tr>
        <tr><td><strong>Real example</strong></td><td>Spam filter</td><td>ChatGPT, Copilot chat</td><td>Copilot Workspace, Klarna AI</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>The evolution in one line:</strong> Traditional AI is a rule book. Generative AI is a brilliant advisor. Agentic AI is a capable employee — you give it a goal, it figures out the steps, uses the right tools, and comes back when it's done.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Find 1 real product for each type and write it in your notes (Example: Traditional = Google's spam filter, Generative = ChatGPT, Agentic = GitHub Copilot Workspace)</li>
        <li>Self-quiz: can you explain each type in 1 sentence without looking at notes?</li>
      </ol>
    </div>

  </div>
</div>

</div><!-- /day1 -->

<!-- ═══════════════════════════════════════════════
     DAY 2 — Topics 4, 5, 6
     ═══════════════════════════════════════════════ -->
<div id="day2" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d2prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 2 overview</div>
  <div class="sched-body">
    <h4>Inside the machine — how agents are built</h4>
    <p>Three topics · ~3 hours · Cover: Building blocks, autonomous agents, human-in-the-loop systems</p>
  </div>
</div>

<!-- ── TOPIC 4 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">4</div>
    <h2>Agentic AI Building Blocks</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>Every agent — from the simplest script to a production-grade system — is assembled from the same fundamental components. Master these, and every framework you encounter later will make instant sense.</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>🧠 LLM (Reasoning Engine)</h4>
        <p>The brain. Takes observations + chat history and decides the next action. GPT-4o, Claude 3, Gemini, Mistral — all can serve as the core engine.</p>
      </div>
      <div class="block-card">
        <h4>🔧 Tools</h4>
        <p>The hands. Any external function the agent can call: web search, code executor, database query, email sender, browser automation, file system access.</p>
      </div>
      <div class="block-card">
        <h4>💾 Memory</h4>
        <p>Short-term (within one task — what happened at step 3) and long-term (across sessions — user preferences, past results). Often backed by vector databases.</p>
      </div>
      <div class="block-card">
        <h4>📋 Planning Module</h4>
        <p>Decomposes a high-level goal into ordered sub-tasks. Strategies include ReAct (reason + act), chain-of-thought, tree-of-thought, or ReWOO (plan all steps first).</p>
      </div>
      <div class="block-card">
        <h4>🔁 Orchestrator</h4>
        <p>The loop controller. Runs the perceive → plan → act → observe cycle, routes between agents, handles retries and error recovery. LangGraph, CrewAI, Autogen are examples.</p>
      </div>
      <div class="block-card">
        <h4>🌍 Environment</h4>
        <p>Everything external the agent can observe and affect: APIs, file systems, web pages, databases, other agents. The agent both reads from and writes to its environment.</p>
      </div>
    </div>

    <!-- Agent loop diagram (text-based) -->
    <h3>The Agent Core Loop</h3>
    <div style="background: var(--gray-900); color: var(--white); border-radius: var(--radius-md); padding: 24px; margin: 16px 0; font-family: 'Fira Code', monospace; font-size: 13px; line-height: 1.8; text-align: center;">
      <div style="color: #a5b4fc;">┌──────────────────────────────────────┐</div>
      <div style="color: #a5b4fc;">│         <span style="color:#E0F82E; font-weight:600;">AGENT CORE LOOP</span>              │</div>
      <div style="color: #a5b4fc;">├──────────────────────────────────────┤</div>
      <div><span style="color: #6ee7b7;">Goal</span> ──► <span style="color: #93c5fd;">Perceive</span> ──► <span style="color: #c4b5fd;">Plan</span> ──► <span style="color: #fcd34d;">Act</span></div>
      <div style="color: #64748b;">                ▲                    │</div>
      <div style="color: #64748b;">                │     <span style="color: #fca5a5;">Observe</span>       │</div>
      <div style="color: #64748b;">                └────────────────────┘</div>
      <div style="margin-top: 8px; color: #64748b; font-size: 11px;">Repeats until goal is achieved or agent asks for help</div>
    </div>

    <div class="insight-box">
      <strong>Key insight:</strong> The loop is what separates an agent from a chatbot. A chatbot does one pass: input → output. An agent does many passes: goal → reason → act → observe → adjust → act again → … → done.
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 5 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">5</div>
    <h2>Autonomous Agents — How Much Freedom Should They Have?</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>Not all agents are equally autonomous. The <strong>autonomy spectrum</strong> ranges from fully supervised (a human approves every action) to fully autonomous (the agent handles everything end-to-end).</p>

    <table class="cmp-table">
      <thead><tr><th>Level</th><th>Description</th><th>Example</th></tr></thead>
      <tbody>
        <tr><td><strong>Level 0</strong></td><td>No autonomy — human does everything, AI only suggests</td><td>Autocomplete in your IDE</td></tr>
        <tr><td><strong>Level 1</strong></td><td>AI executes one step at a time, human approves each</td><td>Copilot suggesting code line-by-line</td></tr>
        <tr><td><strong>Level 2</strong></td><td>AI plans and executes a full task, human reviews output</td><td>Agent writes an entire function, you review before merging</td></tr>
        <tr><td><strong>Level 3</strong></td><td>AI handles most tasks independently, escalates edge cases</td><td>Customer support agent that resolves 80% of tickets, routes 20% to humans</td></tr>
        <tr><td><strong>Level 4</strong></td><td>Fully autonomous — runs end-to-end with no human</td><td>Automated trading agent, self-healing infrastructure</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>Practical reality:</strong> Most production agents today operate at Level 2–3. Fully autonomous (Level 4) requires extremely high reliability, which current LLMs haven't achieved for all tasks. Design for the level your use case actually needs.
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 6 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">6</div>
    <h2>Human-in-the-Loop Systems</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p><strong>Human-in-the-Loop (HITL)</strong> is the design pattern where an agent operates autonomously for most steps but pauses and asks a human for approval before taking high-stakes actions.</p>

    <h3>When to insert a human checkpoint</h3>
    <ul style="padding-left:20px; margin-bottom:16px;">
      <li><strong>Irreversible actions</strong> — sending an email, making a payment, deleting data</li>
      <li><strong>High-cost mistakes</strong> — deploying code to production, executing financial transactions</li>
      <li><strong>Ambiguous intent</strong> — the user's goal could be interpreted multiple ways</li>
      <li><strong>Regulatory requirements</strong> — healthcare, finance, legal decisions that need human sign-off</li>
    </ul>

    <h3>HITL in the flight booking example</h3>
    <p>Remember the travel agent from Day 1? At step 4 (filling the booking form) and step 5 (switching airlines after sold-out fare), a well-designed HITL system would:</p>
    <ol style="padding-left:20px; margin-bottom:16px;">
      <li>Show you: "IndiGo ₹4,200 is sold out. Air India ₹4,800 is available. Shall I proceed?" </li>
      <li>Wait for your "Yes" before charging your card</li>
      <li>Then continue autonomously with the email confirmation</li>
    </ol>

    <div class="insight-box">
      <strong>Design principle:</strong> The best HITL systems are invisible when things go well and only surface when something unexpected happens. Users should feel the agent is autonomous, not that they're babysitting it.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Pick any agent use case (code review, customer support, data analysis)</li>
        <li>List every action the agent would take</li>
        <li>Mark which actions need a human checkpoint and which can run freely</li>
      </ol>
    </div>
  </div>
</div>

</div><!-- /day2 -->

<!-- ═══════════════════════════════════════════════
     DAY 3 — Topics 7, 8
     ═══════════════════════════════════════════════ -->
<div id="day3" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d3prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 3 overview</div>
  <div class="sched-body">
    <h4>One agent or many? Architectures that scale</h4>
    <p>Two topics · ~2.5 hours · Cover: Single vs multi-agent systems, frameworks landscape</p>
  </div>
</div>

<!-- ── TOPIC 7 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">7</div>
    <h2>Single-Agent vs. Multi-Agent Systems</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <h3>Single-agent architecture</h3>
    <p>One agent handles the entire task from start to finish. It has one LLM, one set of tools, one memory. Simple to build, easy to debug, works well for focused tasks.</p>

    <h3>Multi-agent architecture</h3>
    <p>Multiple specialised agents collaborate. Each owns a slice of the problem. An orchestrator agent coordinates them — routing tasks, combining results, handling failures.</p>

    <table class="cmp-table">
      <thead><tr><th></th><th>Single Agent</th><th>Multi-Agent System</th></tr></thead>
      <tbody>
        <tr><td><strong>Best for</strong></td><td>Focused tasks with clear scope</td><td>Complex workflows requiring diverse expertise</td></tr>
        <tr><td><strong>Complexity</strong></td><td>Low — one loop, one prompt</td><td>Higher — agent communication, routing, error cascades</td></tr>
        <tr><td><strong>Debugging</strong></td><td>Straightforward — single trace</td><td>Harder — must trace across multiple agents</td></tr>
        <tr><td><strong>Failure mode</strong></td><td>Agent gets stuck or hallucinates</td><td>Miscommunication between agents, infinite loops</td></tr>
        <tr><td><strong>Example</strong></td><td>Code review agent</td><td>Dev team: writer agent + tester agent + reviewer agent</td></tr>
      </tbody>
    </table>

    <div style="background: var(--gray-900); color: var(--white); border-radius: var(--radius-md); padding: 24px; margin: 16px 0; font-family: 'Fira Code', monospace; font-size: 13px; line-height: 1.8;">
      <div style="color: #a5b4fc; font-weight: 600; margin-bottom: 8px;">Multi-Agent Architecture</div>
      <div><span style="color: #fcd34d;">Orchestrator Agent</span></div>
      <div style="color: #64748b;">   ├── <span style="color: #6ee7b7;">Research Agent</span>    → gathers information</div>
      <div style="color: #64748b;">   ├── <span style="color: #93c5fd;">Writer Agent</span>      → drafts content</div>
      <div style="color: #64748b;">   ├── <span style="color: #c4b5fd;">Critic Agent</span>      → reviews and scores</div>
      <div style="color: #64748b;">   └── <span style="color: #fca5a5;">Publisher Agent</span>   → formats and ships</div>
    </div>

    <div class="insight-box">
      <strong>Rule of thumb:</strong> Start with a single agent. Only add more agents when you hit a clear capability boundary — when one agent can't hold all the tools, context, or expertise needed. Premature multi-agent design is the #1 cause of agent system complexity.
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 8 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">8</div>
    <h2>The Agentic AI Framework Landscape</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>You don't need to master these yet — you'll build with each one in later units. This is your map so you know what exists and when to reach for what.</p>

    <table class="fw-table">
      <thead><tr><th>Layer</th><th>Tools</th><th>You'll Learn In</th></tr></thead>
      <tbody>
        <tr><td><strong>LLMs (reasoning engines)</strong></td><td>OpenAI GPT-4o, Anthropic Claude 3, Google Gemini, Mistral, Llama 3</td><td>Used throughout</td></tr>
        <tr><td><strong>Agent frameworks</strong></td><td>LangChain, LangGraph, LlamaIndex, CrewAI, Autogen, Phidata</td><td>Units 3–8</td></tr>
        <tr><td><strong>Memory / Vector stores</strong></td><td>Chroma, Pinecone, Weaviate, pgvector</td><td>Unit 5</td></tr>
        <tr><td><strong>Tool integrations</strong></td><td>Tavily (web search), E2B (code sandbox), Browserbase (browser)</td><td>Units 3–4</td></tr>
        <tr><td><strong>Observability</strong></td><td>LangSmith, Langfuse, AgentOps</td><td>Unit 9</td></tr>
        <tr><td><strong>No/low-code builders</strong></td><td>Langflow, Relevance AI, Wordware</td><td>Unit 10</td></tr>
        <tr><td><strong>Cloud platforms</strong></td><td>AWS Bedrock, Azure OpenAI, GCP Vertex AI</td><td>Capstone</td></tr>
      </tbody>
    </table>

    <div class="insight-box">
      <strong>How to think about frameworks:</strong> They're all solving the same problem — running the agent loop — but with different trade-offs. LangGraph gives you maximum control. CrewAI makes multi-agent easy. Phidata is fastest to prototype. You'll develop opinions as you build with them.
    </div>
  </div>
</div>

</div><!-- /day3 -->

<!-- ═══════════════════════════════════════════════
     DAY 4 — Topics 9, 10
     ═══════════════════════════════════════════════ -->
<div id="day4" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d4prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 4 overview</div>
  <div class="sched-body">
    <h4>Responsible agents — ethics, safety, and best practices</h4>
    <p>Two topics · ~2.5 hours · Cover: Ethics and responsible AI, agentic AI best practices</p>
  </div>
</div>

<!-- ── TOPIC 9 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">9</div>
    <h2>Ethical and Responsible AI for Agents</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>Agentic systems introduce risks that don't exist with single LLM calls. Because the agent <em>acts in the world</em> — calling APIs, writing files, sending emails, making payments — mistakes have real consequences.</p>

    <h3>The six key risks of autonomous agents</h3>

    <div class="risk-cards">
      <div class="risk-row">
        <div class="risk-icon">🎭</div>
        <div>
          <h5>Hallucinated Tool Calls</h5>
          <p>The agent invents an API endpoint or fabricates parameters that don't exist, causing silent failures or unintended actions.</p>
          <span class="risk-chip">Mitigation: Strict tool schemas + output validation</span>
        </div>
      </div>
      <div class="risk-row">
        <div class="risk-icon">🎯</div>
        <div>
          <h5>Goal Mis-specification</h5>
          <p>The agent achieves exactly what you <em>said</em> but not what you <em>meant</em>. Like a genie granting wishes too literally.</p>
          <span class="risk-chip">Mitigation: Clear, constrained goal definitions + edge case tests</span>
        </div>
      </div>
      <div class="risk-row">
        <div class="risk-icon">💉</div>
        <div>
          <h5>Prompt Injection</h5>
          <p>Malicious content hidden in tool output or user input hijacks the agent's reasoning — making it ignore original instructions.</p>
          <span class="risk-chip">Mitigation: Sanitise observations + system-level guardrails</span>
        </div>
      </div>
      <div class="risk-row">
        <div class="risk-icon">🔄</div>
        <div>
          <h5>Runaway Actions</h5>
          <p>Agent takes far more (or far more destructive) actions than expected — sending 1,000 emails instead of 1, deleting wrong files.</p>
          <span class="risk-chip">Mitigation: Action budgets + HITL checkpoints</span>
        </div>
      </div>
      <div class="risk-row">
        <div class="risk-icon">🔓</div>
        <div>
          <h5>Data Leakage</h5>
          <p>Agent sends private data (credentials, PII, internal docs) to external tools or APIs it shouldn't have access to.</p>
          <span class="risk-chip">Mitigation: Tool-level permission scoping + audit logs</span>
        </div>
      </div>
      <div class="risk-row">
        <div class="risk-icon">⚖️</div>
        <div>
          <h5>Bias Amplification</h5>
          <p>Agent applies biased reasoning at scale across thousands of autonomous decisions — amplifying unfairness that a single human might catch.</p>
          <span class="risk-chip">Mitigation: Diverse evaluation sets + adversarial red-teaming</span>
        </div>
      </div>
    </div>

    <h3>Five principles for responsible agent design</h3>
    <ol style="padding-left:20px; margin-bottom: 16px;">
      <li><strong>Minimal footprint</strong> — request only the permissions the task actually needs</li>
      <li><strong>Prefer reversible actions</strong> — move to trash instead of permanent delete; draft before send</li>
      <li><strong>Human-in-the-loop</strong> — for consequential actions, require explicit approval</li>
      <li><strong>Full audit trail</strong> — log every action, tool call, and observation for post-hoc review</li>
      <li><strong>Fail safe</strong> — when uncertain, stop and ask rather than guess</li>
    </ol>
  </div>
</div>

<hr class="section-divider">

<!-- ── TOPIC 10 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">10</div>
    <h2>Agentic AI Best Practices</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>These are hard-won lessons from teams that have shipped agentic systems to production. Internalise them now, and you'll avoid the most common failure modes.</p>

    <div class="blocks-grid">
      <div class="block-card">
        <h4>🎯 Start simple, add complexity</h4>
        <p>Begin with a single agent + 2–3 tools. Only add agents when you hit a clear capability wall. Most "multi-agent" systems that fail started too complex.</p>
      </div>
      <div class="block-card">
        <h4>📝 Write crystal-clear system prompts</h4>
        <p>The system prompt is the agent's job description. Be explicit about what it can and cannot do, what tools are available, and when to ask for help.</p>
      </div>
      <div class="block-card">
        <h4>🧪 Test with adversarial inputs</h4>
        <p>What happens if the tool returns an error? If the user gives contradictory instructions? If the API is down? Test the unhappy paths — they're where agents break.</p>
      </div>
      <div class="block-card">
        <h4>📊 Observe everything</h4>
        <p>Use tracing tools (LangSmith, Langfuse) from day one. You cannot debug an agent you can't see. Every tool call, every LLM response, every decision — log it.</p>
      </div>
      <div class="block-card">
        <h4>💰 Budget your actions</h4>
        <p>Set hard limits on loop iterations, tool calls, and tokens per task. An agent without a budget can run up your API bill in minutes.</p>
      </div>
      <div class="block-card">
        <h4>🔄 Version your prompts</h4>
        <p>Treat prompts like code. Version them, review changes, A/B test them. A single-word change in a system prompt can completely alter agent behaviour.</p>
      </div>
    </div>
  </div>
</div>

</div><!-- /day4 -->

<!-- ═══════════════════════════════════════════════
     DAY 5 — Case Studies + Hands-on Labs
     ═══════════════════════════════════════════════ -->
<div id="day5" class="day-panel">

<div class="day-progress"><div class="day-progress-fill" style="width:0%" id="d5prog"></div></div>

<div class="sched-card" style="background:var(--eucalyptus); border-color: rgba(84,100,20,0.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 5 overview</div>
  <div class="sched-body">
    <h4>From theory to practice — case studies and hands-on</h4>
    <p>Case studies + 2 labs · ~3 hours · Apply everything you've learned this week</p>
  </div>
</div>

<!-- ── TOPIC 11 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">11</div>
    <h2>Real-World Success Stories</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">

    <div class="blocks-grid" style="grid-template-columns: 1fr;">
      <div class="block-card">
        <h4>🛫 Travel — Autonomous booking agents</h4>
        <p>Companies like Kayak and booking platforms now deploying agents that handle end-to-end trip planning: searching flights, comparing hotels, booking transfers, and sending itineraries — reducing customer service load by 40%+. The agent handles routine requests; humans handle complex complaints.</p>
      </div>
      <div class="block-card">
        <h4>🛒 E-commerce — Personalized shopping assistants</h4>
        <p>Klarna's AI assistant handles 2/3 of customer service chats (equivalent to 700 full-time agents), resolving queries in under 2 minutes vs. 11 minutes with human agents. It accesses order history, processes returns, and provides product recommendations.</p>
      </div>
      <div class="block-card">
        <h4>💻 Software Engineering — Code generation and review</h4>
        <p>GitHub Copilot Workspace takes a GitHub issue, generates a step-by-step plan, writes the code across multiple files, runs tests, and opens a PR. Developers review and approve rather than writing from scratch — an agent at autonomy Level 2–3.</p>
      </div>
      <div class="block-card">
        <h4>🔍 Research — Deep information synthesis</h4>
        <p>Perplexity AI runs an agent that searches the web in real-time, reads multiple sources, cross-references claims, and synthesises a cited answer — replacing the "open 10 tabs and read each one" workflow. Over 10 million queries per day.</p>
      </div>
    </div>

    <table class="cmp-table">
      <thead><tr><th>Domain</th><th>Agent Task</th><th>Tools Used</th></tr></thead>
      <tbody>
        <tr><td><strong>Software engineering</strong></td><td>Write, test, and debug code autonomously</td><td>Code executor, file system, GitHub API</td></tr>
        <tr><td><strong>Research & analysis</strong></td><td>Gather, synthesise, and cite sources</td><td>Web search, PDF reader, vector DB</td></tr>
        <tr><td><strong>Customer support</strong></td><td>Resolve tickets end-to-end</td><td>CRM API, knowledge base, email tool</td></tr>
        <tr><td><strong>Data analysis</strong></td><td>Clean, analyse, and visualise from a prompt</td><td>Python REPL, SQL, charting libraries</td></tr>
        <tr><td><strong>Finance</strong></td><td>Monitor markets, generate signals</td><td>Market data API, calculator, report writer</td></tr>
        <tr><td><strong>DevOps</strong></td><td>Investigate incidents, propose fixes</td><td>Log search, shell access, alerting API</td></tr>
      </tbody>
    </table>
  </div>
</div>

<hr class="section-divider">

<!-- ── HANDS-ON LAB 1 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background: var(--earth);">L1</div>
    <h2>Lab 1 — Analysing AI Agent Use Cases</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <div class="lab-box">
      <h4>🛠 Hands-on exercise</h4>
      <p style="margin-bottom: 12px;">Pick <strong>two</strong> use cases from the table above. For each one, write a structured analysis:</p>
      <ol>
        <li><strong>Goal:</strong> What is the agent trying to achieve? (one clear sentence)</li>
        <li><strong>Agent loop:</strong> Map the perceive → plan → act → learn steps for this use case</li>
        <li><strong>Tools needed:</strong> List every tool the agent would need access to</li>
        <li><strong>Autonomy level:</strong> What level (0–4) is appropriate? Why?</li>
        <li><strong>HITL points:</strong> Where should a human checkpoint be inserted?</li>
        <li><strong>Risks:</strong> What could go wrong? (hallucination, tool failure, runaway actions)</li>
        <li><strong>Blast radius:</strong> How would you limit damage if the agent makes a mistake?</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<!-- ── HANDS-ON LAB 2 ── -->
<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background: var(--earth);">L2</div>
    <h2>Lab 2 — Exploring the Agentic AI Framework Landscape</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <div class="lab-box">
      <h4>🛠 Hands-on exercise</h4>
      <p style="margin-bottom: 12px;">Get your hands dirty with real frameworks — no code yet, just exploration and comparison:</p>
      <ol>
        <li><strong>Visit the docs:</strong> Open the official docs for LangChain, CrewAI, and Phidata. Spend 10 minutes on each.</li>
        <li><strong>Identify the loop:</strong> For each framework, find where the perceive → plan → act → observe loop happens. What does the framework call it?</li>
        <li><strong>Compare:</strong> Create a table with columns: Framework, How agents are defined, How tools are attached, How memory works, Ease of getting started (your subjective rating)</li>
        <li><strong>Pick one:</strong> Which framework would you use to build the travel booking agent from Day 1? Write 3 sentences explaining why.</li>
        <li><strong>Ethics audit:</strong> Take your travel booking agent and map out: every tool it needs and what data that tool can access, 3 things that could go wrong, a safeguard for each risk.</li>
      </ol>
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
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agentic AI</strong> — AI that pursues goals autonomously via perceive → plan → act → learn</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agent vs Agentic</strong> — An agent is the unit; agentic AI is the system/paradigm</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Three AI eras</strong> — Traditional (rules) → Generative (content) → Agentic (action)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Building blocks</strong> — LLM + Tools + Memory + Planning + Orchestrator + Environment</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Autonomy spectrum</strong> — Level 0 (suggestions) to Level 4 (fully autonomous)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>HITL</strong> — Insert human checkpoints for irreversible, high-cost, or ambiguous actions</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Multi-agent</strong> — Start simple, add agents only at capability boundaries</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Ethics</strong> — Minimal footprint, reversible, auditable, fail-safe</span></div>
</div>

<h3 style="font-size: 17px; margin-top: 24px; margin-bottom: 12px;">Check Your Understanding</h3>
<p style="font-size: 14px; margin-bottom: 8px;">Before moving to Unit 2, make sure you can answer:</p>
<ol style="padding-left: 20px; font-size: 14px; line-height: 1.8;">
  <li>What are the four core traits of an agentic AI system?</li>
  <li>Explain the difference between an AI Agent and Agentic AI with an analogy.</li>
  <li>Describe a task that Traditional AI and Generative AI both fail at, but an Agentic AI can handle. Why?</li>
  <li>What is prompt injection in an agentic context and how do you defend against it?</li>
  <li>When should you use a multi-agent system vs. a single agent?</li>
  <li>Name three frameworks from the landscape and what each is best at.</li>
</ol>

<div style="text-align: center; margin-top: 36px;">
  <a href="/courses/agentic-ai-engineering/" style="display: inline-flex; align-items: center; gap: 6px; padding: 12px 28px; background: var(--gum); color: var(--white); border-radius: 8px; text-decoration: none; font-weight: 600; font-size: 15px; transition: background var(--transition);">
    ← Back to Course Overview
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

---

[← Back to Autonomous AI Engineering track](/courses/agentic-ai-engineering/)
