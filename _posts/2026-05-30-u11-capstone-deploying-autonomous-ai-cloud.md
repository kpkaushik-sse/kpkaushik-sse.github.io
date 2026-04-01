---
layout: default
title: "Unit 11 ★ Capstone — Deploying Autonomous AI on Major Clouds"
date: 2026-05-30
categories: [agentic-ai, production]
permalink: /blog/2026/05/30/u11-capstone-deploying-autonomous-ai-cloud/
description: "Capstone project — deploy production AI agents on AWS Bedrock, Azure OpenAI, and GCP Vertex AI. Compare managed AI services, build a portable agent, and graduate the course."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 11 ★ Capstone</span>
</nav>

<div class="mod-hero">
  <h1>Unit 11 ★ Capstone — Deploying Autonomous AI on Major Clouds</h1>
  <p class="mod-hero-sub">This is the finish line. You've built agents with LangChain, LangGraph, Phidata, CrewAI, and AutoGen. You've traced, evaluated, and prototyped with visual tools. Now you'll take an agent from your laptop to the three major cloud platforms — <strong>AWS Bedrock</strong>, <strong>Azure OpenAI</strong>, and <strong>GCP Vertex AI</strong> — and learn when to use each.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track D · Production & Deployment</span>
    <span class="mod-pill time">⏱ ~10 hrs across 5 days (Week 12)</span>
    <span class="mod-pill hands">🛠 1 capstone project with 3 deployments</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisites:</strong> Complete all previous units, especially <a href="/blog/2026/05/23/u9-tracing-evaluation-agent-telemetry/" style="color:var(--gum);">Unit 9 — Telemetry</a> and <a href="/blog/2026/05/23/u10-visual-low-code-agent-builders/" style="color:var(--gum);">Unit 10 — Low-Code Builders</a>. You'll need free tier accounts on AWS, Azure, and GCP (each offers free credits for new accounts).
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Compare AWS Bedrock, Azure OpenAI, and GCP Vertex AI: models, pricing, features</li>
    <li>Deploy a LangChain agent using AWS Bedrock models (Claude, Llama, Titan)</li>
    <li>Deploy the same agent using Azure OpenAI (GPT-4o, GPT-4o-mini)</li>
    <li>Deploy the same agent using GCP Vertex AI (Gemini, PaLM)</li>
    <li>Build a portable agent that can switch between cloud providers via configuration</li>
    <li>Containerise an agent with Docker and deploy to a cloud compute service</li>
    <li>Set up production infrastructure: API gateway, secrets management, auto-scaling</li>
    <li>Create a cost comparison across all three providers for the same workload</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">AWS Bedrock</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Azure OpenAI</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">GCP Vertex AI</span>
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
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 1</div><div class="sched-body"><h4>Cloud AI landscape & AWS Bedrock</h4><p>Two topics · ~2 hours · Cover: Cloud comparison + Bedrock deployment</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">1</div><h2>The Cloud AI Services Landscape</h2><span class="topic-time">45 min</span></div>
<div class="topic-body">
<p>All three major clouds offer managed AI services that let you call foundation models via API. The key differences are model selection, pricing, compliance certifications, and ecosystem integration.</p>

<table class="cmp-table">
  <thead><tr><th>Feature</th><th>AWS Bedrock</th><th>Azure OpenAI</th><th>GCP Vertex AI</th></tr></thead>
  <tbody>
    <tr><td><strong>Models</strong></td><td>Claude (Anthropic), Llama (Meta), Titan (Amazon), Mistral, Cohere</td><td>GPT-4o, GPT-4o-mini, GPT-4 Turbo, DALL-E, Whisper</td><td>Gemini (Google), PaLM 2, Claude (via Model Garden)</td></tr>
    <tr><td><strong>Multi-model</strong></td><td>Yes — access 20+ models from one API</td><td>OpenAI models only (but best-in-class)</td><td>Yes — Google models + Model Garden</td></tr>
    <tr><td><strong>Knowledge bases</strong></td><td>Built-in RAG with S3 + vector DB</td><td>Azure AI Search (formerly Cognitive Search)</td><td>Vertex AI Search + vector embeddings</td></tr>
    <tr><td><strong>Agent framework</strong></td><td>Bedrock Agents (no code)</td><td>Azure AI Agent Service</td><td>Vertex AI Agent Builder</td></tr>
    <tr><td><strong>Fine-tuning</strong></td><td>Yes (Titan, Llama)</td><td>Yes (GPT-4o-mini, GPT-3.5)</td><td>Yes (Gemini, PaLM 2)</td></tr>
    <tr><td><strong>Data residency</strong></td><td>Multi-region, GovCloud</td><td>Multi-region, sovereign clouds</td><td>Multi-region, EU options</td></tr>
    <tr><td><strong>Best for</strong></td><td>Multi-model strategy, AWS-heavy orgs</td><td>GPT-focused apps, Microsoft ecosystem</td><td>Google ecosystem, Gemini users</td></tr>
  </tbody>
