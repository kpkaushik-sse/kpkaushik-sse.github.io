---
layout: post
title: "HTML Basics: Structure Every Web Page Needs"
date: 2026-03-01
categories: [Web Development, HTML]
tags: [html, beginners, web]
excerpt: "Learn the essential HTML elements that form the skeleton of every website — doctype, head, body, headings, paragraphs, links, and images."
---

# HTML Basics: Structure Every Web Page Needs

HTML (HyperText Markup Language) is the foundation of every webpage on the internet. In this lesson you will learn the core elements you need to build any page from scratch.

## What is HTML?

HTML is a **markup language** — it uses tags to describe the structure and meaning of content. Browsers read HTML and render it as visual pages.

---

## The Minimal HTML Document

Every HTML file should start with this structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My First Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is my first webpage.</p>
  </body>
</html>
```

| Tag               | Purpose                         |
| ----------------- | ------------------------------- |
| `<!DOCTYPE html>` | Tells the browser this is HTML5 |
| `<html>`          | Root element of the page        |
| `<head>`          | Metadata (not shown on page)    |
| `<body>`          | Visible content                 |

---

## Headings

Use `<h1>` through `<h6>` for headings. `<h1>` is the most important — use only one per page.

```html
<h1>Page Title</h1>
<h2>Section Heading</h2>
<h3>Subsection</h3>
```

## Paragraphs & Text

```html
<p>This is a paragraph.</p>
<strong>Bold text</strong>
<em>Italic text</em>
```

## Links

```html
<a href="https://example.com">Visit Example</a> <a href="/about">About Page</a>
<!-- relative link -->
```

## Images

```html
<img src="photo.jpg" alt="A description of the photo" width="400" />
```

> Always fill in the `alt` attribute — it improves accessibility and SEO.

---

## Practice Exercise

Create a file called `index.html` with:

- A page title
- A main `<h1>` heading
- Two paragraphs about yourself
- A link to your favourite website
- An image (use any URL from the web)

Open it in your browser — that's a real webpage you just built!

---

**Next lesson:** [CSS Basics: Styling Your First Page &rarr;](/blog/2026/03/05/css-basics-styling-your-first-page/)
