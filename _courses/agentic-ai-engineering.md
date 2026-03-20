---
layout: default
title: "Agentic AI Engineering — Self-Paced Course"
permalink: /courses/agentic-ai-engineering/
description: "A comprehensive 12-week self-paced plan covering Agentic AI from foundations to cloud deployment — LangChain, LangGraph, CrewAI, Autogen, RAG, and more."
---

<style>
  /* CSS variable fallbacks for the architect theme */
  .course-page {
    --c-text-primary:   #1a1a1a;
    --c-text-secondary: #555;
    --c-text-tertiary:  #888;
    --c-bg-primary:     #ffffff;
    --c-bg-secondary:   #f6f6f6;
    --c-border:         #e2e2e2;
    --c-border-sec:     #ccc;
    --r-lg: 10px;
    --r-md:  6px;
  }
  @media (prefers-color-scheme: dark) {
    .course-page {
      --c-text-primary:   #e8e8e8;
      --c-text-secondary: #aaa;
      --c-text-tertiary:  #666;
      --c-bg-primary:     #1e1e1e;
      --c-bg-secondary:   rgb(48, 23, 116);
      --c-border:         #363636;
      --c-border-sec:     #444;
    }
  }

  .course-page { padding: 4px 0 24px; max-width: 740px; }

  .course-hero-title { font-size: 22px; font-weight: 600; color: var(--c-text-primary); margin-bottom: 4px; }
  .course-hero-sub   { font-size: 14px; color: var(--c-text-secondary); margin-bottom: 16px; }

  .overview-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-bottom: 16px; }
  .stat-card { background: var(--c-bg-secondary); border-radius: var(--r-md); padding: 10px 14px; border: 0.5px solid var(--c-border); }
  .stat-label { font-size: 11px; color: var(--c-text-secondary); }
  .stat-val   { font-size: 20px; font-weight: 600; color: var(--c-text-primary); margin-top: 2px; }

  .phase { border-radius: var(--r-lg); border: 0.5px solid var(--c-border); background: var(--c-bg-primary); margin-bottom: 10px; overflow: hidden; }
  .phase-header { display: flex; align-items: center; gap: 10px; padding: 12px 16px; cursor: pointer; user-select: none; }
  .phase-header:hover { background: var(--c-bg-secondary); }
  .phase-badge { font-size: 11px; font-weight: 500; padding: 3px 8px; border-radius: 20px; white-space: nowrap; }
  .phase-title { font-size: 15px; font-weight: 500; color: var(--c-text-primary); flex: 1; }
  .phase-meta  { font-size: 12px; color: var(--c-text-secondary); white-space: nowrap; }
  .chevron     { font-size: 11px; color: var(--c-text-tertiary); transition: transform 0.2s; }
  .phase-body  { display: none; padding: 0 16px 14px; border-top: 0.5px solid var(--c-border); }
  .phase-body.open { display: block; }

  .mod-row { display: flex; align-items: flex-start; gap: 10px; padding: 8px 0; border-bottom: 0.5px solid var(--c-border); }
  .mod-row:last-child { border-bottom: none; }
  .mod-num     { font-size: 11px; font-weight: 600; min-width: 24px; color: var(--c-text-tertiary); padding-top: 3px; }
  .mod-content { flex: 1; }
  .mod-title   { font-size: 13px; font-weight: 500; color: var(--c-text-primary); }
  .mod-duration{ font-size: 11px; color: var(--c-text-secondary); margin-top: 1px; }
  .mod-tags    { display: flex; flex-wrap: wrap; gap: 4px; margin-top: 5px; }

  .tag         { font-size: 10px; padding: 2px 7px; border-radius: 20px; background: var(--c-bg-secondary); color: var(--c-text-secondary); border: 0.5px solid var(--c-border); }
  .tag.tool    { background: #E6F1FB; color: #0C447C; border-color: #B5D4F4; }
  .tag.lab     { background: #EAF3DE; color: #27500A; border-color: #C0DD97; }
  .tag.concept { background: #EEEDFE; color: #3C3489; border-color: #CECBF6; }
  @media (prefers-color-scheme: dark) {
    .tag.tool    { background: #0C447C; color: #B5D4F4; border-color: #185FA5; }
    .tag.lab     { background: #27500A; color: #C0DD97; border-color: #3B6D11; }
    .tag.concept { background: #3C3489; color: #CECBF6; border-color: #534AB7; }
  }

  .progress-bar  { height: 4px; border-radius: 2px; background: var(--c-border); margin: 6px 0 10px; }
  .progress-fill { height: 4px; border-radius: 2px; }
  .week-label    { font-size: 11px; font-weight: 600; color: var(--c-text-secondary); margin: 10px 0 4px; text-transform: uppercase; letter-spacing: 0.06em; }

  .tip-box { background: var(--c-bg-secondary); border-left: 3px solid #7F77DD; border-radius: 0 var(--r-md) var(--r-md) 0; padding: 8px 12px; margin-top: 10px; font-size: 12px; color: var(--c-text-secondary); line-height: 1.55; }

  .study-footer { margin-top: 16px; padding: 10px 14px; background: var(--c-bg-secondary); border-radius: var(--r-md); border: 0.5px solid var(--c-border); font-size: 12px; color: var(--c-text-secondary); line-height: 1.6; }
  .study-footer strong { color: var(--c-text-primary); font-weight: 600; }
  .back-link { display: inline-block; font-size: 13px; margin-bottom: 14px; color: var(--c-text-secondary); text-decoration: none; }
  .back-link:hover { color: var(--c-text-primary); }
</style>

<div class="course-page">
  <a class="back-link" href="/courses/">&larr; All Courses</a>

  <div class="course-hero-title">Agentic AI Engineering</div>
  <div class="course-hero-sub">Self-paced plan &nbsp;·&nbsp; 11 modules &nbsp;·&nbsp; ~12 weeks &nbsp;·&nbsp; study 8–10 hrs/week</div>

  <div class="overview-grid">
    <div class="stat-card"><div class="stat-label">Total modules</div><div class="stat-val">11</div></div>
    <div class="stat-card"><div class="stat-label">Hands-on labs</div><div class="stat-val">20+</div></div>
    <div class="stat-card"><div class="stat-label">Est. duration</div><div class="stat-val">12 wks</div></div>
  </div>

  <!-- PHASE 1 -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p1')">
      <span class="phase-badge" style="background:#EEEDFE;color:#3C3489;border:0.5px solid #CECBF6;">Phase 1</span>
      <span class="phase-title">Foundations</span>
      <span class="phase-meta">Weeks 1–3</span>
      <span class="chevron" id="p1-chev">▶</span>
    </div>
    <div class="phase-body" id="p1">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#7F77DD;"></div></div>

      <div class="week-label">Week 1</div>
      <div class="mod-row">
        <div class="mod-num">M1</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/03/21/m1-agentic-ai-essentials/" style="color:inherit;text-decoration:none;">Agentic AI Essentials ↗</a></div>
          <div class="mod-duration">~8 hrs · 2 labs</div>
          <div class="mod-tags">
            <span class="tag concept">Concepts</span>
            <span class="tag concept">Ethics</span>
            <span class="tag lab">Analyze use cases</span>
          </div>
        </div>
      </div>

      <div class="week-label">Weeks 2–3</div>
      <div class="mod-row">
        <div class="mod-num">M2</div>
        <div class="mod-content">
          <div class="mod-title">Architectures &amp; Design Patterns</div>
          <div class="mod-duration">~10 hrs · 2 labs</div>
          <div class="mod-tags">
            <span class="tag concept">ReAct / ReWOO</span>
            <span class="tag concept">Multi-agent</span>
            <span class="tag lab">Design an architecture</span>
          </div>
        </div>
      </div>

      <div class="tip-box">Start a notes doc. Sketch each design pattern (Reflection, Tool Use, Planning, ReAct) by hand — it cements them far better than just reading.</div>
    </div>

  </div>

  <!-- PHASE 2 -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p2')">
      <span class="phase-badge" style="background:#E6F1FB;color:#0C447C;border:0.5px solid #B5D4F4;">Phase 2</span>
      <span class="phase-title">Core Frameworks</span>
      <span class="phase-meta">Weeks 4–7</span>
      <span class="chevron" id="p2-chev">▶</span>
    </div>
    <div class="phase-body" id="p2">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#378ADD;"></div></div>

      <div class="week-label">Week 4</div>
      <div class="mod-row">
        <div class="mod-num">M3</div>
        <div class="mod-content">
          <div class="mod-title">LangChain &amp; LCEL</div>
          <div class="mod-duration">~9 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">LangChain</span>
            <span class="tag tool">LCEL</span>
            <span class="tag lab">Build self-correcting coding assistant</span>
          </div>
        </div>
      </div>

      <div class="week-label">Weeks 5–6</div>
      <div class="mod-row">
        <div class="mod-num">M4</div>
        <div class="mod-content">
          <div class="mod-title">Building AI Agents with LangGraph</div>
          <div class="mod-duration">~12 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">LangGraph</span>
            <span class="tag concept">State &amp; Memory</span>
            <span class="tag lab">Finance bot</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 7</div>
      <div class="mod-row">
        <div class="mod-num">M5</div>
        <div class="mod-content">
          <div class="mod-title">Implementing Agentic RAG</div>
          <div class="mod-duration">~10 hrs · 2 projects</div>
          <div class="mod-tags">
            <span class="tag tool">LlamaIndex</span>
            <span class="tag tool">Cohere</span>
            <span class="tag lab">Sales report analyzer</span>
            <span class="tag lab">Market research agent</span>
          </div>
        </div>
      </div>

      <div class="tip-box">This is the densest phase. Don't rush M4 — LangGraph's state/memory model is the backbone of everything that follows. Spend extra time on the Finance Bot project.</div>
    </div>

  </div>

  <!-- PHASE 3 -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p3')">
      <span class="phase-badge" style="background:#E1F5EE;color:#085041;border:0.5px solid #9FE1CB;">Phase 3</span>
      <span class="phase-title">Advanced Agents</span>
      <span class="phase-meta">Weeks 8–10</span>
      <span class="chevron" id="p3-chev">▶</span>
    </div>
    <div class="phase-body" id="p3">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#1D9E75;"></div></div>

      <div class="week-label">Week 8</div>
      <div class="mod-row">
        <div class="mod-num">M6</div>
        <div class="mod-content">
          <div class="mod-title">AI Agents with Phidata</div>
          <div class="mod-duration">~8 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">Phidata</span>
            <span class="tag tool">Vector DB</span>
            <span class="tag lab">Data analysis agent</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 9</div>
      <div class="mod-row">
        <div class="mod-num">M7</div>
        <div class="mod-content">
          <div class="mod-title">Multi-Agent Systems — LangGraph + CrewAI</div>
          <div class="mod-duration">~10 hrs · 2 projects</div>
          <div class="mod-tags">
            <span class="tag tool">CrewAI</span>
            <span class="tag concept">Multi-agent design</span>
            <span class="tag lab">Customer support chatbot</span>
            <span class="tag lab">Stock analysis agent</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 10</div>
      <div class="mod-row">
        <div class="mod-num">M8</div>
        <div class="mod-content">
          <div class="mod-title">Advanced Agent Dev with Autogen</div>
          <div class="mod-duration">~9 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">Autogen</span>
            <span class="tag concept">Conversation patterns</span>
            <span class="tag lab">AI research agent</span>
          </div>
        </div>
      </div>

      <div class="tip-box">Compare CrewAI vs LangGraph multi-agent vs Autogen side-by-side. Each has a different philosophy — a written comparison will be your best study artifact.</div>
    </div>

  </div>

  <!-- PHASE 4 -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p4')">
      <span class="phase-badge" style="background:#FAEEDA;color:#633806;border:0.5px solid #FAC775;">Phase 4</span>
      <span class="phase-title">Ops, No-Code &amp; Cloud</span>
      <span class="phase-meta">Weeks 11–12</span>
      <span class="chevron" id="p4-chev">▶</span>
    </div>
    <div class="phase-body" id="p4">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#BA7517;"></div></div>

      <div class="week-label">Week 11</div>
      <div class="mod-row">
        <div class="mod-num">M9</div>
        <div class="mod-content">
          <div class="mod-title">AI Agent Observability &amp; AgentOps</div>
          <div class="mod-duration">~8 hrs · 2 labs</div>
          <div class="mod-tags">
            <span class="tag tool">Langfuse</span>
            <span class="tag tool">Langsmith</span>
            <span class="tag lab">Observability implementation</span>
          </div>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">M10</div>
        <div class="mod-content">
          <div class="mod-title">Building Agents with No/Low-Code Tools</div>
          <div class="mod-duration">~8 hrs · 3 labs</div>
          <div class="mod-tags">
            <span class="tag tool">Wordware</span>
            <span class="tag tool">Relevance AI</span>
            <span class="tag tool">Langflow</span>
            <span class="tag lab">SEO agent, content writer</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 12</div>
      <div class="mod-row">
        <div class="mod-num">B</div>
        <div class="mod-content">
          <div class="mod-title">Bonus: Generative &amp; Agentic AI on Cloud</div>
          <div class="mod-duration">~10 hrs · 1 capstone lab (self-paced)</div>
          <div class="mod-tags">
            <span class="tag tool">AWS Bedrock</span>
            <span class="tag tool">Azure OpenAI</span>
            <span class="tag tool">GCP Vertex AI</span>
            <span class="tag lab">Deploy across all 3 clouds</span>
          </div>
        </div>
      </div>

      <div class="tip-box">Week 12 is intentionally lighter to give you time to build a capstone project that strings together multiple modules — e.g., a multi-agent RAG system with observability deployed to cloud.</div>
    </div>

  </div>

  <div class="study-footer">
    <strong>Suggested study rhythm</strong><br>
    Work through each phase sequentially. After finishing a module, review your notes, push your lab code to GitHub, and write a short reflection before moving on. The capstone in Week 12 is your portfolio piece — start scoping it during Week 10.
  </div>
</div>

<script>
function toggle(id) {
  var body = document.getElementById(id);
  var chev = document.getElementById(id + '-chev');
  var open = body.classList.toggle('open');
  chev.textContent = open ? '▼' : '▶';
}
toggle('p1');
</script>
