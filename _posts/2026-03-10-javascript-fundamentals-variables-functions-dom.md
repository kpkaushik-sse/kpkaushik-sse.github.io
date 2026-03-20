---
layout: post
title: "JavaScript Fundamentals: Variables, Functions & the DOM"
date: 2026-03-10
categories: [Web Development, JavaScript]
tags: [javascript, beginners, dom]
excerpt: "Get up and running with JavaScript: var/let/const, functions, conditionals, loops, and your first DOM manipulation."
---

# JavaScript Fundamentals: Variables, Functions & the DOM

JavaScript brings interactivity to the web. In this lesson you will learn the core syntax and how to manipulate HTML elements directly from your script.

---

## Variables

```js
// Prefer const by default
const siteName = "LearnHub"; // cannot be reassigned
let lessonCount = 0; // can be reassigned
// Avoid var in modern JS
```

### Data Types

```js
const name = "Alice"; // string
const score = 95; // number
const passed = true; // boolean
const nothing = null; // null
let pending; // undefined
const user = { name, score }; // object
const tags = ["js", "web"]; // array
```

---

## Functions

```js
// Declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Arrow function (preferred for callbacks)
const double = (n) => n * 2;

console.log(greet("Alice")); // Hello, Alice!
console.log(double(5)); // 10
```

---

## Conditionals & Loops

```js
const score = 72;

if (score >= 90) {
  console.log("A");
} else if (score >= 70) {
  console.log("B");
} else {
  console.log("C or below");
}

// for...of loop (arrays)
const lessons = ["HTML", "CSS", "JS"];
for (const lesson of lessons) {
  console.log(lesson);
}
```

---

## DOM Manipulation

The Document Object Model (DOM) lets JavaScript read and change the HTML on a page.

```html
<!-- index.html -->
<h1 id="title">Original Title</h1>
<button id="changeBtn">Change Title</button>

<script>
  const title = document.getElementById("title");
  const changeBtn = document.getElementById("changeBtn");

  changeBtn.addEventListener("click", () => {
    title.textContent = "Title Changed by JavaScript!";
    title.style.color = "#155799";
  });
</script>
```

### Selecting Elements

```js
document.getElementById("myId"); // by ID
document.querySelector(".my-class"); // first match (CSS selector)
document.querySelectorAll("li"); // all matches → NodeList
```

### Modifying Elements

```js
el.textContent = "New text"; // change text
el.innerHTML = "<em>Emphasis</em>"; // change HTML (careful with XSS!)
el.classList.add("active"); // add class
el.classList.remove("hidden"); // remove class
el.setAttribute("href", "/new-page"); // set attribute
```

> **Security note:** Only use `innerHTML` with trusted content. Never insert raw user input into `innerHTML` — it opens an XSS vulnerability. Use `textContent` for user-supplied strings.

---

## Practice Exercise

Build a simple quiz card:

1. Create an HTML page with a question, four option buttons, and a result `<div>`
2. In JS, listen for clicks on each button
3. If the correct option is clicked, show "Correct! ✓" in green
4. Otherwise show "Try again." in red

---

**Previous lesson:** [CSS Basics &larr;](/blog/2026/03/05/css-basics-styling-your-first-page/)  
**Next lesson:** [Git Basics: Track Your Code Changes &rarr;](/blog/2026/03/14/git-basics-track-your-code-changes/)