</table>

<div class="insight-box"><strong>The portability principle:</strong> Don't lock your agent to one cloud provider's SDK. Use LangChain's model abstraction — swap <code>ChatOpenAI</code> for <code>ChatBedrock</code> or <code>ChatVertexAI</code> with a config change. Your chains, tools, and logic stay the same.</div>
</div></div>

<hr class="section-divider">

<div class="topic-section"><div class="topic-header"><div class="topic-num">2</div><h2>AWS Bedrock — Multi-Model Agent Deployment</h2><span class="topic-time">60 min</span></div>
<div class="topic-body">

<div class="arch-diagram">
  <div class="title">LANGCHAIN + AWS BEDROCK</div>
  <div><span class="purple">from</span> langchain_aws <span class="purple">import</span> ChatBedrock</div>
  <div></div>
  <div>llm = ChatBedrock(</div>
  <div>    model_id=<span class="green">"anthropic.claude-3-5-sonnet-20241022-v2:0"</span>,</div>
  <div>    region_name=<span class="green">"us-east-1"</span>,</div>
  <div>    model_kwargs={<span class="green">"temperature"</span>: <span class="yellow">0</span>, <span class="green">"max_tokens"</span>: <span class="yellow">4096</span>},</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># Use it like any LangChain LLM — chains, agents, tools all work</span></div>
  <div>response = llm.invoke(<span class="green">"Summarise the key features of AWS Bedrock."</span>)</div>
</div>

<div class="lab-box"><h4>✏️ Lab — Deploy on Bedrock (45 min)</h4><ol>
  <li>Set up AWS credentials (<code>aws configure</code>) and enable Claude in Bedrock console.</li>
  <li>Install: <code>pip install langchain-aws boto3</code></li>
  <li>Swap your U3 LangChain agent's model from ChatOpenAI to ChatBedrock.</li>
  <li>Run 5 queries. Compare response quality and latency vs. OpenAI directly.</li>
  <li>Try a different model: switch to <code>meta.llama3-70b-instruct-v1:0</code>. How does quality change?</li>
</ol></div>
</div></div>
</div><!-- /day1 -->

<!-- DAY 2 -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 2</div><div class="sched-body"><h4>Azure OpenAI — enterprise-grade GPT deployment</h4><p>One topic · ~2 hours · Cover: Azure OpenAI setup + deployment</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">3</div><h2>Azure OpenAI — GPT in the Enterprise Cloud</h2><span class="topic-time">90 min</span></div>
<div class="topic-body">
<p>Azure OpenAI gives you the same GPT models as OpenAI's API, but running within Azure's infrastructure. This means Azure Active Directory authentication, virtual network integration, content filtering, and compliance certifications (SOC 2, HIPAA, etc.).</p>

<div class="arch-diagram">
  <div class="title">LANGCHAIN + AZURE OPENAI</div>
  <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> AzureChatOpenAI</div>
  <div></div>
  <div>llm = AzureChatOpenAI(</div>
  <div>    azure_deployment=<span class="green">"gpt-4o-mini"</span>,</div>
  <div>    api_version=<span class="green">"2024-08-01-preview"</span>,</div>
  <div>    azure_endpoint=<span class="green">"https://your-resource.openai.azure.com/"</span>,</div>
  <div>    api_key=<span class="green">"your-azure-key"</span>,</div>
  <div>    temperature=<span class="yellow">0</span>,</div>
  <div>)</div>
  <div></div>
  <div><span class="dim"># Same LangChain interface — all your chains work unchanged</span></div>
  <div>response = llm.invoke(<span class="green">"Explain Azure OpenAI content filtering."</span>)</div>
</div>

<div class="blocks-grid">
  <div class="block-card"><h4>🔐 Enterprise security</h4><p>Azure AD auth, managed identity, private endpoints, VNet integration. Your data never leaves your Azure tenant.</p></div>
  <div class="block-card"><h4>🛡️ Content filtering</h4><p>Built-in safety system: hate, violence, self-harm, sexual content detection. Configurable severity thresholds.</p></div>
  <div class="block-card"><h4>📊 Provisioned throughput</h4><p>Reserve capacity for predictable performance. No rate limits, no noisy neighbours. Pay per provisioned unit.</p></div>
  <div class="block-card"><h4>🌍 Regional deployment</h4><p>Deploy models in specific Azure regions for data residency compliance. EU, US, Asia availability.</p></div>
</div>

<div class="lab-box"><h4>✏️ Lab — Deploy on Azure OpenAI (60 min)</h4><ol>
  <li>Create an Azure OpenAI resource in the Azure portal. Deploy a gpt-4o-mini model.</li>
  <li>Install: <code>pip install langchain-openai</code></li>
  <li>Swap your agent's model to AzureChatOpenAI. Run the same 5 queries as Day 1.</li>
  <li>Compare: response quality, latency, token pricing between Bedrock Claude and Azure GPT-4o-mini.</li>
  <li>Test content filtering: send a borderline query and observe Azure's safety response.</li>
</ol></div>
</div></div>
</div><!-- /day2 -->

<!-- DAY 3 -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 3</div><div class="sched-body"><h4>GCP Vertex AI — Gemini and the Google ecosystem</h4><p>One topic · ~2 hours · Cover: Vertex AI setup + Gemini deployment</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">4</div><h2>GCP Vertex AI — Gemini in Production</h2><span class="topic-time">90 min</span></div>
<div class="topic-body">
<p>Google's Vertex AI platform hosts Gemini models alongside a Model Garden with 100+ open-source and partner models. The standout feature: Gemini's massive context window (up to 2M tokens) and native multimodal support (text, images, video, audio).</p>

<div class="arch-diagram">
  <div class="title">LANGCHAIN + VERTEX AI</div>
  <div><span class="purple">from</span> langchain_google_vertexai <span class="purple">import</span> ChatVertexAI</div>
  <div></div>
  <div>llm = ChatVertexAI(</div>
  <div>    model=<span class="green">"gemini-1.5-pro"</span>,</div>
  <div>    project=<span class="green">"your-gcp-project-id"</span>,</div>
  <div>    location=<span class="green">"us-central1"</span>,</div>
  <div>    temperature=<span class="yellow">0</span>,</div>
  <div>)</div>
  <div></div>
  <div>response = llm.invoke(<span class="green">"Explain the advantages of Gemini's 2M token context window."</span>)</div>
</div>

<div class="blocks-grid">
  <div class="block-card"><h4>📐 Massive context</h4><p>Gemini 1.5 Pro supports up to 2M tokens. Process entire codebases, long documents, or hours of video in a single call.</p></div>
  <div class="block-card"><h4>🎥 Multimodal native</h4><p>Send text, images, video, and audio in the same request. No separate vision API needed.</p></div>
  <div class="block-card"><h4>🏪 Model Garden</h4><p>100+ models: Gemini, Claude, Llama, Mistral. One-click deployment to Vertex AI endpoints.</p></div>
  <div class="block-card"><h4>🔍 Grounding</h4><p>Built-in Google Search grounding: the model can search the web during generation for up-to-date answers.</p></div>
</div>

<div class="lab-box"><h4>✏️ Lab — Deploy on Vertex AI (60 min)</h4><ol>
  <li>Set up GCP authentication: <code>gcloud auth application-default login</code></li>
  <li>Install: <code>pip install langchain-google-vertexai</code></li>
  <li>Swap your agent's model to ChatVertexAI with Gemini 1.5 Pro. Run the same 5 queries.</li>
  <li>Test the long-context advantage: send a 10,000-word document and ask a question about it.</li>
  <li>Compare: response quality, latency, pricing across all three clouds for the same workload.</li>
</ol></div>
</div></div>
</div><!-- /day3 -->

<!-- DAY 4 -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 4</div><div class="sched-body"><h4>Portable agent — one codebase, three clouds</h4><p>One topic · ~2 hours · Cover: Build a cloud-portable agent with config-based model switching</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num">5</div><h2>Building a Cloud-Portable Agent</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">
<p>The capstone challenge: build a single agent codebase that can run on any of the three clouds by changing a configuration variable. The agent logic, tools, chains, and memory stay identical — only the LLM provider changes.</p>

<div class="arch-diagram">
  <div class="title">PORTABLE MODEL FACTORY</div>
  <div><span class="purple">import</span> os</div>
  <div></div>
  <div><span class="blue">def</span> <span class="yellow">get_llm</span>(provider: str = <span class="yellow">None</span>):</div>
  <div>    provider = provider <span class="purple">or</span> os.getenv(<span class="green">"LLM_PROVIDER"</span>, <span class="green">"openai"</span>)</div>
  <div></div>
  <div>    <span class="purple">if</span> provider == <span class="green">"openai"</span>:</div>
  <div>        <span class="purple">from</span> langchain_openai <span class="purple">import</span> ChatOpenAI</div>
  <div>        <span class="purple">return</span> ChatOpenAI(model=<span class="green">"gpt-4o-mini"</span>)</div>
  <div></div>
  <div>    <span class="purple">elif</span> provider == <span class="green">"bedrock"</span>:</div>
  <div>        <span class="purple">from</span> langchain_aws <span class="purple">import</span> ChatBedrock</div>
  <div>        <span class="purple">return</span> ChatBedrock(model_id=<span class="green">"anthropic.claude-3-5-sonnet..."</span>)</div>
  <div></div>
  <div>    <span class="purple">elif</span> provider == <span class="green">"azure"</span>:</div>
  <div>        <span class="purple">from</span> langchain_openai <span class="purple">import</span> AzureChatOpenAI</div>
  <div>        <span class="purple">return</span> AzureChatOpenAI(azure_deployment=<span class="green">"gpt-4o-mini"</span>, ...)</div>
  <div></div>
  <div>    <span class="purple">elif</span> provider == <span class="green">"vertex"</span>:</div>
  <div>        <span class="purple">from</span> langchain_google_vertexai <span class="purple">import</span> ChatVertexAI</div>
  <div>        <span class="purple">return</span> ChatVertexAI(model=<span class="green">"gemini-1.5-pro"</span>)</div>
  <div></div>
  <div><span class="dim"># Usage — same agent code, different cloud</span></div>
  <div>llm = get_llm()  <span class="dim"># reads from LLM_PROVIDER env var</span></div>
  <div>agent = create_my_agent(llm)  <span class="dim"># all tools, chains, memory work identically</span></div>
</div>

<div class="lab-box"><h4>✏️ Phase 1 — Model Factory (30 min)</h4><ol>
  <li>Implement the <code>get_llm()</code> factory function above.</li>
  <li>Create a <code>.env</code> file with <code>LLM_PROVIDER=openai</code>. Verify it loads correctly.</li>
  <li>Switch to each provider and confirm the agent works identically.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 2 — Containerise with Docker (30 min)</h4><ol>
  <li>Write a Dockerfile: Python 3.12 base, install dependencies, copy agent code.</li>
  <li>Use environment variables for all secrets (API keys, endpoints). Never hardcode.</li>
  <li>Build and run locally: <code>docker build -t my-agent . && docker run -e LLM_PROVIDER=openai my-agent</code></li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 3 — Deploy to Cloud Compute (30 min)</h4><ol>
  <li>Push your Docker image to a container registry (ECR, ACR, or GCR).</li>
  <li>Deploy to a managed compute service: AWS ECS, Azure Container Instances, or GCP Cloud Run.</li>
  <li>Expose as an API endpoint. Test from Postman or curl.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Phase 4 — Production Hardening (30 min)</h4><ol>
  <li>Add an API gateway with rate limiting and authentication.</li>
  <li>Store secrets in a secrets manager (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager).</li>
  <li>Set up auto-scaling based on request volume.</li>
</ol></div>
</div></div>
</div><!-- /day4 -->

<!-- DAY 5 -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>
<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);"><div class="sched-time" style="color:var(--gum-dark)">Day 5</div><div class="sched-body"><h4>Cost comparison, final report & course graduation</h4><p>One topic · ~2 hours · Cover: Cross-cloud comparison + capstone deliverables</p></div></div>

