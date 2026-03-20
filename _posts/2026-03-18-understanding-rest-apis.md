---
layout: post
title: "Understanding REST APIs"
date: 2026-03-18
categories: [Backend, APIs]
tags: [rest, api, http, backend]
excerpt: "Understand what REST APIs are, how HTTP methods work, status codes, and how to consume an API in JavaScript using fetch()."
---

# Understanding REST APIs

REST (Representational State Transfer) APIs are the backbone of modern web apps. In this lesson you will learn the concepts and build the skills to consume any public API.

---

## What is an API?

An **API** (Application Programming Interface) is a contract between two programs. A REST API uses HTTP to transfer data — typically JSON.

```
Client  ──── HTTP Request ────►  Server
        ◄─── HTTP Response ────  (JSON data)
```

---

## HTTP Methods

| Method   | Action       | Example                 |
| -------- | ------------ | ----------------------- |
| `GET`    | Read data    | Get a list of courses   |
| `POST`   | Create data  | Submit a new post       |
| `PUT`    | Replace data | Update an entire record |
| `PATCH`  | Modify data  | Update one field        |
| `DELETE` | Remove data  | Delete a post           |

---

## HTTP Status Codes

| Code                        | Meaning                       |
| --------------------------- | ----------------------------- |
| `200 OK`                    | Success                       |
| `201 Created`               | Resource created (POST)       |
| `400 Bad Request`           | Client sent invalid data      |
| `401 Unauthorized`          | Authentication required       |
| `403 Forbidden`             | Authenticated but not allowed |
| `404 Not Found`             | Resource does not exist       |
| `500 Internal Server Error` | Server-side problem           |

---

## REST Naming Conventions

```
GET    /courses          → list all courses
POST   /courses          → create a course
GET    /courses/42       → get course with id 42
PUT    /courses/42       → replace course 42
PATCH  /courses/42       → update part of course 42
DELETE /courses/42       → delete course 42
```

---

## Consuming an API with `fetch()`

```js
// GET request
async function fetchCourses() {
  const response = await fetch("https://api.example.com/courses");

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  const courses = await response.json();
  console.log(courses);
}

fetchCourses();
```

### POST request with JSON body

```js
async function createPost(data) {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });

  if (!response.ok) throw new Error(`Failed: ${response.status}`);
  return response.json();
}

createPost({ title: "My Post", body: "Hello!", userId: 1 }).then(console.log);
```

---

## Try It: JSONPlaceholder

[JSONPlaceholder](https://jsonplaceholder.typicode.com) is a free fake REST API for testing.

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then((r) => r.json())
  .then((users) => users.forEach((u) => console.log(u.name)));
```

Paste that into the browser DevTools console and run it right now!

---

## Practice Exercise

1. Fetch the list of posts from `https://jsonplaceholder.typicode.com/posts`
2. Display the `title` of the first 10 posts as `<li>` items in an HTML page
3. Add a button that fetches a single random post (use `Math.random()`) and displays its full content

---

**Previous lesson:** [Git Basics &larr;](/blog/2026/03/14/git-basics-track-your-code-changes/)
