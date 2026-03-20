---
layout: post
title: "CSS Basics: Styling Your First Page"
date: 2026-03-05
categories: [Web Development, CSS]
tags: [css, beginners, web]
excerpt: "Add colour, typography, spacing, and layout to your HTML using CSS. Covers selectors, the box model, and Flexbox fundamentals."
---

# CSS Basics: Styling Your First Page

CSS (Cascading Style Sheets) controls how HTML elements look. In this lesson we cover selectors, properties, the box model, and a first look at Flexbox.

---

## Linking CSS to HTML

You can write CSS three ways. **External stylesheet** (recommended):

```html
<!-- In <head> -->
<link rel="stylesheet" href="styles.css" />
```

---

## Selectors

```css
/* Element selector */
p {
  color: #333;
}

/* Class selector */
.highlight {
  background-color: yellow;
}

/* ID selector */
#hero {
  font-size: 2rem;
}

/* Descendant */
nav a {
  text-decoration: none;
}
```

---

## Common Properties

```css
body {
  font-family: "Segoe UI", sans-serif;
  background-color: #f5f5f5;
  color: #222;
  margin: 0;
  padding: 0;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #155799; /* Architect theme blue */
}

a {
  color: #155799;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
```

---

## The Box Model

Every element is a box:

```
┌──────────────────────┐
│        margin        │
│  ┌────────────────┐  │
│  │    border      │  │
│  │  ┌──────────┐  │  │
│  │  │ padding  │  │  │
│  │  │ content  │  │  │
│  │  └──────────┘  │  │
│  └────────────────┘  │
└──────────────────────┘
```

```css
.card {
  width: 300px;
  padding: 1rem;
  border: 1px solid #ddd;
  margin: 1rem;
  box-sizing: border-box; /* padding included in width */
}
```

---

## Flexbox Quickstart

Flexbox makes layout much easier:

```css
.container {
  display: flex;
  gap: 1rem;
  justify-content: space-between; /* main axis */
  align-items: center; /* cross axis */
  flex-wrap: wrap;
}
```

```html
<div class="container">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
</div>
```

---

## Practice Exercise

Style the HTML page you built in the previous lesson:

1. Set a background colour and a readable font on `body`
2. Give your `<h1>` a different colour and larger size
3. Add padding and a border to one element
4. Create a two-column layout using Flexbox

---

**Previous lesson:** [HTML Basics &larr;](/blog/2026/03/01/html-basics-structure-every-web-page-needs/)  
**Next lesson:** [JavaScript Fundamentals: Variables, Functions & DOM &rarr;](/blog/2026/03/10/javascript-fundamentals-variables-functions-dom/)