<div class="topic-section"><div class="topic-header"><div class="topic-num" style="background:var(--earth);">★</div><h2>Capstone Deliverables & Course Graduation</h2><span class="topic-time">2 hrs</span></div>
<div class="topic-body">

<div class="lab-box"><h4>✏️ Deliverable 1 — Cross-Cloud Comparison Report (45 min)</h4><ol>
  <li>Run the same 20 queries on all three clouds (Bedrock/Claude, Azure/GPT-4o-mini, Vertex/Gemini).</li>
  <li>Measure for each: response quality (1–5 scale), latency (P50, P95), token cost.</li>
  <li>Create a comparison table with your findings. Include a recommendation section.</li>
</ol></div>

<div class="lab-box"><h4>✏️ Deliverable 2 — Architecture Diagram (30 min)</h4><ol>
  <li>Draw the full architecture of your deployed agent: user request → API gateway → compute → model provider → response.</li>
  <li>Include observability: where does Langfuse/LangSmith capture traces?</li>
  <li>Include error handling: what happens when the model provider is down?</li>
</ol></div>

<div class="lab-box"><h4>✏️ Deliverable 3 — Retrospective (30 min)</h4><ol>
  <li>Write a 1-page summary of what you learned across all 11 units.</li>
  <li>What was the most surprising thing? What would you do differently?</li>
  <li>What's your go-to stack? Which framework + cloud + observability tool would you default to for a new project?</li>
