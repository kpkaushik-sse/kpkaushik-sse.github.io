---
layout: post
title: "Axios Supply Chain Attack – What Happened and How (Explained Simply)"
date: 2026-04-02
categories: [Security, JavaScript]
tags: [axios, npm, supply-chain, security, rat, malware]
excerpt: "A hacker compromised the Axios npm package to secretly install malware on developers' machines. Here's what happened, step by step, in plain English."
---

# Axios Supply Chain Attack – What Happened and How

On March 31, 2026, one of the most popular JavaScript libraries — **Axios** (83 million+ weekly downloads) — was hit by a **supply chain attack**. Two poisoned versions were pushed to npm that secretly installed malware on developers' computers. Here's how it all went down, explained simply.

---

## What Is Axios?

Axios is a JavaScript library that developers use to make HTTP requests (like fetching data from an API). It's used in millions of projects — frontend apps, backend services, mobile apps, you name it.

---

## What Is a Supply Chain Attack?

Imagine you order a sealed bottle of water from a trusted store. But someone at the factory secretly added something harmful before it was sealed. You trust the bottle because the brand is legit — you'd never think to check.

A **supply chain attack** works the same way. Instead of attacking _your_ code, the attacker poisons a **dependency** (a library your code relies on). When you install it, the malicious code runs automatically.

---

## What Exactly Happened?

### Step 1: The Attacker Stole the Maintainer's Account

The main Axios maintainer on npm had a username called **"jasonsaayman"**. The attacker got hold of a **long-lived npm access token** for this account. With that token, they could publish new versions of Axios directly — no password needed, no GitHub review needed.

They even changed the account's email to a Proton Mail address they controlled (`ifstap@proton.me`).

### Step 2: A Fake Dependency Was Planted

Before touching Axios, the attacker created a separate, innocent-looking npm package called **`plain-crypto-js`**.

- **Version 4.2.0** (published March 30, 05:57 UTC) — completely clean, nothing harmful.
- **Version 4.2.1** (published March 30, 23:59 UTC) — the malware payload was added.

This is the "poisoned water" that would later be injected into Axios.

### Step 3: Poisoned Axios Versions Were Published

Using the stolen maintainer account, the attacker published two new Axios versions:

- **axios@1.14.1** (March 31, 00:21 UTC)
- **axios@0.30.4** (March 31, 01:00 UTC)

Both versions added `plain-crypto-js@4.2.1` as a dependency. **No actual Axios source code was changed** — the only difference was one extra line in `package.json` listing this new dependency.

### Step 4: npm's `postinstall` Script Did the Dirty Work

When you run `npm install`, npm can automatically run scripts defined in a package. The `plain-crypto-js` package had a **postinstall script** — a file called `setup.js` that ran immediately after installation.

This script was the **dropper** — it checked which operating system you were running and delivered a matching **Remote Access Trojan (RAT)**:

| OS          | What the Dropper Did                                                                                                             |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **macOS**   | Ran an AppleScript to download a C++ trojan binary, saved it as `/Library/Caches/com.apple.act.mond`, and ran it silently.       |
| **Windows** | Copied PowerShell to `%PROGRAMDATA%\wt.exe` (disguised as Windows Terminal), then fetched and ran a PowerShell RAT via VBScript. |
| **Linux**   | Downloaded a Python RAT script to `/tmp/ld.py` and ran it in the background using `nohup`.                                       |

All three reached out to the same **command-and-control (C2) server** at `sfrclak[.]com` to get their instructions.

### Step 5: The Malware Covered Its Tracks

After deploying the RAT, the dropper cleaned up after itself:

1. Deleted the `postinstall` script.
2. Replaced the `package.json` (that had the malicious hook) with a clean copy (`package.md` was renamed to `package.json`).
3. Deleted the original malicious files.

This meant that if someone inspected their `node_modules` folder _after_ the attack, everything would look normal.

---

## What Could the RAT Do?

Once installed, the RAT would **phone home every 60 seconds** and could:

- Run shell commands on your machine
- List files and directories
- Execute additional malware
- Load DLLs into memory (Windows)
- Exfiltrate data

The **Windows version** was the most persistent — it created a batch file and a Registry Run key so the RAT would restart on every login. The macOS and Linux versions did **not** survive reboots.

---

## How Was It Caught?

Security researchers at **StepSecurity**, **Endor Labs**, **Socket**, **SafeDep**, **Huntress**, and **Elastic Security Labs** all analyzed the attack. Key red flags:

- Axios suddenly had a **new dependency** (`plain-crypto-js`) that was never imported anywhere in its source code.
- The real Axios only has three dependencies: `follow-redirects`, `form-data`, and `proxy-from-env`.
- The new versions were published directly to npm without going through GitHub's CI/CD pipeline.

---

## Who Did This?

The investigation is ongoing, but **Elastic Security Labs** found that the macOS malware had significant overlap with **WAVESHAPER** — a C++ backdoor linked to **UNC1069**, a **North Korean** threat actor previously identified by Google's Mandiant team.

---

## What Should You Do?

If you use Axios in any project, check immediately:

1. **Are you on version 1.14.1 or 0.30.4?** If yes, you were affected.
2. **Downgrade** to `axios@1.14.0` or `axios@0.30.3`.
3. **Remove** `plain-crypto-js` from your `node_modules`.
4. **Check for RAT files**:
   - macOS: `/Library/Caches/com.apple.act.mond`
   - Windows: `%PROGRAMDATA%\wt.exe`
   - Linux: `/tmp/ld.py`
5. If you find any of those files: **assume full compromise**. Rotate all secrets, tokens, passwords, and API keys on that machine.
6. **Block** the domain `sfrclak[.]com` in your network.
7. **Audit** your CI/CD pipelines for any runs that installed the affected versions.

---

## The Big Takeaway

This attack is a textbook example of why **software supply chain security matters**. The attacker didn't change a single line of Axios code. They just added one dependency — and npm's automatic `postinstall` scripts did the rest.

**Tips to protect yourself:**

- **Pin your dependency versions** — don't auto-upgrade to the latest patch.
- **Use lockfiles** (`package-lock.json`) and review changes to them.
- **Disable postinstall scripts** when possible (`npm install --ignore-scripts`).
- **Use tools** like Socket, Snyk, or npm audit to monitor for compromised packages.
- **Enable 2FA** on your npm account — a stolen token shouldn't be enough.

---

_Source: [The Hacker News – Axios Supply Chain Attack Pushes Cross-Platform RAT via Compromised npm Account](https://thehackernews.com/2026/03/axios-supply-chain-attack-pushes-cross.html) (March 31, 2026)_
