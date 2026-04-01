---
layout: default
title: "Autonomous AI Systems — Practical Engineering Track"
permalink: /courses/agentic-ai-engineering/
description: "A hands-on 12-week learning track for building autonomous AI agents — covering orchestration frameworks, retrieval-augmented pipelines, multi-agent coordination, and production deployment."
---

<style>
  /* Course page — harmonized with new LMS layout */
  .course-page {
    --c-text-primary:   var(--gray-900, #1A1917);
    --c-text-secondary: var(--gray-700, #4A4640);
    --c-text-tertiary:  var(--gray-500, #8C8578);
    --c-bg-primary:     var(--white, #FFFFFF);
    --c-bg-secondary:   var(--gray-100, #F5F3EF);
    --c-border:         var(--gray-200, #E8E4DD);
    --c-border-sec:     var(--gray-300, #D9D3C7);
    --r-lg: 12px;
    --r-md:  8px;
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

  <div class="course-hero-title">Autonomous AI Systems — Practical Engineering Track</div>
  <div class="course-hero-sub">Learn at your pace &nbsp;·&nbsp; 11 units &nbsp;·&nbsp; ~12 weeks &nbsp;·&nbsp; 8–10 hrs/week recommended</div>

  <div class="overview-grid">
    <div class="stat-card"><div class="stat-label">Learning units</div><div class="stat-val">11</div></div>
    <div class="stat-card"><div class="stat-label">Practice projects</div><div class="stat-val">20+</div></div>
    <div class="stat-card"><div class="stat-label">Timeline</div><div class="stat-val">12 wks</div></div>
  </div>

  <!-- TRACK A -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p1')">
      <span class="phase-badge" style="background:#EEEDFE;color:#3C3489;border:0.5px solid #CECBF6;">Track A</span>
      <span class="phase-title">Groundwork &amp; Principles</span>
      <span class="phase-meta">Weeks 1–3</span>
      <span class="chevron" id="p1-chev">▶</span>
    </div>
    <div class="phase-body" id="p1">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#7F77DD;"></div></div>

      <div class="week-label">Week 1</div>
      <div class="mod-row">
        <div class="mod-num">U1</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/03/21/m1-agentic-ai-essentials/" style="color:inherit;text-decoration:none;">Introduction to Autonomous AI ↗</a></div>
          <div class="mod-duration">~8 hrs · 2 exercises</div>
          <div class="mod-tags">
            <span class="tag concept">Core ideas</span>
            <span class="tag concept">Responsible AI</span>
            <span class="tag lab">Evaluate real-world scenarios</span>
          </div>
        </div>
      </div>

      <div class="week-label">Weeks 2–3</div>
      <div class="mod-row">
        <div class="mod-num">U2</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/03/28/u2-agentic-ai-architecture-design-patterns/" style="color:inherit;text-decoration:none;">Agent Blueprints &amp; Reasoning Strategies ↗</a></div>
          <div class="mod-duration">~10 hrs · 2 exercises</div>
          <div class="mod-tags">
            <span class="tag concept">ReAct / ReWOO loops</span>
            <span class="tag concept">Cooperative agents</span>
            <span class="tag lab">Draft a system blueprint</span>
          </div>
        </div>
      </div>

      <div class="tip-box">Keep a personal journal. Draw each reasoning loop (Reflection, Tool Invocation, Planning, Action-Observation) on paper — active recall beats passive reading every time.</div>
    </div>

  </div>

  <!-- TRACK B -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p2')">
      <span class="phase-badge" style="background:#E6F1FB;color:#0C447C;border:0.5px solid #B5D4F4;">Track B</span>
      <span class="phase-title">Orchestration Toolkits</span>
      <span class="phase-meta">Weeks 4–7</span>
      <span class="chevron" id="p2-chev">▶</span>
    </div>
    <div class="phase-body" id="p2">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#378ADD;"></div></div>

      <div class="week-label">Week 4</div>
      <div class="mod-row">
        <div class="mod-num">U3</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/04/11/u3-chain-composition-langchain/" style="color:inherit;text-decoration:none;">Chain Composition with LangChain ↗</a></div>
          <div class="mod-duration">~9 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">LangChain</span>
            <span class="tag tool">LCEL</span>
            <span class="tag lab">Create an auto-debugging code helper</span>
          </div>
        </div>
      </div>

      <div class="week-label">Weeks 5–6</div>
      <div class="mod-row">
        <div class="mod-num">U4</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/04/18/u4-stateful-agent-workflows-langgraph/" style="color:inherit;text-decoration:none;">Stateful Agent Workflows with LangGraph ↗</a></div>
          <div class="mod-duration">~12 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">LangGraph</span>
            <span class="tag concept">State management</span>
            <span class="tag lab">Personal budget advisor</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 7</div>
      <div class="mod-row">
        <div class="mod-num">U5</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/04/25/u5-retrieval-augmented-agent-pipelines/" style="color:inherit;text-decoration:none;">Retrieval-Augmented Agent Pipelines ↗</a></div>
          <div class="mod-duration">~10 hrs · 2 projects</div>
          <div class="mod-tags">
            <span class="tag tool">LlamaIndex</span>
            <span class="tag tool">Cohere</span>
            <span class="tag lab">Quarterly earnings summarizer</span>
            <span class="tag lab">Competitive intelligence bot</span>
          </div>
        </div>
      </div>

      <div class="tip-box">This track is the most intensive. Take your time with U4 — understanding how LangGraph manages state and memory is critical for everything ahead. Put extra effort into the budget advisor project.</div>
    </div>

  </div>

  <!-- TRACK C -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p3')">
      <span class="phase-badge" style="background:#E1F5EE;color:#085041;border:0.5px solid #9FE1CB;">Track C</span>
      <span class="phase-title">Collaborative &amp; Specialized Agents</span>
      <span class="phase-meta">Weeks 8–10</span>
      <span class="chevron" id="p3-chev">▶</span>
    </div>
    <div class="phase-body" id="p3">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#1D9E75;"></div></div>

      <div class="week-label">Week 8</div>
      <div class="mod-row">
        <div class="mod-num">U6</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/02/u6-rapid-agent-prototyping-phidata/" style="color:inherit;text-decoration:none;">Rapid Agent Prototyping with Phidata ↗</a></div>
          <div class="mod-duration">~8 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">Phidata</span>
            <span class="tag tool">Vector DB</span>
            <span class="tag lab">Automated insights dashboard</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 9</div>
      <div class="mod-row">
        <div class="mod-num">U7</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/09/u7-coordinated-agent-teams-crewai/" style="color:inherit;text-decoration:none;">Coordinated Agent Teams with CrewAI ↗</a></div>
          <div class="mod-duration">~10 hrs · 2 projects</div>
          <div class="mod-tags">
            <span class="tag tool">CrewAI</span>
            <span class="tag concept">Agent collaboration</span>
            <span class="tag lab">Help-desk automation</span>
            <span class="tag lab">Equity screening assistant</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 10</div>
      <div class="mod-row">
        <div class="mod-num">U8</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/16/u8-conversational-agent-networks-autogen/" style="color:inherit;text-decoration:none;">Conversational Agent Networks with Autogen ↗</a></div>
          <div class="mod-duration">~9 hrs · 1 project</div>
          <div class="mod-tags">
            <span class="tag tool">Autogen</span>
            <span class="tag concept">Dialogue patterns</span>
            <span class="tag lab">Literature review assistant</span>
          </div>
        </div>
      </div>

      <div class="tip-box">After completing this track, write a side-by-side comparison of CrewAI, LangGraph multi-agent, and Autogen. Each takes a fundamentally different approach — documenting the trade-offs is the most valuable exercise here.</div>
    </div>

  </div>

  <!-- TRACK D -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p4')">
      <span class="phase-badge" style="background:#FAEEDA;color:#633806;border:0.5px solid #FAC775;">Track D</span>
      <span class="phase-title">Production, Monitoring &amp; Deployment</span>
      <span class="phase-meta">Weeks 11–12</span>
      <span class="chevron" id="p4-chev">▶</span>
    </div>
    <div class="phase-body" id="p4">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#BA7517;"></div></div>

      <div class="week-label">Week 11</div>
      <div class="mod-row">
        <div class="mod-num">U9</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/" style="color:inherit;text-decoration:none;">Tracing, Evaluation &amp; Agent Telemetry ↗</a></div>
          <div class="mod-duration">~8 hrs · 2 labs</div>
          <div class="mod-tags">
            <span class="tag tool">Langfuse</span>
            <span class="tag tool">Langsmith</span>
            <span class="tag lab">End-to-end tracing setup</span>
          </div>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">U10</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/23/u10-visual-low-code-agent-builders/" style="color:inherit;text-decoration:none;">Visual &amp; Low-Code Agent Builders ↗</a></div>
          <div class="mod-duration">~8 hrs · 3 labs</div>
          <div class="mod-tags">
            <span class="tag tool">Wordware</span>
            <span class="tag tool">Relevance AI</span>
            <span class="tag tool">Langflow</span>
            <span class="tag lab">Content pipeline &amp; SEO assistant</span>
          </div>
        </div>
      </div>

      <div class="week-label">Week 12</div>
      <div class="mod-row">
        <div class="mod-num">★</div>
        <div class="mod-content">
          <div class="mod-title"><a href="/blog/2026/05/30/u11-capstone-deploying-autonomous-ai-cloud/" style="color:inherit;text-decoration:none;">Capstone: Deploying Autonomous AI on Major Clouds ↗</a></div>
          <div class="mod-duration">~10 hrs · 1 capstone project (flexible pace)</div>
          <div class="mod-tags">
            <span class="tag tool">AWS Bedrock</span>
            <span class="tag tool">Azure OpenAI</span>
            <span class="tag tool">GCP Vertex AI</span>
            <span class="tag lab">Multi-cloud deployment exercise</span>
          </div>
        </div>
      </div>

      <div class="tip-box">The final week is kept lighter on purpose — use it to build your capstone that ties several units together: for instance, a coordinated agent pipeline with retrieval, tracing, and cloud deployment.</div>
    </div>

  </div>

  <div class="study-footer">
    <strong>How to get the most from this track</strong><br>
    Progress through each track in order. After each unit, revisit your notes, commit your project code, and jot a brief reflection. Begin planning your capstone during Week 10 — it will serve as the centerpiece of your portfolio.
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
