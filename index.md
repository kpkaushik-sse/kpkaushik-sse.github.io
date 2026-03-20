---
layout: default
title: Home
---

# Welcome to LearnHub

**Your structured path to mastering modern development.**

Whether you're just starting out or leveling up, LearnHub provides clear, hands-on tutorials organized into focused learning tracks. Build real skills — one lesson at a time.

---

## Featured Learning Tracks

<div class="track-grid">

### Web Development Fundamentals

Master the building blocks of the web — HTML, CSS, and JavaScript from scratch to proficiency.

- 12 lessons &bull; Beginner
- [Start Learning &rarr;](/courses/web-fundamentals/)

---

### JavaScript Deep Dive

Go beyond the basics. Closures, async/await, the event loop, and ES2024 features explained clearly.

- 9 lessons &bull; Intermediate
- [Start Learning &rarr;](/courses/javascript-deep-dive/)

---

### Git & Version Control

Understand Git workflows, branching strategies, pull requests, and collaboration best practices.

- 7 lessons &bull; Beginner
- [Start Learning &rarr;](/courses/git-version-control/)

---

### REST APIs & Backend Basics

Design, build, and consume REST APIs. Learn HTTP, JSON, authentication, and server-side thinking.

- 10 lessons &bull; Intermediate
- [Start Learning &rarr;](/courses/rest-apis/)

</div>

---

## Latest Tutorials

{% for post in site.posts limit:5 %}

- **[{{ post.title }}]({{ post.url | relative_url }})** — <small>{{ post.date | date: "%B %d, %Y" }} &bull; {{ post.categories | join: ", " }}</small>
  {% endfor %}

[View all tutorials &rarr;](/blog/)

---

## How LearnHub Works

1. **Choose a track** — Browse curated learning paths aligned to real-world skills.
2. **Follow the lessons** — Each lesson is short, focused, and includes code examples you can run immediately.
3. **Practice & build** — Every track ends with a mini project to cement your knowledge.
4. **Go further** — Explore the blog for tips, tool reviews, and deep dives on specific topics.

---

## About This Platform

LearnHub is a free, open-source tutorial blog built with Jekyll and hosted on GitHub Pages. Content is written by developers, for developers — practical, no-fluff, and always up to date.

[Learn more about LearnHub &rarr;](/about/)
