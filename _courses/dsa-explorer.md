---
layout: default
title: "DSA Explorer — Interactive Algorithm & Data Structure Track"
permalink: /courses/dsa-explorer/
description: "A visual, interactive learning track covering 12 essential algorithms and data structures — sorting, searching, graph traversal, dynamic programming, and core data structures with step-by-step animations."
---

<style>
  /* Course page — harmonized with LMS layout */
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
  .tag.algo    { background: #E6F1FB; color: #0C447C; border-color: #B5D4F4; }
  .tag.viz     { background: #EAF3DE; color: #27500A; border-color: #C0DD97; }
  .tag.concept { background: #EEEDFE; color: #3C3489; border-color: #CECBF6; }
  .tag.ds      { background: #FAEEDA; color: #633806; border-color: #FAC775; }

  .explorer-cta {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    margin-top: 8px;
    padding: 5px 12px;
    border-radius: 999px;
    border: 0.5px solid #00b8d4;
    background: #006064;
    color: #FFFFFF;
    font-size: 11px;
    font-weight: 600;
    text-decoration: none;
    transition: background 0.2s ease, transform 0.2s ease;
  }
  .explorer-cta:hover {
    background: #004d52;
    transform: translateY(-1px);
  }

  @media (prefers-color-scheme: dark) {
    .tag.algo    { background: #0C447C; color: #B5D4F4; border-color: #185FA5; }
    .tag.viz     { background: #27500A; color: #C0DD97; border-color: #3B6D11; }
    .tag.concept { background: #3C3489; color: #CECBF6; border-color: #534AB7; }
    .tag.ds      { background: #633806; color: #FAC775; border-color: #8B4F08; }
  }

  .progress-bar  { height: 4px; border-radius: 2px; background: var(--c-border); margin: 6px 0 10px; }
  .progress-fill { height: 4px; border-radius: 2px; }

  .tip-box { background: var(--c-bg-secondary); border-left: 3px solid #00b8d4; border-radius: 0 var(--r-md) var(--r-md) 0; padding: 8px 12px; margin-top: 10px; font-size: 12px; color: var(--c-text-secondary); line-height: 1.55; }

  .study-footer { margin-top: 16px; padding: 10px 14px; background: var(--c-bg-secondary); border-radius: var(--r-md); border: 0.5px solid var(--c-border); font-size: 12px; color: var(--c-text-secondary); line-height: 1.6; }
  .study-footer strong { color: var(--c-text-primary); font-weight: 600; }
  .back-link { display: inline-block; font-size: 13px; margin-bottom: 14px; color: var(--c-text-secondary); text-decoration: none; }
  .back-link:hover { color: var(--c-text-primary); }
</style>

<div class="course-page">
  <a class="back-link" href="/courses/">&larr; All Courses</a>

  <div class="course-hero-title">DSA Explorer — Interactive Algorithm &amp; Data Structure Track</div>
  <div class="course-hero-sub">Visual walkthroughs &nbsp;&middot;&nbsp; 12 algorithms &nbsp;&middot;&nbsp; 5 categories &nbsp;&middot;&nbsp; 4 views per algorithm</div>

  <div class="overview-grid">
    <div class="stat-card"><div class="stat-label">Algorithms</div><div class="stat-val">12</div></div>
    <div class="stat-card"><div class="stat-label">Categories</div><div class="stat-val">5</div></div>
    <div class="stat-card"><div class="stat-label">Views per algo</div><div class="stat-val">4</div></div>
  </div>

  <p style="font-size:13px; color:var(--c-text-secondary); margin-bottom:16px; line-height:1.7;">
    Each algorithm includes <strong>step-by-step visual animations</strong>, complexity analysis with Big-O growth charts, real-world use cases, and production-ready Python code. Use the interactive explorer to play, step through, and reset each algorithm at your own pace.
  </p>

<a class="explorer-cta" href="/dsa-explorer.html" style="margin-bottom:18px; display:inline-flex;">▶ Open Interactive DSA Explorer</a>

  <!-- MODULE A — SORTING -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p1')">
      <span class="phase-badge" style="background:#E6F1FB;color:#0C447C;border:0.5px solid #B5D4F4;">Module A</span>
      <span class="phase-title">Sorting Algorithms</span>
      <span class="phase-meta">3 algorithms</span>
      <span class="chevron" id="p1-chev">▶</span>
    </div>
    <div class="phase-body" id="p1">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#378ADD;"></div></div>

      <div class="mod-row">
        <div class="mod-num">1</div>
        <div class="mod-content">
          <div class="mod-title">Quick Sort</div>
          <div class="mod-duration">Avg O(n log n) &middot; Space O(log n) &middot; Unstable</div>
          <div class="mod-tags">
            <span class="tag algo">Divide &amp; conquer</span>
            <span class="tag concept">Lomuto partition</span>
            <span class="tag viz">Animated visualization</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Selects a pivot, partitions elements around it, and recursively sorts sub-arrays. In-place with excellent cache performance. Used in C++ std::sort, Java Arrays.sort for primitives.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">2</div>
        <div class="mod-content">
          <div class="mod-title">Merge Sort</div>
          <div class="mod-duration">O(n log n) all cases &middot; Space O(n) &middot; Stable</div>
          <div class="mod-tags">
            <span class="tag algo">Divide &amp; conquer</span>
            <span class="tag concept">Stability guarantee</span>
            <span class="tag viz">Animated visualization</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Recursively splits arrays then merges sorted halves. Guarantees O(n log n) in ALL cases. Ideal for linked lists, external sort (disk), and parallel sorting.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">3</div>
        <div class="mod-content">
          <div class="mod-title">Heap Sort</div>
          <div class="mod-duration">O(n log n) all cases &middot; Space O(1) &middot; Unstable</div>
          <div class="mod-tags">
            <span class="tag algo">Binary heap</span>
            <span class="tag concept">Priority queues</span>
            <span class="tag viz">Animated visualization</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Builds a max-heap then repeatedly extracts the maximum. O(1) auxiliary space makes it ideal for embedded systems. Powers most priority queue implementations.</p>
        </div>
      </div>

      <div class="tip-box">Compare all three sorting algorithms side by side in the Explorer. Pay attention to how Quick Sort's pivot selection affects worst-case behavior, and why Merge Sort's stability matters for multi-key sorting.</div>
    </div>

  </div>

  <!-- MODULE B — SEARCHING -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p2')">
      <span class="phase-badge" style="background:#EEEDFE;color:#3C3489;border:0.5px solid #CECBF6;">Module B</span>
      <span class="phase-title">Searching Algorithms</span>
      <span class="phase-meta">2 algorithms</span>
      <span class="chevron" id="p2-chev">▶</span>
    </div>
    <div class="phase-body" id="p2">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#7F77DD;"></div></div>

      <div class="mod-row">
        <div class="mod-num">4</div>
        <div class="mod-content">
          <div class="mod-title">Binary Search</div>
          <div class="mod-duration">O(log n) &middot; Space O(1) &middot; Requires sorted input</div>
          <div class="mod-tags">
            <span class="tag algo">Halving search space</span>
            <span class="tag concept">Lower/upper bound</span>
            <span class="tag concept">Search on answer</span>
            <span class="tag viz">Animated visualization</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Repeatedly halves the search space. Foundational to B-trees, range queries, and monotonic optimization. Also covers lower bound, upper bound, and binary search on answer patterns.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">5</div>
        <div class="mod-content">
          <div class="mod-title">Linear Search</div>
          <div class="mod-duration">O(n) &middot; Space O(1) &middot; No preconditions</div>
          <div class="mod-tags">
            <span class="tag algo">Sequential scan</span>
            <span class="tag concept">Move-to-front optimization</span>
            <span class="tag viz">Animated visualization</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">The baseline every search algorithm tries to beat. Best for small unsorted data, single searches, and streaming/generators. Includes move-to-front self-organizing variant.</p>
        </div>
      </div>

      <div class="tip-box">Use the Explorer to visually compare how Binary Search eliminates half the array each step, while Linear Search checks every element. Notice the dramatic difference as array size grows.</div>
    </div>

  </div>

  <!-- MODULE C — GRAPH & TREE -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p3')">
      <span class="phase-badge" style="background:#E1F5EE;color:#085041;border:0.5px solid #9FE1CB;">Module C</span>
      <span class="phase-title">Graph &amp; Tree Algorithms</span>
      <span class="phase-meta">3 algorithms</span>
      <span class="chevron" id="p3-chev">▶</span>
    </div>
    <div class="phase-body" id="p3">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#1D9E75;"></div></div>

      <div class="mod-row">
        <div class="mod-num">6</div>
        <div class="mod-content">
          <div class="mod-title">BFS — Breadth-First Search</div>
          <div class="mod-duration">O(V+E) &middot; Space O(V) &middot; Queue-based</div>
          <div class="mod-tags">
            <span class="tag algo">Level-order traversal</span>
            <span class="tag concept">Shortest path (unweighted)</span>
            <span class="tag viz">Tree animation</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Explores level by level using a queue. Finds shortest paths in unweighted graphs. Used in GPS navigation, web crawlers, puzzle solving, and network broadcast.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">7</div>
        <div class="mod-content">
          <div class="mod-title">DFS — Depth-First Search</div>
          <div class="mod-duration">O(V+E) &middot; Space O(V) &middot; Stack/recursion</div>
          <div class="mod-tags">
            <span class="tag algo">Backtracking</span>
            <span class="tag concept">Topological sort</span>
            <span class="tag concept">Cycle detection</span>
            <span class="tag viz">Tree animation</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Explores as deep as possible before backtracking. Space-efficient for deep graphs. Foundational for topological sort, cycle detection, maze generation, and compiler analysis.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">8</div>
        <div class="mod-content">
          <div class="mod-title">Dijkstra's Algorithm</div>
          <div class="mod-duration">O(E log V) &middot; Space O(V) &middot; Priority queue</div>
          <div class="mod-tags">
            <span class="tag algo">Greedy relaxation</span>
            <span class="tag concept">Shortest path (weighted)</span>
            <span class="tag concept">A* foundation</span>
            <span class="tag viz">Tree animation with distances</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Finds shortest paths from a source in weighted graphs with non-negative edges. Powers GPS navigation (Google Maps), internet routing (OSPF), flight optimization, and A* game pathfinding.</p>
        </div>
      </div>

      <div class="tip-box">Watch BFS expand outward ring by ring vs DFS diving deep first. In the Explorer, Dijkstra shows distance labels updating in real-time — key intuition for understanding greedy relaxation.</div>
    </div>

  </div>

  <!-- MODULE D — DYNAMIC PROGRAMMING -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p4')">
      <span class="phase-badge" style="background:#FAEEDA;color:#633806;border:0.5px solid #FAC775;">Module D</span>
      <span class="phase-title">Dynamic Programming</span>
      <span class="phase-meta">2 algorithms</span>
      <span class="chevron" id="p4-chev">▶</span>
    </div>
    <div class="phase-body" id="p4">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#BA7517;"></div></div>

      <div class="mod-row">
        <div class="mod-num">9</div>
        <div class="mod-content">
          <div class="mod-title">LCS — Longest Common Subsequence</div>
          <div class="mod-duration">O(mn) &middot; Space O(mn) &middot; 2D table fill</div>
          <div class="mod-tags">
            <span class="tag algo">Optimal substructure</span>
            <span class="tag concept">Overlapping subproblems</span>
            <span class="tag viz">DP table animation</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Finds the longest sequence present in both strings (not necessarily contiguous). Used in Git diff/patch, DNA sequence alignment, plagiarism detection, and 3-way merge.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">10</div>
        <div class="mod-content">
          <div class="mod-title">0/1 Knapsack</div>
          <div class="mod-duration">O(nW) &middot; Space O(nW) &middot; Binary decisions</div>
          <div class="mod-tags">
            <span class="tag algo">Include/exclude DP</span>
            <span class="tag concept">Budget optimization</span>
            <span class="tag viz">DP table animation</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Given items with weights and values, find the maximum value within a weight capacity. Used in budget allocation, cloud cost optimization, cutting stock problems, and subset-sum variants.</p>
        </div>
      </div>

      <div class="tip-box">The DP table animations are the most illuminating part of the Explorer. Step through cell by cell to see how each value depends on previously computed sub-problems. Pay attention to the space-optimized O(W) rolling-row variant in the code tab.</div>
    </div>

  </div>

  <!-- MODULE E — DATA STRUCTURES -->
  <div class="phase">
    <div class="phase-header" onclick="toggle('p5')">
      <span class="phase-badge" style="background:#FCE4EC;color:#880E4F;border:0.5px solid #F48FB1;">Module E</span>
      <span class="phase-title">Core Data Structures</span>
      <span class="phase-meta">2 structures</span>
      <span class="chevron" id="p5-chev">▶</span>
    </div>
    <div class="phase-body" id="p5">
      <div class="progress-bar"><div class="progress-fill" style="width:100%;background:#C2185B;"></div></div>

      <div class="mod-row">
        <div class="mod-num">11</div>
        <div class="mod-content">
          <div class="mod-title">Linked List</div>
          <div class="mod-duration">O(1) insert/delete at pointer &middot; O(n) access &middot; Space O(n)</div>
          <div class="mod-tags">
            <span class="tag ds">Sequential nodes</span>
            <span class="tag concept">Reversal</span>
            <span class="tag concept">Cycle detection (Floyd's)</span>
            <span class="tag viz">Traversal &amp; reverse animation</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Each node holds data and a pointer to the next. Foundation of stacks, queues, LRU caches, and adjacency lists. Interactive traversal and in-place reversal demo.</p>
        </div>
      </div>

      <div class="mod-row">
        <div class="mod-num">12</div>
        <div class="mod-content">
          <div class="mod-title">Hash Table</div>
          <div class="mod-duration">Amortized O(1) insert/lookup/delete &middot; Space O(n)</div>
          <div class="mod-tags">
            <span class="tag ds">Key-value mapping</span>
            <span class="tag concept">Hash function</span>
            <span class="tag concept">Collision chaining</span>
            <span class="tag viz">Interactive insert &amp; search</span>
          </div>
          <p style="font-size:11px; color:var(--c-text-secondary); margin-top:4px; line-height:1.6;">Maps keys to values via a hash function. The most versatile data structure in production — powers database indexes, distributed caches (Redis), compiler symbol tables, and content-addressable storage (Git).</p>
        </div>
      </div>

      <div class="tip-box">The Hash Table visualizer is interactive — insert your own key-value pairs and watch how the hash function distributes them into buckets. Try inserting keys that collide to see chaining in action.</div>
    </div>

  </div>

  <div style="text-align:center; margin: 20px 0 10px;">
    <a class="explorer-cta" href="/dsa-explorer.html" style="padding:8px 20px; font-size:13px;">▶ Launch DSA Explorer</a>
  </div>

  <div class="study-footer">
    <strong>How to get the most from this track</strong><br>
    Work through each module in order. For every algorithm: (1) watch the animation in Play mode, (2) step through manually to build intuition, (3) study the Complexity tab, (4) read the real-world Use Cases, and (5) study and copy the Python code. After all modules, try implementing each algorithm from memory.
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
