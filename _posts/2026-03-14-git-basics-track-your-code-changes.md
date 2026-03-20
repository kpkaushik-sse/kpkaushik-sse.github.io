---
layout: post
title: "Git Basics: Track Your Code Changes"
date: 2026-03-14
categories: [Git, Version Control]
tags: [git, beginners, version-control]
excerpt: "Learn Git from scratch — init, add, commit, branch, merge, and push. Includes a cheat-sheet of the most-used commands."
---

# Git Basics: Track Your Code Changes

Git is a version control system that records changes to your files over time. This lesson covers the essential commands you need every day.

---

## Installing Git

Download from [git-scm.com](https://git-scm.com) and verify:

```bash
git --version
# git version 2.44.0
```

Configure your identity (one-time setup):

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
```

---

## Core Workflow

```
Working Directory  →  Staging Area  →  Repository (commits)
       ↑ edit files     git add          git commit
```

```bash
git init                      # create a new repo in current folder
git status                    # see what changed
git add index.html            # stage one file
git add .                     # stage all changes
git commit -m "Add homepage"  # save a snapshot
git log --oneline             # view commit history
```

---

## Branching

Branches let you develop features in isolation without touching the main code.

```bash
git branch feature/nav-bar    # create branch
git switch feature/nav-bar    # switch to it
# (or: git checkout -b feature/nav-bar  — create + switch)

# ... make changes, commit ...

git switch main               # go back to main
git merge feature/nav-bar     # merge changes in
git branch -d feature/nav-bar # clean up
```

---

## Working with GitHub

```bash
git remote add origin https://github.com/user/repo.git
git push -u origin main       # first push (sets upstream)
git push                      # subsequent pushes
git pull                      # fetch + merge latest changes
git clone https://github.com/user/repo.git  # copy a remote repo
```

---

## Essential Cheat-Sheet

| Command               | What it does                    |
| --------------------- | ------------------------------- |
| `git init`            | Initialise a new repo           |
| `git add .`           | Stage all changes               |
| `git commit -m "msg"` | Commit staged changes           |
| `git status`          | Show working tree status        |
| `git log --oneline`   | Compact commit history          |
| `git branch name`     | Create a branch                 |
| `git switch name`     | Checkout a branch               |
| `git merge name`      | Merge branch into current       |
| `git push`            | Upload commits to remote        |
| `git pull`            | Download & merge remote changes |
| `git diff`            | See unstaged changes            |
| `git stash`           | Temporarily shelve changes      |

---

## Practice Exercise

1. Create a new folder and run `git init`
2. Create `index.html` with some content and commit it
3. Create a branch called `feature/about-page`
4. Add an `about.html` file and commit it on that branch
5. Switch back to `main` and merge the feature branch
6. Run `git log --oneline` to verify the merge commit

---

**Next lesson:** [Understanding REST APIs &rarr;](/blog/2026/03/18/understanding-rest-apis/)