</ol></div>

<div style="margin:30px 0;padding:24px;background:linear-gradient(135deg,rgba(84,100,20,.1),rgba(224,248,46,.1));border-radius:12px;text-align:center;">
  <h3 style="font-size:22px;color:var(--gum-dark);margin-bottom:8px;border:none;">🎓 Congratulations!</h3>
  <p style="font-size:16px;color:var(--gray-700);max-width:600px;margin:0 auto;line-height:1.7;">You've completed the Agentic AI Engineering course. You can now design, build, deploy, monitor, and evaluate autonomous AI agents across multiple frameworks and cloud platforms. Go build something amazing.</p>
</div>
</div></div>
</div><!-- /day5 -->

<hr class="section-divider">
<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 11 — Summary</h2>
<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cloud comparison</strong> — Bedrock (multi-model), Azure (GPT), Vertex AI (Gemini)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>AWS Bedrock</strong> — ChatBedrock, 20+ models, built-in RAG</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Azure OpenAI</strong> — enterprise security, content filtering, provisioned throughput</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>GCP Vertex AI</strong> — Gemini, 2M context, multimodal, grounding</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Portability</strong> — model factory pattern, env-based provider switching</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Docker deployment</strong> — containerise and deploy to any cloud compute</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Production infra</strong> — API gateway, secrets management, auto-scaling</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Cost analysis</strong> — cross-cloud pricing comparison for the same workload</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>Your company is all-in on Azure. Should you still learn Bedrock and Vertex AI? Why?</li>
  <li>You need to process 100-page legal documents. Which cloud model would you choose and why?</li>
  <li>Design a multi-cloud setup: primary on Azure, fallback to Bedrock. How would you implement it?</li>
  <li>Compare the pricing models: pay-per-token (OpenAI) vs. provisioned throughput (Azure). When is each better?</li>
  <li>An agent needs to process medical records. Which cloud provider's compliance certifications matter most?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/05/23/u10-visual-low-code-agent-builders/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 10</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
</div>

</div>

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
