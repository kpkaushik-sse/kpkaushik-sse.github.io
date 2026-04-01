---
layout: default
title: "Unit 5 — Retrieval-Augmented Agent Pipelines"
date: 2026-04-25
categories: [agentic-ai, orchestration]
permalink: /blog/2026/04/25/u5-retrieval-augmented-agent-pipelines/
description: "Build production RAG systems — vector stores, embedding strategies, chunking, hybrid search, re-ranking, agentic RAG with LlamaIndex, and self-correcting retrieval pipelines."
---

<style>
.mod-page{max-width:820px;margin:0 auto;padding:0 0 48px}.mod-breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-500);margin-bottom:20px}.mod-breadcrumb a{color:var(--gum);text-decoration:none}.mod-breadcrumb a:hover{color:var(--earth)}.mod-hero{margin-bottom:32px}.mod-hero h1{font-size:32px;font-weight:700;line-height:1.2;margin-bottom:8px;border:none}.mod-hero-sub{font-size:16px;color:var(--gray-500);line-height:1.6;margin-bottom:16px}.mod-hero-meta{display:flex;flex-wrap:wrap;gap:12px}.mod-pill{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500}.mod-pill.track{background:rgba(84,100,20,.1);color:var(--gum)}.mod-pill.time{background:rgba(172,100,46,.1);color:var(--earth)}.mod-pill.hands{background:rgba(224,248,46,.15);color:var(--gum-dark)}.obj-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:20px 24px;margin-bottom:32px}.obj-card h3{font-size:15px;font-weight:600;margin-bottom:10px;border:none;display:flex;align-items:center;gap:6px}.obj-card ul{list-style:none;padding:0}.obj-card li{position:relative;padding-left:22px;margin-bottom:6px;font-size:14px;line-height:1.6}.obj-card li::before{content:"✓";position:absolute;left:0;color:var(--gum);font-weight:700}.day-tabs{display:flex;gap:4px;margin-bottom:0;border-bottom:2px solid var(--gray-200);overflow-x:auto}.day-tab{padding:10px 20px;font-size:14px;font-weight:500;cursor:pointer;border:none;background:none;color:var(--gray-500);border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .2s;white-space:nowrap}.day-tab:hover{color:var(--gray-700)}.day-tab.active{color:var(--gum);border-bottom-color:var(--gum)}.day-panel{display:none;padding-top:24px}.day-panel.active{display:block}.topic-section{margin-bottom:36px}.topic-header{display:flex;align-items:center;gap:12px;margin-bottom:16px}.topic-num{width:36px;height:36px;border-radius:50%;background:var(--gum);color:var(--white);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;flex-shrink:0}.topic-header h2{font-size:22px;font-weight:600;margin:0;border:none;padding:0}.topic-time{font-size:12px;color:var(--gray-500);margin-left:auto;white-space:nowrap;background:var(--gray-100);padding:3px 10px;border-radius:12px}.topic-body{padding-left:48px}.topic-body p{margin-bottom:14px;font-size:15px;line-height:1.8}.topic-body h3{font-size:17px;font-weight:600;margin:24px 0 10px;border:none;padding:0}.insight-box{background:linear-gradient(135deg,rgba(84,100,20,.06),rgba(235,252,211,.4));border-left:3px solid var(--gum);border-radius:0 var(--radius-sm) var(--radius-sm) 0;padding:14px 18px;margin:16px 0;font-size:14px;line-height:1.7}.insight-box strong{color:var(--gum-dark)}.blocks-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin:16px 0}@media(max-width:560px){.blocks-grid{grid-template-columns:1fr}}.block-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:14px 16px}.block-card h4{font-size:14px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:6px}.block-card p{font-size:13px;color:var(--gray-700);line-height:1.55;margin:0}.cmp-table{width:100%;border-collapse:collapse;margin:16px 0;font-size:13.5px}.cmp-table th{text-align:left;padding:10px 12px;background:var(--gray-100);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.4px}.cmp-table td{padding:10px 12px;border-bottom:1px solid var(--gray-200)}.cmp-table tr:last-child td{border-bottom:none}.cmp-table tr:hover td{background:rgba(84,100,20,.03)}.step-flow{display:flex;flex-direction:column;gap:12px;margin:20px 0}.step-card{background:var(--gray-900);border-radius:var(--radius-md);padding:20px 22px;color:var(--white);display:flex;gap:16px}.step-num{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:700;flex-shrink:0}.step-num.perceive{background:#6366f1;color:#fff}.step-num.plan{background:#8b5cf6;color:#fff}.step-num.act{background:var(--gum);color:#fff}.step-num.learn{background:var(--earth);color:#fff}.step-body{flex:1}.step-label{font-size:11px;font-weight:600;text-transform:uppercase;letter-spacing:.5px;margin-bottom:2px}.step-label.perceive{color:#a5b4fc}.step-label.plan{color:#c4b5fd}.step-label.act{color:#d9f99d}.step-label.learn{color:#fed7aa}.step-title{font-size:17px;font-weight:600;margin-bottom:6px}.step-desc{font-size:13.5px;line-height:1.65;color:#d1d5db}.step-tools{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap}.tool-badge{padding:4px 10px;border-radius:4px;font-size:11px;font-weight:600}.tool-badge.green{background:rgba(16,185,129,.2);color:#6ee7b7}.tool-badge.red{background:rgba(239,68,68,.2);color:#fca5a5}.tool-badge.blue{background:rgba(96,165,250,.2);color:#93c5fd}.tool-badge.amber{background:rgba(245,158,11,.2);color:#fcd34d}.tool-badge.purple{background:rgba(139,92,246,.2);color:#c4b5fd}.sched-card{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-md);padding:16px 20px;margin-bottom:12px;display:flex;gap:14px;align-items:flex-start}.sched-time{font-size:12px;font-weight:600;color:var(--gum);white-space:nowrap;min-width:90px;padding-top:2px}.sched-body h4{font-size:15px;font-weight:600;margin-bottom:4px}.sched-body p{font-size:13px;color:var(--gray-700);line-height:1.5;margin:0}.lab-box{background:linear-gradient(135deg,rgba(172,100,46,.06),rgba(172,100,46,.02));border:1px solid rgba(172,100,46,.2);border-radius:var(--radius-md);padding:20px 22px;margin:20px 0}.lab-box h4{font-size:15px;font-weight:600;color:var(--earth);margin-bottom:8px;display:flex;align-items:center;gap:6px}.lab-box ol,.lab-box ul{padding-left:20px}.lab-box li{font-size:14px;line-height:1.7;margin-bottom:4px}.day-progress{background:var(--gray-200);border-radius:6px;height:6px;margin-bottom:20px;overflow:hidden}.day-progress-fill{height:100%;background:var(--gum);border-radius:6px}.section-divider{border:none;height:1px;background:var(--gray-200);margin:36px 0}.summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:16px 0}@media(max-width:560px){.summary-grid{grid-template-columns:1fr}}.summary-item{background:var(--white);border:1px solid var(--gray-200);border-radius:var(--radius-sm);padding:12px 14px;font-size:13.5px;display:flex;align-items:flex-start;gap:8px}.summary-check{color:var(--gum);font-weight:700;flex-shrink:0}.arch-diagram{background:var(--gray-900);color:var(--white);border-radius:var(--radius-md);padding:24px;margin:16px 0;font-family:'Fira Code',monospace;font-size:13px;line-height:1.8;overflow-x:auto}.arch-diagram .title{color:#a5b4fc;font-weight:600;margin-bottom:8px}.arch-diagram .dim{color:#64748b}.arch-diagram .green{color:#6ee7b7}.arch-diagram .blue{color:#93c5fd}.arch-diagram .purple{color:#c4b5fd}.arch-diagram .yellow{color:#fcd34d}.arch-diagram .red{color:#fca5a5}.arch-diagram .orange{color:#fdba74}.arch-diagram .highlight{color:#E0F82E;font-weight:600}@media(max-width:768px){.mod-hero h1{font-size:24px}.topic-body{padding-left:0}.step-card{flex-direction:column;gap:10px}.sched-card{flex-direction:column;gap:6px}.sched-time{min-width:auto}}
</style>

<div class="mod-page">

<nav class="mod-breadcrumb">
  <a href="/">Home</a> <span>/</span>
  <a href="/courses/agentic-ai-engineering/">Course</a> <span>/</span>
  <span>Unit 5</span>
</nav>

<div class="mod-hero">
  <h1>Unit 5 — Retrieval-Augmented Agent Pipelines</h1>
  <p class="mod-hero-sub">LLMs know what they were trained on — nothing more. When your agent needs to answer questions about your company's docs, recent data, or private knowledge, it needs to retrieve information first. RAG (Retrieval-Augmented Generation) is how you give agents access to your data without retraining the model.</p>
  <div class="mod-hero-meta">
    <span class="mod-pill track">Track B · Orchestration Toolkits</span>
    <span class="mod-pill time">⏱ ~10 hrs across 5 days (Week 7)</span>
    <span class="mod-pill hands">🛠 2 hands-on projects</span>
  </div>
</div>

<div class="insight-box" style="margin-bottom:24px;">
  <strong>Prerequisite:</strong> Complete <a href="/blog/2026/04/18/u4-stateful-agent-workflows-langgraph/" style="color:var(--gum);">Unit 4 — Stateful Agent Workflows</a>. You need LangGraph fundamentals (state, nodes, conditional edges) because agentic RAG builds on graph-based workflows.
</div>

<div class="obj-card">
  <h3><span class="material-icons-outlined" style="font-size:18px">flag</span> What You Will Be Able To Do</h3>
  <ul>
    <li>Explain the RAG pipeline: ingest → chunk → embed → store → retrieve → generate</li>
    <li>Choose and implement chunking strategies: fixed-size, recursive, semantic, and document-aware</li>
    <li>Generate and store embeddings using OpenAI, Cohere, and open-source models</li>
    <li>Set up vector stores (FAISS, Chroma, Pinecone) and understand similarity search vs. MMR</li>
    <li>Implement hybrid search combining dense vectors with sparse BM25 keyword matching</li>
    <li>Add re-ranking with Cohere Rerank and cross-encoders to boost retrieval precision</li>
    <li>Build agentic RAG with LlamaIndex — query engines, routers, and sub-question decomposition</li>
    <li>Create a self-correcting RAG pipeline that detects hallucinations and re-retrieves</li>
  </ul>
</div>

<div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;">
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(84,100,20,.1);color:var(--gum);">RAG Architecture & Chunking</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(172,100,46,.1);color:var(--earth);">Vector Stores & Retrieval Strategies</span>
  <span style="padding:5px 14px;border-radius:20px;font-size:12px;font-weight:500;background:rgba(224,248,46,.15);color:var(--gum-dark);">Agentic RAG with LlamaIndex</span>
</div>

<div class="day-tabs" role="tablist">
  <button class="day-tab active" onclick="switchDay(1)" role="tab">Day 1</button>
  <button class="day-tab" onclick="switchDay(2)" role="tab">Day 2</button>
  <button class="day-tab" onclick="switchDay(3)" role="tab">Day 3</button>
  <button class="day-tab" onclick="switchDay(4)" role="tab">Day 4</button>
  <button class="day-tab" onclick="switchDay(5)" role="tab">Day 5</button>
</div>

<!-- DAY 1 — RAG Fundamentals -->
<div id="day1" class="day-panel active">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 1 overview</div>
  <div class="sched-body">
    <h4>Why RAG exists and how the pipeline works end-to-end</h4>
    <p>Two topics · ~2 hours · Cover: The RAG problem + Chunking strategies</p>
  </div>
</div>

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">1</div>
    <h2>The RAG Problem — Why LLMs Need External Knowledge</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>Every LLM has a <strong>knowledge cutoff</strong> — a date after which it knows nothing. GPT-4o's training data stops months before you deploy it. Ask it about yesterday's stock prices, your company's internal policies, or a document uploaded an hour ago, and it will either hallucinate an answer or admit it doesn't know.</p>

    <p>RAG solves this by adding a retrieval step before generation. Instead of relying solely on the model's training data, you <strong>search your own data sources</strong>, pull the most relevant chunks, inject them into the prompt, and let the LLM generate an answer grounded in retrieved facts.</p>

    <h3>The end-to-end RAG pipeline</h3>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num perceive">1</div>
        <div class="step-body">
          <div class="step-label perceive">INGEST</div>
          <div class="step-title">Load documents from any source</div>
          <div class="step-desc">PDFs, web pages, databases, APIs, CSVs, Notion pages. LangChain and LlamaIndex provide 100+ document loaders. Each loader normalises the source into a list of Document objects with text content and metadata.</div>
          <div class="step-tools"><span class="tool-badge green">Document loaders</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">2</div>
        <div class="step-body">
          <div class="step-label plan">CHUNK</div>
          <div class="step-title">Split documents into retrievable pieces</div>
          <div class="step-desc">A 50-page PDF can't fit in a prompt. Split it into chunks of 500–1000 tokens that each contain a coherent idea. The chunking strategy dramatically affects retrieval quality.</div>
          <div class="step-tools"><span class="tool-badge purple">Text splitters</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">3</div>
        <div class="step-body">
          <div class="step-label act">EMBED</div>
          <div class="step-title">Convert text chunks into vectors</div>
          <div class="step-desc">An embedding model converts each chunk into a high-dimensional vector (e.g., 1536 dimensions for OpenAI ada-002). Semantically similar texts produce similar vectors, enabling meaning-based search.</div>
          <div class="step-tools"><span class="tool-badge green">Embedding models</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num learn">4</div>
        <div class="step-body">
          <div class="step-label learn">STORE</div>
          <div class="step-title">Save embeddings in a vector database</div>
          <div class="step-desc">Vector stores (FAISS, Chroma, Pinecone, Weaviate) index the embeddings for fast similarity search. Given a query vector, they return the k most similar chunks in milliseconds.</div>
          <div class="step-tools"><span class="tool-badge amber">Vector stores</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num perceive">5</div>
        <div class="step-body">
          <div class="step-label perceive">RETRIEVE</div>
          <div class="step-title">Find the most relevant chunks for a query</div>
          <div class="step-desc">Embed the user's question, search the vector store, and return the top-k chunks. This is where hybrid search and re-ranking make the biggest difference.</div>
          <div class="step-tools"><span class="tool-badge blue">Similarity search</span><span class="tool-badge purple">Re-ranking</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">6</div>
        <div class="step-body">
          <div class="step-label act">GENERATE</div>
          <div class="step-title">LLM answers using retrieved context</div>
          <div class="step-desc">Inject the retrieved chunks into the prompt: "Based on the following context, answer the question: [context] [question]". The LLM generates a grounded response.</div>
          <div class="step-tools"><span class="tool-badge green">LLM generation</span></div>
        </div>
      </div>
    </div>

    <div class="insight-box">
      <strong>RAG vs. fine-tuning:</strong> Fine-tuning changes the model's weights — expensive, slow, and the knowledge is baked in permanently. RAG keeps the model untouched and swaps the knowledge at query time — cheap, fast to update, and you can add or remove documents instantly. Use fine-tuning for style/format changes; use RAG for knowledge.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Ask GPT-4o a question about a document that doesn't exist in its training data (e.g., your company's holiday policy). Note the hallucination.</li>
        <li>Now manually paste the document text into the prompt before the question. Compare the quality of the grounded answer.</li>
        <li>That manual paste is exactly what RAG automates. Draw the 6-step pipeline on paper and label each step.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">2</div>
    <h2>Chunking Strategies — The Most Underrated Step</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>Chunking is where most RAG systems silently fail. Bad chunking → bad retrieval → bad answers → users lose trust. The goal is to create chunks that are <strong>self-contained</strong> (make sense without context), <strong>coherent</strong> (contain one idea), and <strong>retrievable</strong> (likely to match a user's question).</p>

    <h3>Four chunking approaches</h3>

    <table class="cmp-table">
      <thead><tr><th>Strategy</th><th>How It Works</th><th>Best For</th><th>Watch Out</th></tr></thead>
      <tbody>
        <tr><td><strong>Fixed-size</strong></td><td>Split every N characters/tokens with optional overlap</td><td>Quick prototyping, uniform text</td><td>Splits mid-sentence, breaks semantic meaning</td></tr>
        <tr><td><strong>Recursive</strong></td><td>Try splitting by paragraphs, then sentences, then characters</td><td>General-purpose documents</td><td>May produce uneven chunk sizes</td></tr>
        <tr><td><strong>Semantic</strong></td><td>Group sentences by embedding similarity — split when topic changes</td><td>Long documents with varying topics</td><td>Slower (requires embedding each sentence)</td></tr>
        <tr><td><strong>Document-aware</strong></td><td>Use document structure (headings, sections, tables) as boundaries</td><td>Structured documents (markdown, HTML, code)</td><td>Requires document-type-specific parsers</td></tr>
      </tbody>
    </table>

    <div class="arch-diagram">
      <div class="title">RECURSIVE TEXT SPLITTER — MOST COMMON CHOICE</div>
      <div><span class="purple">from</span> langchain_text_splitters <span class="purple">import</span> RecursiveCharacterTextSplitter</div>
      <div></div>
      <div>splitter = RecursiveCharacterTextSplitter(</div>
      <div>    chunk_size=<span class="yellow">1000</span>,          <span class="dim"># target chunk size in characters</span></div>
      <div>    chunk_overlap=<span class="yellow">200</span>,        <span class="dim"># overlap between chunks for context</span></div>
      <div>    separators=[<span class="green">"\n\n"</span>, <span class="green">"\n"</span>, <span class="green">". "</span>, <span class="green">" "</span>],  <span class="dim"># try these in order</span></div>
      <div>)</div>
      <div></div>
      <div>chunks = splitter.split_documents(documents)</div>
      <div><span class="dim"># Each chunk preserves paragraph boundaries when possible</span></div>
    </div>

    <div class="insight-box">
      <strong>The overlap trick:</strong> A 200-character overlap means each chunk shares its last 200 characters with the next chunk's first 200. This ensures that if an important sentence spans two chunks, it appears in full in at least one of them. Overlap typically ranges from 10–20% of chunk_size.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Take a 5-page document and split it using <code>RecursiveCharacterTextSplitter</code> with chunk_size=500 and no overlap. Read the chunks — do any split mid-sentence?</li>
        <li>Re-split with chunk_overlap=100. Find a chunk where the overlap preserved an important sentence.</li>
        <li>Try <code>MarkdownTextSplitter</code> on a markdown file. Compare the chunk boundaries with the recursive splitter — which preserves section structure better?</li>
      </ol>
    </div>
  </div>
</div>
</div><!-- /day1 -->

<!-- DAY 2 — Embeddings & Vector Stores -->
<div id="day2" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 2 overview</div>
  <div class="sched-body">
    <h4>Embeddings, vector stores, and similarity search</h4>
    <p>Two topics · ~2 hours · Cover: Embedding models + Vector store setup & querying</p>
  </div>
</div>

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">3</div>
    <h2>Embedding Models — Turning Text into Vectors</h2>
    <span class="topic-time">45 min</span>
  </div>
  <div class="topic-body">
    <p>An embedding model converts text into a fixed-length vector of floating-point numbers. The key property: <strong>semantically similar texts produce vectors that are close together</strong> in the vector space. "How to cook pasta" and "Italian cooking recipe" will have nearly identical vectors, even though they share no words.</p>

    <h3>Popular embedding models</h3>
    <table class="cmp-table">
      <thead><tr><th>Model</th><th>Provider</th><th>Dimensions</th><th>Cost</th><th>Notes</th></tr></thead>
      <tbody>
        <tr><td><strong>text-embedding-3-small</strong></td><td>OpenAI</td><td>1536</td><td>$0.02/1M tokens</td><td>Best cost-performance ratio for most use cases</td></tr>
        <tr><td><strong>text-embedding-3-large</strong></td><td>OpenAI</td><td>3072</td><td>$0.13/1M tokens</td><td>Higher accuracy, 2x the dimensions and cost</td></tr>
        <tr><td><strong>embed-v3</strong></td><td>Cohere</td><td>1024</td><td>Free tier available</td><td>Supports search_document vs search_query input types</td></tr>
        <tr><td><strong>all-MiniLM-L6-v2</strong></td><td>HuggingFace (local)</td><td>384</td><td>Free (run locally)</td><td>Fast, lightweight, good for prototyping</td></tr>
      </tbody>
    </table>

    <div class="arch-diagram">
      <div class="title">EMBEDDING WITH LANGCHAIN</div>
      <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> OpenAIEmbeddings</div>
      <div></div>
      <div>embeddings = OpenAIEmbeddings(model=<span class="green">"text-embedding-3-small"</span>)</div>
      <div></div>
      <div><span class="dim"># Embed a single query</span></div>
      <div>query_vec = embeddings.embed_query(<span class="green">"What is agentic AI?"</span>)</div>
      <div>print(len(query_vec))  <span class="dim"># → 1536</span></div>
      <div></div>
      <div><span class="dim"># Embed multiple documents</span></div>
      <div>doc_vecs = embeddings.embed_documents([<span class="green">"chunk 1 text"</span>, <span class="green">"chunk 2 text"</span>])</div>
    </div>

    <div class="insight-box">
      <strong>Never mix embedding models.</strong> If you embed documents with model A and query with model B, the vectors live in different spaces and similarity search produces garbage. Pick one model and use it consistently for both documents and queries.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Embed three sentences: one about cooking, one about programming, one about cooking with code. Compute cosine similarity between all pairs and verify the cooking sentences are closest.</li>
        <li>Compare OpenAI embeddings (1536-dim) with HuggingFace all-MiniLM (384-dim). Is the quality difference noticeable for your test sentences?</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">4</div>
    <h2>Vector Stores — FAISS, Chroma & Pinecone</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>A vector store is a specialised database that indexes embeddings for fast similarity search. You give it a query vector, and it returns the k most similar vectors (and their associated text chunks) in milliseconds — even across millions of documents.</p>

    <h3>Local vs. managed vector stores</h3>
    <div class="blocks-grid">
      <div class="block-card" style="border-left:3px solid #6ee7b7;">
        <h4>FAISS (local)</h4>
        <p>Facebook's library. Runs in-memory, no server needed. Lightning fast for up to ~1M vectors. Great for development and single-machine production.</p>
      </div>
      <div class="block-card" style="border-left:3px solid #93c5fd;">
        <h4>Chroma (local/server)</h4>
        <p>Developer-friendly, supports metadata filtering. Runs locally or as a server. Good middle ground between FAISS simplicity and production features.</p>
      </div>
      <div class="block-card" style="border-left:3px solid #c4b5fd;">
        <h4>Pinecone (managed cloud)</h4>
        <p>Fully managed, auto-scaling, serverless option. Handles billions of vectors. Best for production when you don't want to manage infrastructure.</p>
      </div>
      <div class="block-card" style="border-left:3px solid #fcd34d;">
        <h4>Weaviate (managed/self-hosted)</h4>
        <p>Supports hybrid search natively (vector + keyword). GraphQL API. Good when you need both semantic and keyword search in one store.</p>
      </div>
    </div>

    <div class="arch-diagram">
      <div class="title">FAISS — QUICK SETUP</div>
      <div><span class="purple">from</span> langchain_community.vectorstores <span class="purple">import</span> FAISS</div>
      <div><span class="purple">from</span> langchain_openai <span class="purple">import</span> OpenAIEmbeddings</div>
      <div></div>
      <div><span class="dim"># Create from documents (embed + store in one call)</span></div>
      <div>vectorstore = FAISS.from_documents(chunks, OpenAIEmbeddings())</div>
      <div></div>
      <div><span class="dim"># Similarity search — returns top 4 most relevant chunks</span></div>
      <div>results = vectorstore.similarity_search(<span class="green">"What is RAG?"</span>, k=<span class="yellow">4</span>)</div>
      <div><span class="purple">for</span> doc <span class="purple">in</span> results:</div>
      <div>    print(doc.page_content[:100])</div>
      <div></div>
      <div><span class="dim"># Save to disk and reload later</span></div>
      <div>vectorstore.save_local(<span class="green">"./faiss_index"</span>)</div>
      <div>vectorstore = FAISS.load_local(<span class="green">"./faiss_index"</span>, OpenAIEmbeddings())</div>
    </div>

    <h3>Similarity search vs. MMR</h3>
    <table class="cmp-table">
      <thead><tr><th>Method</th><th>How It Works</th><th>When to Use</th></tr></thead>
      <tbody>
        <tr><td><strong>Similarity</strong></td><td>Returns the k vectors closest to the query</td><td>When you want the most relevant results, even if they're redundant</td></tr>
        <tr><td><strong>MMR (Maximal Marginal Relevance)</strong></td><td>Balances relevance with diversity — avoids returning near-duplicate chunks</td><td>When your chunks have overlap and you want broad coverage</td></tr>
      </tbody>
    </table>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Load a PDF with <code>PyPDFLoader</code>, chunk it, and create a FAISS vector store.</li>
        <li>Run a similarity search and an MMR search with the same query. Compare the results — does MMR provide more diverse answers?</li>
        <li>Save the FAISS index to disk, restart Python, reload the index, and verify search still works.</li>
      </ol>
    </div>
  </div>
</div>
</div><!-- /day2 -->

<!-- DAY 3 — Hybrid Search & Re-ranking -->
<div id="day3" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 3 overview</div>
  <div class="sched-body">
    <h4>Advanced retrieval — hybrid search and re-ranking to boost precision</h4>
    <p>Two topics · ~2 hours · Cover: Hybrid search + Re-ranking strategies</p>
  </div>
</div>

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">5</div>
    <h2>Hybrid Search — Vectors + Keywords Together</h2>
    <span class="topic-time">50 min</span>
  </div>
  <div class="topic-body">
    <p>Pure vector search is great at understanding meaning but can miss exact matches. If a user searches for error code "ERR-4032", a semantic embedding won't find it — but a keyword search will. <strong>Hybrid search</strong> combines both approaches: dense vector search for meaning + sparse BM25 search for exact keywords.</p>

    <h3>How hybrid search works</h3>
    <div class="arch-diagram">
      <div class="title">HYBRID SEARCH PIPELINE</div>
      <div><span class="green">User Query</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">├───▶</span> <span class="blue">Dense Retriever</span> <span class="dim">(vector similarity)</span> ──▶ <span class="blue">Top-K results</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">├───▶</span> <span class="purple">Sparse Retriever</span> <span class="dim">(BM25 keyword)</span> ──▶ <span class="purple">Top-K results</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="yellow">Reciprocal Rank Fusion</span> <span class="dim">— merge + re-score both result sets</span></div>
      <div>  <span class="dim">│</span></div>
      <div>  <span class="dim">▼</span></div>
      <div><span class="highlight">Final ranked results</span></div>
    </div>

    <div class="arch-diagram">
      <div class="title">LANGCHAIN ENSEMBLE RETRIEVER</div>
      <div><span class="purple">from</span> langchain.retrievers <span class="purple">import</span> EnsembleRetriever</div>
      <div><span class="purple">from</span> langchain_community.retrievers <span class="purple">import</span> BM25Retriever</div>
      <div></div>
      <div><span class="dim"># Dense retriever — vector similarity</span></div>
      <div>vector_retriever = vectorstore.as_retriever(search_kwargs={<span class="green">"k"</span>: <span class="yellow">5</span>})</div>
      <div></div>
      <div><span class="dim"># Sparse retriever — BM25 keyword matching</span></div>
      <div>bm25_retriever = BM25Retriever.from_documents(chunks, k=<span class="yellow">5</span>)</div>
      <div></div>
      <div><span class="dim"># Combine with equal weights</span></div>
      <div>hybrid = EnsembleRetriever(</div>
      <div>    retrievers=[vector_retriever, bm25_retriever],</div>
      <div>    weights=[<span class="yellow">0.5</span>, <span class="yellow">0.5</span>],</div>
      <div>)</div>
      <div></div>
      <div>results = hybrid.invoke(<span class="green">"error code ERR-4032 in production"</span>)</div>
    </div>

    <div class="insight-box">
      <strong>When to use hybrid search:</strong> Technical documentation (error codes, API endpoints, config keys), legal documents (section numbers, clause references), medical records (drug names, ICD codes). Anytime exact tokens matter alongside semantic meaning.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Create both a FAISS retriever and a BM25 retriever from the same document chunks.</li>
        <li>Search for a specific error code that appears verbatim in the documents. Compare results from vector-only, BM25-only, and hybrid.</li>
        <li>Adjust the weights (0.7 vector / 0.3 BM25) and observe how result ordering changes.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">6</div>
    <h2>Re-Ranking — Precision After Retrieval</h2>
    <span class="topic-time">50 min</span>
  </div>
  <div class="topic-body">
    <p>Retrieval cast a wide net — you pull back 20 chunks. But only 3–5 are truly relevant. <strong>Re-ranking</strong> is a second-pass scoring step that uses a more powerful model (a cross-encoder) to re-score each retrieved chunk against the query and surface the best ones to the top.</p>

    <h3>Why re-ranking matters</h3>
    <p>Embedding-based retrieval uses bi-encoders — the query and document are encoded separately, then compared. This is fast but imprecise because the model never sees the query and document together. A cross-encoder scores the query-document pair <em>together</em>, which is far more accurate but too slow to run over millions of documents. So you do a two-stage approach: fast retrieval first, precise re-ranking second.</p>

    <div class="arch-diagram">
      <div class="title">TWO-STAGE RETRIEVAL</div>
      <div><span class="green">Query</span> → <span class="blue">Bi-encoder retrieval</span> <span class="dim">(fast, top-20)</span></div>
      <div>      → <span class="purple">Cross-encoder re-ranking</span> <span class="dim">(precise, top-5)</span></div>
      <div>      → <span class="highlight">LLM generation</span></div>
    </div>

    <div class="arch-diagram">
      <div class="title">COHERE RE-RANKER WITH LANGCHAIN</div>
      <div><span class="purple">from</span> langchain.retrievers <span class="purple">import</span> ContextualCompressionRetriever</div>
      <div><span class="purple">from</span> langchain_cohere <span class="purple">import</span> CohereRerank</div>
      <div></div>
      <div><span class="dim"># Base retriever pulls top-20</span></div>
      <div>base_retriever = vectorstore.as_retriever(search_kwargs={<span class="green">"k"</span>: <span class="yellow">20</span>})</div>
      <div></div>
      <div><span class="dim"># Re-ranker scores and keeps top-5</span></div>
      <div>reranker = CohereRerank(top_n=<span class="yellow">5</span>)</div>
      <div></div>
      <div>retriever = ContextualCompressionRetriever(</div>
      <div>    base_compressor=reranker,</div>
      <div>    base_retriever=base_retriever,</div>
      <div>)</div>
      <div></div>
      <div>results = retriever.invoke(<span class="green">"How does RAG handle hallucinations?"</span>)</div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Set up Cohere re-ranking (free API key) with your FAISS retriever. Compare top-5 results with and without re-ranking.</li>
        <li>Measure latency: how much time does re-ranking add vs. the quality improvement?</li>
        <li>Try different <code>top_n</code> values (3, 5, 10). At what point does adding more chunks stop improving answer quality?</li>
      </ol>
    </div>
  </div>
</div>
</div><!-- /day3 -->

<!-- DAY 4 — Agentic RAG & LlamaIndex -->
<div id="day4" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 4 overview</div>
  <div class="sched-body">
    <h4>From passive RAG to agentic RAG — self-correcting retrieval with LlamaIndex</h4>
    <p>Two topics · ~2.5 hours · Cover: LlamaIndex fundamentals + Agentic RAG patterns</p>
  </div>
</div>

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">7</div>
    <h2>LlamaIndex — The RAG-First Framework</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>While LangChain is a general-purpose LLM framework that includes RAG features, <strong>LlamaIndex is purpose-built for data retrieval and augmentation</strong>. It excels at connecting LLMs to structured and unstructured data sources through a rich set of indexing and querying abstractions.</p>

    <h3>LlamaIndex core concepts</h3>
    <div class="blocks-grid">
      <div class="block-card">
        <h4>📄 Documents & Nodes</h4>
        <p>A Document is a loaded file. Nodes are the chunks — LlamaIndex splits documents into nodes automatically with metadata, relationships, and embeddings.</p>
      </div>
      <div class="block-card">
        <h4>📇 Indices</h4>
        <p>An Index organises nodes for retrieval. VectorStoreIndex (most common), SummaryIndex (for entire-document summarisation), TreeIndex (hierarchical).</p>
      </div>
      <div class="block-card">
        <h4>🔍 Query Engines</h4>
        <p>An interface that takes a natural language query and returns a response. Handles retrieval + synthesis in one step. Supports streaming, filtering, and citations.</p>
      </div>
      <div class="block-card">
        <h4>🔀 Routers</h4>
        <p>Route queries to different indices based on the question type. "Financial data → SQL index. Policy questions → vector index." Like conditional edges in LangGraph.</p>
      </div>
    </div>

    <div class="arch-diagram">
      <div class="title">LLAMAINDEX — FIVE-LINE RAG PIPELINE</div>
      <div><span class="purple">from</span> llama_index.core <span class="purple">import</span> VectorStoreIndex, SimpleDirectoryReader</div>
      <div></div>
      <div><span class="dim"># Load + chunk + embed + store — all in two lines</span></div>
      <div>documents = SimpleDirectoryReader(<span class="green">"./data"</span>).load_data()</div>
      <div>index = VectorStoreIndex.from_documents(documents)</div>
      <div></div>
      <div><span class="dim"># Query</span></div>
      <div>engine = index.as_query_engine()</div>
      <div>response = engine.query(<span class="green">"What is the refund policy?"</span>)</div>
      <div>print(response)</div>
    </div>

    <div class="insight-box">
      <strong>LangChain vs. LlamaIndex for RAG:</strong> Use LlamaIndex when RAG is the core of your application — it has better indexing strategies, citation support, and query optimisation. Use LangChain when RAG is one feature among many (tools, agents, chains). They can also be combined: use LlamaIndex for the retrieval layer and LangChain for the agent layer.
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Install LlamaIndex: <code>pip install llama-index</code></li>
        <li>Create a <code>./data</code> folder, put 2–3 text files in it, and run the five-line pipeline above.</li>
        <li>Try <code>as_query_engine(streaming=True)</code> and observe token-by-token response streaming.</li>
        <li>Enable citation mode and verify that the response includes references to specific source documents.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num">8</div>
    <h2>Agentic RAG — Self-Correcting Retrieval</h2>
    <span class="topic-time">60 min</span>
  </div>
  <div class="topic-body">
    <p>Standard RAG is passive: retrieve → generate → done. If the retrieval was bad, the answer is bad — and nobody catches it. <strong>Agentic RAG</strong> adds an agent loop around the retrieval step: the agent evaluates whether the retrieved documents actually answer the question, and if not, it reformulates the query and retrieves again.</p>

    <h3>Three agentic RAG patterns</h3>

    <div class="step-flow">
      <div class="step-card">
        <div class="step-num perceive">1</div>
        <div class="step-body">
          <div class="step-label perceive">SELF-REFLECTING RAG</div>
          <div class="step-title">Check → Retry if insufficient</div>
          <div class="step-desc">After retrieval, the agent asks: "Do these chunks actually answer the question?" If not, it reformulates the query (more specific, different keywords) and retrieves again. Loops up to N times.</div>
          <div class="step-tools"><span class="tool-badge green">Query reformulation</span><span class="tool-badge blue">Relevance grading</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num plan">2</div>
        <div class="step-body">
          <div class="step-label plan">SUB-QUESTION DECOMPOSITION</div>
          <div class="step-title">Break complex queries into parts</div>
          <div class="step-desc">"Compare Q1 and Q2 revenue" becomes two sub-queries: "What was Q1 revenue?" and "What was Q2 revenue?" Each sub-query retrieves independently, and the results are synthesised into a final answer.</div>
          <div class="step-tools"><span class="tool-badge purple">Query decomposition</span><span class="tool-badge amber">Multi-retrieval</span></div>
        </div>
      </div>
      <div class="step-card">
        <div class="step-num act">3</div>
        <div class="step-body">
          <div class="step-label act">ROUTER RAG</div>
          <div class="step-title">Route to the right data source</div>
          <div class="step-desc">Different questions need different indices. "What was last year's revenue?" → SQL database. "What does the policy say?" → document vector store. A router agent decides which index to query based on the question type.</div>
          <div class="step-tools"><span class="tool-badge green">Index routing</span><span class="tool-badge red">Multi-index</span></div>
        </div>
      </div>
    </div>

    <div class="arch-diagram">
      <div class="title">SELF-CORRECTING RAG WITH LANGGRAPH</div>
      <div></div>
      <div><span class="green">START</span> → <span class="blue">retrieve</span> → <span class="yellow">grade_relevance</span> ─┐</div>
      <div><span class="dim">                                     │</span></div>
      <div><span class="dim">          ┌─── "relevant" ───────────┘</span></div>
      <div><span class="dim">          │</span></div>
      <div><span class="dim">          ▼</span></div>
      <div><span class="purple">     generate</span> → <span class="yellow">check_hallucination</span> ─┐</div>
      <div><span class="dim">                                     │</span></div>
      <div><span class="dim">          ┌─── "grounded" ──────────┘</span></div>
      <div><span class="dim">          ▼</span></div>
      <div><span class="red">         END</span></div>
      <div></div>
      <div><span class="dim">"not_relevant" → </span><span class="orange">reformulate_query</span><span class="dim"> → retrieve (cycle)</span></div>
      <div><span class="dim">"hallucinated" → </span><span class="orange">regenerate</span><span class="dim"> → check_hallucination (cycle)</span></div>
    </div>

    <div class="lab-box">
      <h4>✏️ Mini-exercise</h4>
      <ol>
        <li>Build a relevance grading chain: given a query and a retrieved chunk, have the LLM return "relevant" or "not_relevant" with a confidence score.</li>
        <li>Build a hallucination checker: given the retrieved context and the generated answer, have the LLM verify that every claim in the answer is supported by the context.</li>
        <li>Wire both into a LangGraph with the self-correcting pattern shown above. Test with a question that your documents can answer and one they can't.</li>
      </ol>
    </div>
  </div>
</div>
</div><!-- /day4 -->

<!-- DAY 5 — Projects -->
<div id="day5" class="day-panel">
<div class="day-progress"><div class="day-progress-fill" style="width:0%"></div></div>

<div class="sched-card" style="background:var(--eucalyptus);border-color:rgba(84,100,20,.2);">
  <div class="sched-time" style="color:var(--gum-dark)">Day 5 overview</div>
  <div class="sched-body">
    <h4>Two hands-on projects — build real RAG applications</h4>
    <p>Two projects · ~3 hours · Apply everything from this week</p>
  </div>
</div>

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background:var(--earth);">P1</div>
    <h2>Project 1 — Quarterly Earnings Summariser</h2>
    <span class="topic-time">90 min</span>
  </div>
  <div class="topic-body">
    <p>Build a RAG agent that ingests quarterly earnings reports (PDFs), indexes them in a vector store, and answers analyst-style questions with cited sources. The agent should handle multi-quarter comparisons using sub-question decomposition.</p>

    <div class="lab-box">
      <h4>✏️ Phase 1 — Ingest & Index (30 min)</h4>
      <ol>
        <li>Download 2–3 sample earnings reports (public filings from SEC EDGAR or any public company).</li>
        <li>Load with <code>PyPDFLoader</code>, chunk with <code>RecursiveCharacterTextSplitter</code> (chunk_size=800, overlap=150).</li>
        <li>Create a FAISS vector store. Add metadata (company name, quarter, year) to each chunk.</li>
      </ol>
    </div>

    <div class="lab-box">
      <h4>✏️ Phase 2 — Retrieval Chain (30 min)</h4>
      <ol>
        <li>Build a basic RAG chain: retriever → prompt (inject context) → LLM → StrOutputParser.</li>
        <li>Add Cohere re-ranking to boost precision.</li>
        <li>Test with: "What was the revenue in Q3 2024?" and verify the answer cites the correct document.</li>
      </ol>
    </div>

    <div class="lab-box">
      <h4>✏️ Phase 3 — Agentic RAG (30 min)</h4>
      <ol>
        <li>Add sub-question decomposition: "Compare Q2 and Q3 revenue" should split into two sub-queries.</li>
        <li>Add relevance grading and hallucination checking.</li>
        <li>Test with a question your documents DON'T answer. Verify the agent says "I don't have enough information" instead of hallucinating.</li>
      </ol>
    </div>
  </div>
</div>

<hr class="section-divider">

<div class="topic-section">
  <div class="topic-header">
    <div class="topic-num" style="background:var(--earth);">P2</div>
    <h2>Project 2 — Competitive Intelligence Bot</h2>
    <span class="topic-time">90 min</span>
  </div>
  <div class="topic-body">
    <p>Build a router-based RAG agent that answers questions from multiple data sources: product documentation (vector store), pricing data (SQL database), and competitor press releases (web search). The agent routes each query to the right source.</p>

    <div class="lab-box">
      <h4>✏️ Tasks</h4>
      <ol>
        <li>Create three data sources: (a) vector store from product docs, (b) SQLite database with pricing tables, (c) Tavily web search tool for real-time competitor news.</li>
        <li>Build a LangGraph router that classifies the query as "product", "pricing", or "competitor" and routes to the appropriate source.</li>
        <li>Implement the full flow: classify → route → retrieve → generate. Test with questions for each source type.</li>
        <li>Add a fallback: if no source has a confident answer, combine results from all three sources.</li>
      </ol>
    </div>
  </div>
</div>
</div><!-- /day5 -->

<!-- SUMMARY -->
<hr class="section-divider">

<h2 style="font-size:22px;font-weight:700;margin-bottom:16px;">Unit 5 — Summary</h2>

<div class="summary-grid">
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>RAG pipeline</strong> — ingest → chunk → embed → store → retrieve → generate</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Chunking strategies</strong> — fixed-size, recursive, semantic, document-aware</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Embeddings</strong> — OpenAI, Cohere, HuggingFace; never mix models</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Vector stores</strong> — FAISS (local), Chroma (hybrid), Pinecone (managed)</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Similarity vs. MMR</strong> — relevance-only vs. relevance + diversity</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Hybrid search</strong> — dense vectors + sparse BM25 via EnsembleRetriever</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Re-ranking</strong> — cross-encoder second pass; Cohere Rerank integration</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>LlamaIndex</strong> — Documents, Nodes, Indices, Query Engines, Routers</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Agentic RAG</strong> — self-correcting retrieval, sub-question decomposition, router RAG</span></div>
  <div class="summary-item"><span class="summary-check">✓</span> <span><strong>Hallucination detection</strong> — grading retrieval relevance and checking answer groundedness</span></div>
</div>

<h3 style="font-size:17px;margin-top:24px;margin-bottom:12px;">Check Your Understanding</h3>
<ol style="padding-left:20px;font-size:14px;line-height:1.8;">
  <li>Why is chunking the most impactful step in a RAG pipeline? What happens with chunks that are too large or too small?</li>
  <li>Explain why you can't mix embedding models between indexing and querying.</li>
  <li>When would you choose FAISS over Pinecone? When would Pinecone be worth the cost?</li>
  <li>Describe the two-stage retrieval pattern. Why not just run the cross-encoder over all documents?</li>
  <li>Design an agentic RAG system for a legal firm. What data sources, chunking strategies, and retrieval patterns would you use?</li>
  <li>How does sub-question decomposition handle "Compare X and Y" queries? Why can't simple RAG handle them well?</li>
</ol>

<div style="margin-top:24px;display:flex;gap:12px;flex-wrap:wrap;justify-content:center;">
  <a href="/blog/2026/04/18/u4-stateful-agent-workflows-langgraph/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">← Unit 4</a>
  <a href="/courses/agentic-ai-engineering/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gum);color:var(--white);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Course Overview</a>
  <a href="/blog/2026/05/02/u6-rapid-agent-prototyping-phidata/" style="display:inline-flex;align-items:center;gap:6px;padding:12px 28px;background:var(--gray-200);color:var(--gray-700);border-radius:8px;text-decoration:none;font-weight:600;font-size:15px;">Unit 6 →</a>
</div>

</div><!-- /mod-page -->

<script>
function switchDay(n){document.querySelectorAll('.day-tab').forEach(function(t,i){t.classList.toggle('active',i===n-1)});document.querySelectorAll('.day-panel').forEach(function(p,i){p.classList.toggle('active',i===n-1)});window.scrollTo({top:document.querySelector('.day-tabs').offsetTop-70,behavior:'smooth'})}
</script>
