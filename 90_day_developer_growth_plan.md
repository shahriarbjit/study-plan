# 90-Day Developer Growth Plan
**Full-Stack · AI Skills · Communication · Soft Skills**

> **Who this is for:** A mid-level developer (3–5 years) on an ecommerce team who has been over-relying on AI and wants to rebuild genuine depth across technical, communication, and AI skills.
>
> **How to use with AI:** Share this document with any AI assistant and ask: _"I am on Day X of this plan. Help me study [topic]"_ — the AI will know exactly where you are and what to teach you.

---

## Overview

| Phase | Days | Focus |
|-------|------|-------|
| Phase 1 | Days 1–30 | Foundation — Audit, AI mastery, Communication, Architecture |
| Phase 2 | Days 31–60 | Build — Code quality, DevOps, Problem solving, Side project |
| Phase 3 | Days 61–90 | Lead — System design, Testing, Leadership, Reflection |

**Daily commitment:** 60–90 minutes study + apply in real work  
**Core rule:** Study first, AI second. Never let AI think for you.

---

## PHASE 1 — Days 1–30: Foundation

---

### Week 1 — Knowledge Audit (Days 1–7)
**Focus:** All Skills | **Daily:** 60 min | **Output:** Written gap map

**Goal:** Stop assuming you know things. Map your real knowledge across ALL dimensions — coding, AI usage, communication, architecture, and soft skills.

**Mindset:** Don't ask AI to write anything this week. Use it only at the END of each day to quiz you. Studying first, AI second. Brutal honesty is the foundation.

#### Day 1 — Map what you know, honestly across everything
- List every technical concept you use daily: OOP, APIs, DB, caching, Docker, CI/CD, etc.
- Rate each: "Explain to anyone" / "Use but can't explain" / "Just copy-paste or AI does it" — be brutally honest
- Do the same audit for soft skills: communication, estimation, documentation, presenting ideas
- Audit your AI usage: list every task you delegate to AI — which ones could you do without it?
- Write 5 sentences in your journal: what surprised you most about your own gaps?

#### Day 2 — Core programming concepts (language-agnostic)
- Study OOP principles: interfaces, abstract classes, inheritance, composition — understand WHY, not syntax
- Study data structures: arrays, hash maps, trees, graphs — when to use each
- Find one design pattern in your project codebase — read every line and understand it fully
- Write from memory: implement a simple interface + class. Note where you got stuck.

#### Day 3 — Database & SQL (the most important backend skill)
- Study the N+1 query problem — find one example in your codebase
- Run EXPLAIN on a complex query in your project — understand every output column
- Study index types: B-tree, hash, composite — when they speed up reads vs slow down writes
- Document one slow page in your platform — list all queries it fires (don't fix yet, just document)

#### Day 4 — Async patterns & concurrency (language-agnostic)
- Study async patterns: callbacks, promises, async/await, event loops — understand the concepts behind them
- Learn concurrency vs parallelism — what's the difference? When does each matter?
- Study race conditions — what are they, how do they happen, and how to prevent them
- Find an async function in your codebase with missing error handling — note it

#### Day 5 — Security fundamentals (OWASP Top 10)
- Study OWASP Top 10: SQL injection, XSS, CSRF, broken auth — at a code level
- Find one place in your project where user input is processed — is it properly sanitized?
- Study authentication tokens: Sessions vs JWT vs API keys — tradeoffs of each
- Check: does your platform use prepared statements everywhere? Find one that doesn't.

#### Day 6 — Apply: review your own code with new eyes
- Pick a file you wrote in the last 2 weeks — find 3 things you'd do differently today
- Review one teammate's PR — write 2–3 lines of real, constructive feedback (start this habit daily)
- Try solving a small coding task WITHOUT AI — just you and the docs. Time yourself.

#### Day 7 — Review & build your gap map
- Re-read all 6 days of journal notes
- Write final gap map: 5 technical gaps, 3 AI usage gaps, 3 communication gaps
- Answer: which topics would you struggle to explain to a junior developer? → That becomes your Week 2+ priority.

**Key Resources:**
- OWASP Top 10: https://owasp.org/www-project-top-ten/
- Big-O Cheat Sheet: https://www.bigocheatsheet.com/
- Refactoring Guru — Design Patterns: https://refactoring.guru/design-patterns
- Use The Index, Luke (SQL): https://use-the-index-luke.com/

**Week 1 Outcome:**
- A real, written gap map — technical, AI usage, and soft skills — the foundation of your entire 90 days
- Solid understanding of core CS fundamentals, database optimization, security, and async patterns
- First habit of journaling, code review, and studying without AI

---

### Week 2 — AI Mastery (Days 8–14)
**Focus:** AI · Prompting | **Daily:** 60 min | **Output:** Personal prompt library

**Goal:** AI isn't going away. But using it like a crutch vs using it like a power tool are completely different things. Learn to be 10x more effective WITH AI — not dependent ON it.

**Mindset:** The goal is not to stop using AI. It's to use it so skillfully that you multiply your output while keeping your brain sharp.

#### Day 8 — Prompt engineering fundamentals
- Study prompt engineering basics: role, context, constraints, examples, output format
- Learn zero-shot vs few-shot prompting; chain-of-thought prompting — when to use each
- Take a vague prompt you used recently → rewrite it 3 times, each better than the last
- Compare outputs: how much better is the result with a well-structured prompt?

**Key prompt structure:**
```
Role: You are a [expert role]
Context: [background about the situation]
Task: [exactly what you want]
Constraints: [format, length, style, things to avoid]
Example: [show an example of good output if possible]
```

#### Day 9 — AI for code review, debugging & architecture
- Practice: use AI as a code reviewer — ask for specific feedback on security, performance, naming
- Practice: rubber-duck debugging with AI — describe a bug, let AI ask you clarifying questions
- Practice: ask AI to critique your architecture decisions — "what are the tradeoffs of this approach?"
- Key rule: ALWAYS verify AI output. Find one case today where AI gave you wrong or outdated information.

#### Day 10 — AI-powered development workflows
- Learn GitHub Copilot workflows: tab completion, inline chat, slash commands, agents
- Learn how to write effective `.github/copilot-instructions.md` or system prompts for your projects
- Study Cursor, Windsurf, or other AI coding tools — understand what each does differently
- Create a "prompt library" file — save your best prompts for code review, debugging, test generation, docs

#### Day 11 — AI for non-coding tasks (docs, emails, planning)
- Use AI to draft a technical document — then heavily edit it in YOUR voice. Learn the edit workflow.
- Use AI to break down a large task into subtasks with time estimates — then critique its breakdown
- Practice: use AI to improve a professional email or Slack message — maintain your tone

#### Day 12 — AI ethics, limitations & critical thinking
- Study AI hallucinations — when and why do models generate wrong answers? How to detect them?
- Understand security risks of putting proprietary code into AI tools — what's safe? What isn't?
- Write your personal "AI usage rules" — when you use AI, when you don't, and why

**Personal AI rules template (fill in your own):**
```
I use AI for: [list]
I do NOT use AI for: [list — things that require my own judgment]
I always verify AI output when: [list situations]
I never put into AI: [confidential data, passwords, PII, etc.]
```

#### Day 13 — AI for learning & self-teaching
- Use AI as a teacher: ask it to explain a concept you rated "can't explain" in Day 1 — at 3 different levels
- Use AI to generate quiz questions about topics from Week 1 — test yourself WITHOUT looking at notes
- Practice the Feynman technique with AI: explain a concept to AI, ask it to point out where you're wrong

#### Day 14 — Build your personal AI toolkit
- Finalize your prompt library: 10+ tested prompts for code review, debugging, testing, docs, learning
- Write a 1-page "How I use AI" guide — your personal workflow and rules. Share with your team.
- Reflection: what tasks should you NEVER outsource to AI? Write 5 and explain why.

**Key Resources:**
- OpenAI Prompt Engineering Guide: https://platform.openai.com/docs/guides/prompt-engineering
- Anthropic Prompt Engineering: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering
- GitHub Copilot Docs: https://docs.github.com/en/copilot
- Prompting Guide: https://www.promptingguide.ai/

**Week 2 Outcome:**
- A personal prompt library with 10+ tested, reusable prompts
- Clear understanding of AI strengths, limitations, and security risks
- A personal "AI usage rules" document — you use AI with intention, not habit

---

### Week 3 — Communication & Professional Skills (Days 15–21)
**Focus:** Writing · Speaking | **Daily:** 30 min writing practice | **Output:** 3 documents

**Goal:** Your ideas only have value if others understand them. Writing clearly, speaking up in meetings, and estimating accurately — these are the skills that get developers promoted.

**Mindset:** Communication is engineering too. A developer who can explain things clearly is worth 3 who can't.

#### Day 15 — Technical writing (write for humans, not machines)
- Choose one part of your system a new dev would struggle to understand — write a clear explanation doc
- Include: what it does, why it exists, how it works, and common pitfalls
- Give the doc to a teammate — ask if it makes sense. Revise based on feedback.

**Good technical doc structure:**
```
## What it does (1 sentence)
## Why it exists (problem it solves)
## How it works (step by step)
## Common pitfalls / gotchas
## How to test / verify it works
```

#### Day 16 — English communication (emails, Slack, PR descriptions)
- Study professional email structure: subject, context, ask, close — rewrite 3 of your recent emails
- Write 3 PR descriptions this week that explain: what changed, why, and how to test it
- Practice: summarize a complex technical problem in 3 sentences for a non-technical person

**Good PR description template:**
```
## What changed
[1–2 sentences]

## Why
[The problem this solves / requirement it fulfills]

## How to test
[Steps to verify it works]

## Notes / tradeoffs
[Anything reviewers should know]
```

#### Day 17 — Estimation (the hardest developer skill)
- Study estimation techniques: task decomposition, buffer for unknowns, 3-point estimation (optimistic / realistic / pessimistic)
- Estimate your next 3 real tasks before starting — log predicted vs actual time after
- Reflect: where did you underestimate? Was it technical complexity, unclear requirements, or something else?

#### Day 18 — Speaking up (meetings, standups, presenting ideas)
- Before the next team meeting: prepare one technical observation or alternative approach to share
- Actually say it in the meeting — even just one clear, well-reasoned point
- Practice the SBI framework: Situation → Behavior → Impact — use it to give feedback to a peer
- Journal: how did it feel? What was the reaction? Make it a weekly habit.

#### Day 19 — Write a postmortem (structured problem documentation)
- Choose a bug or outage from the last month — write a structured postmortem
- Structure: what happened, why, how detected, how fixed, how to prevent
- Focus on systems, not blame — a good postmortem never blames individuals

**Postmortem template:**
```
## Incident Summary
## Timeline
## Root Cause
## How It Was Detected
## How It Was Fixed
## Prevention — what changes to process or code will prevent recurrence
```

#### Day 20 — Requirement analysis (ask the right questions)
- Study: analyze vague requirements — ask "what's the user trying to achieve?" not just "what should I build?"
- Take your next task — before coding, write down 5 clarifying questions you should ask
- Practice: convert a vague requirement into a clear user story with acceptance criteria

**User story format:**
```
As a [user type], I want to [action] so that [outcome].

Acceptance criteria:
- [ ] Given [condition], when [action], then [result]
```

#### Day 21 — Phase 1 review (measure your 21-day growth)
- Re-read all journal notes from Weeks 1, 2, and 3
- List 5 specific things you now understand that you didn't 3 weeks ago
- Write: what are the 3 biggest communication improvements you noticed in yourself?

**Key Resources:**
- Google Eng Practices — Code Review: https://google.github.io/eng-practices/review/
- Writing for Developers — FreeCodeCamp: https://www.freecodecamp.org/news/technical-writing-for-developers/
- Postmortem Templates — PagerDuty: https://postmortems.pagerduty.com/

**Week 3 Outcome:**
- A technical doc, a postmortem, and improved PR descriptions — real writing practice
- Estimation log with predicted vs actual times — you'll get better every week
- First experience speaking up in meetings and giving structured feedback

---

### Week 4 — System Thinking & Architecture (Days 22–30)
**Focus:** Architecture · Design | **Daily:** 90 min | **Output:** System architecture diagram

**Goal:** Understand how your own platform is built — and where it would break under pressure. Think architecturally. Most developers never do this — you will.

**Mindset:** Draw before you code. Plan before you implement. This week forces you to think like a senior engineer.

#### Day 22 — Draw your platform's architecture from memory
- On paper: draw how a user request flows through your ecommerce system — server, DB, cache, CDN, etc.
- Ask your team lead or senior dev to correct your diagram — note what you missed
- Identify: where is the single point of failure in your platform right now?

#### Day 23 — Caching, queues & scalability patterns
- Study: Redis cache vs full-page cache vs HTTP cache vs CDN cache — when to use each
- Study message queues: Redis, RabbitMQ, SQS — what problem do they solve?
- If traffic 10x'd tomorrow, what would crash first in your platform? Database? Sessions? File storage?

**Caching decision guide:**
```
HTTP Cache / CDN → for static assets, public pages (no personalization)
Full-page Cache → for pages that rarely change per user
Redis Cache → for computed data: user sessions, query results, rates
Database Cache → last resort; try to cache at a higher layer first
```

#### Day 24 — API design (REST, GraphQL, and beyond)
- Study REST constraints: statelessness, resource naming, HTTP methods, versioning, pagination
- Understand GraphQL basics — when is it better than REST? When is REST simpler?
- Review 3 API endpoints in your project — list any that violate best practices

**REST best practices:**
```
Naming:      /users/{id}/orders (nouns, not verbs)
Methods:     GET (read), POST (create), PUT/PATCH (update), DELETE (remove)
Versioning:  /api/v1/... in URL or Accept header
Pagination:  ?page=1&limit=20 + total_count in response
Status codes: 200/201/204/400/401/403/404/422/500
```

#### Day 25–26 — SOLID principles & design patterns
- Study all 5 SOLID principles — write one code example for each (in any language you use)
- Study key patterns: Repository, Factory, Observer, Strategy — with real ecommerce use cases
- Find a class in your project that violates at least one SOLID principle — document why

**SOLID in plain English:**
```
S — Single Responsibility: one class = one job
O — Open/Closed: extend without modifying existing code
L — Liskov Substitution: subclasses must work wherever the parent works
I — Interface Segregation: don't force classes to implement methods they don't need
D — Dependency Inversion: depend on abstractions (interfaces), not concrete classes
```

#### Day 27–28 — Learn something new (Python or TypeScript intro)
- Pick ONE: Python for scripting/AI/automation OR TypeScript for type safety
- Spend 2 hours learning basics — build one small utility script or tool
- Reflection: what concepts from PHP/JS transfer? What's genuinely different?

#### Day 29–30 — Phase 1 review (measure your 30-day growth)
- Re-do Day 1's knowledge audit — how has your rating changed across ALL dimensions?
- List 5 things you understand now that you didn't 30 days ago — be specific
- Identify your top 3 priorities for Phase 2 — be specific about what you still need to build
- Choose your side project idea for Week 8 — write 3 sentences about what it will be

**Phase 1 Outcome:**
- A real knowledge gap map — technical, AI, and communication — updated with progress
- AI mastery: prompt library, usage rules, and intentional AI workflows
- Communication: technical docs, estimation habits, speaking up in meetings
- Architecture & patterns: system thinking + SOLID + first exposure to a new language

---

## PHASE 2 — Days 31–60: Build

---

### Week 5 — Code Quality & Refactoring (Days 31–37)
**Focus:** Code · Refactoring | **Daily:** 90 min | **Output:** Refactored real module

**Goal:** Write code that your team can maintain, extend, and trust. Refactor something real. Review code like a senior engineer.

**Mindset:** Plan your approach for 10 minutes before opening any file. Write it in plain text. This is your new default way of working.

#### Day 31–32 — Refactor a real module (apply SOLID patterns)
- Choose the messiest module or class in your project that you're responsible for
- Plan the refactor on paper first — what changes, what stays, what are the risks?
- Refactor it applying SOLID — use AI only to review your refactor AFTER you're done

**Refactoring checklist (before you start):**
```
[ ] Do I understand the full behavior of this code?
[ ] Are there existing tests I need to keep passing?
[ ] What's the smallest safe change I can make first?
[ ] Have I planned the rollback if this breaks something?
```

#### Day 33 — Code review mastery (give feedback like a senior)
- Review 2 PRs today — give written feedback with reasons, not just "looks good"
- Write a personal "code review checklist" — 10 things you now look for in every review
- Share your checklist with a teammate — get their additions

**Senior-level code review looks for:**
```
Security: input validation, auth checks, SQL injection risks
Performance: N+1 queries, unnecessary loops, missing indexes
Readability: clear naming, single-purpose functions, no magic numbers
Tests: are edge cases covered? Are failure paths tested?
Design: does this follow existing patterns? Is it too clever?
```

#### Day 34–35 — Performance profiling & optimization
- Profile one slow endpoint in your project — use browser devtools, Xdebug, or APM tools
- Identify the top 3 hotspots — fix the highest-impact one and measure the improvement
- Fix the slow query from Day 3 — measure before/after with EXPLAIN

#### Day 36–37 — Build a small API from scratch (no framework)
- Build a small REST API without any framework — understand what frameworks actually do for you
- Implement: routing, request handling, response formatting, DB layer — from scratch
- Note every time you hit a problem that a framework normally solves — that's framework understanding

**Key Resources:**
- Martin Fowler — Refactoring: https://refactoring.com/
- Clean Code (book) — Robert C. Martin
- PHP Xdebug profiler: https://xdebug.org/docs/profiler

**Week 5 Outcome:**
- One real refactored module in your project — cleaner, more maintainable
- A personal code review checklist and one real performance fix
- A scratch-built API that shows you understand what frameworks abstract

---

### Week 6 — DevOps, Cloud & Deployment (Days 38–44)
**Focus:** DevOps · Cloud | **Daily:** 90 min | **Output:** Dockerized app + CI/CD pipeline

**Goal:** Understand how your code gets to production — Docker, CI/CD, cloud basics, monitoring. A developer who understands deployment is twice as valuable.

**Mindset:** You're not "just a developer." You're an engineer who owns the full lifecycle — from code to production to monitoring.

#### Day 38–39 — Docker (containerize an application)
- Study Docker concepts: images, containers, volumes, networks, multi-stage builds — not just commands
- Write a Dockerfile for your API from Week 5 — build and run it locally
- Add docker-compose.yml: app + DB + Redis — make it run with one command

**Dockerfile best practices:**
```dockerfile
# Use specific version tags, never "latest"
FROM php:8.2-fpm

# Use multi-stage builds for smaller images
# Copy only what's needed
# Run as non-root user
# Use .dockerignore to exclude unnecessary files
```

#### Day 40–41 — CI/CD (automated testing & deployment)
- Create a GitHub Actions workflow: on push to main, run tests and lint
- Ask your DevOps person how your real deployment pipeline works — document it
- What happens when a bad deploy goes out? How do you roll back? Document the answer.

**Basic GitHub Actions workflow structure:**
```yaml
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: composer test
      - name: Lint
        run: composer lint
```

#### Day 42 — Cloud basics (AWS/GCP/Azure fundamentals)
- Study: EC2/VMs, S3/storage, RDS/managed DB, Lambda/serverless — understand the building blocks
- Which cloud services does your platform use? Draw a diagram of the infrastructure.
- Study secrets management: .env vs secret managers vs CI environment variables — what's safe?

**Secrets management rule:**
```
Never commit secrets to git — not even in .env files
Development: .env files (gitignored)
CI/CD: environment variables in the CI platform
Production: AWS Secrets Manager / GCP Secret Manager / Vault
```

#### Day 43–44 — Logging, monitoring & error tracking
- Study: what should you log? What NOT to log? (no PII, no passwords, no tokens)
- Set up Sentry (free tier) on your side project — trigger a test error and see it tracked
- Understand structured logging — why JSON logs are better than plain text in production

**Logging levels guide:**
```
DEBUG   → detailed debugging info (disabled in production)
INFO    → normal operations, user actions
WARNING → something unexpected but not breaking
ERROR   → something broke, needs attention
CRITICAL → system is down or data corruption risk
```

**Key Resources:**
- Docker Getting Started: https://docs.docker.com/get-started/
- GitHub Actions Docs: https://docs.github.com/en/actions
- Sentry (free error tracking): https://sentry.io/

**Week 6 Outcome:**
- A Dockerized application running with docker-compose
- A working CI/CD pipeline on GitHub Actions
- Cloud infrastructure understanding + error monitoring set up

---

### Week 7 — Problem Solving & Critical Thinking (Days 45–51)
**Focus:** Problem Solving | **Daily:** 60 min | **Output:** Technical decision document

**Goal:** Stop jumping to code. Learn to break down problems, think through tradeoffs, debug systematically, and make decisions under uncertainty.

**Mindset:** The best developers don't type faster — they think better. Problem decomposition is the #1 skill AI can't replace.

#### Day 45–46 — Systematic debugging (stop guessing)
- Study: scientific method for debugging — hypothesize, test, eliminate. Never "try random things."
- Learn debugging tools deeply: browser DevTools, Xdebug, log analysis, network tab, profilers
- Find and fix a real bug in your project WITHOUT asking AI — document your debugging process step by step

**Systematic debugging process:**
```
1. Reproduce reliably — if you can't reproduce it, you can't fix it
2. Isolate — narrow down WHERE in the code the problem occurs
3. Form hypothesis — "I think X is happening because Y"
4. Test hypothesis — add logging, use debugger, write a failing test
5. Fix and verify — does the fix actually solve the root cause?
6. Check for regressions — did the fix break anything else?
```

#### Day 47 — Problem decomposition (break big into small)
- Take a large upcoming feature — break it into 10+ small, independent tasks on paper
- For each subtask: what's the input, output, dependencies, and edge cases?
- Practice: explain your decomposition to a teammate. Do they agree? What did you miss?

#### Day 48–49 — Data structures & algorithms (practical patterns)
- Study Big-O notation — understand time/space complexity for common operations
- Solve 5 LeetCode Easy problems in your preferred language — focus on understanding, not speed
- Find one place in your codebase where the algorithm choice matters — could it be more efficient?

**Big-O quick reference:**
```
O(1)      → hash table lookup, array access by index
O(log n)  → binary search, balanced tree operations
O(n)      → linear scan, simple loops
O(n log n)→ efficient sorting (merge sort, quick sort)
O(n²)     → nested loops over same data — usually bad at scale
```

#### Day 50–51 — Decision making (tradeoffs & technical judgment)
- Study: how to evaluate tradeoffs — speed vs quality, build vs buy, simple vs scalable
- Write a decision document for a real technical choice in your project
- Practice: when AI suggests something, ask "why this approach?" and "what are the alternatives?"

**Technical decision document template:**
```
## Problem
[1 paragraph — what problem are we solving?]

## Options Considered
### Option 1: [name]
- Pros: ...
- Cons: ...
- Effort: ...

### Option 2: [name]
- Pros: ...
- Cons: ...
- Effort: ...

## Recommendation
[Which option and why — be specific]

## Risks
[What could go wrong and how we'd handle it]
```

**Key Resources:**
- LeetCode Easy problems: https://leetcode.com/problemset/?difficulty=EASY
- The Pragmatic Programmer (book)
- Big-O Cheat Sheet: https://www.bigocheatsheet.com/

**Week 7 Outcome:**
- Systematic debugging process — no more guessing
- Problem decomposition skill — break anything into manageable parts
- A real technical decision document showing engineering judgment

---

### Week 8 — Side Project v1 (Days 52–60)
**Focus:** Build · Ship | **Daily:** 3–4 hrs | **Output:** Side project on GitHub

**Goal:** Build something real that YOU designed. Plan it yourself — AI can help you debug, not think.

**Mindset:** Use AI to review your plan and debug errors. NEVER use it to generate the initial design or architecture. That part must be yours.

#### Day 52–53 — Design everything before touching code
- Define: what problem does your project solve? Who is the user? What are the core features (max 5)?
- Design the database schema on paper — tables, columns, relationships, indexes
- Design the API: endpoints, request/response shapes, auth strategy — all before coding
- Ask AI to review your design — "what are the weaknesses in this schema?" — then revise

**Side project requirements:**
```
[ ] Solves one real problem clearly
[ ] Max 5 features for v1 — scope it ruthlessly
[ ] Has a data layer (database or API)
[ ] Has some form of auth or user context
[ ] Will be testable (unit + integration tests)
```

#### Day 54–58 — Build the working v1
- Build the core feature first — not a "nice to have", the single most important thing
- Add Docker + CI/CD pipeline (reuse what you built in Week 6)
- Write at least 5 unit tests for core logic — before marking this as "done"
- Add Sentry error monitoring from Day 43

#### Day 59 — Document and share it
- Write a README: what it is, why you built it, how to run it, architecture decisions you made
- Push to GitHub — your first real portfolio piece
- Share with one person — a teammate or developer friend — and get their honest feedback

**Good README structure:**
```markdown
# Project Name
One sentence description.

## Why I built this
## Tech stack
## How to run locally
## Architecture decisions
## What I'd do differently
```

#### Day 60 — Phase 2 review (measure your 60-day growth)
- Re-read all journal notes from Weeks 5, 6, 7, and 8
- List 5 specific skills you improved in Phase 2 — code quality, DevOps, problem solving, building
- Honest reflection: where did you still rely on AI when you shouldn't have? Name it specifically.
- Identify your top 3 focus areas for Phase 3 — be specific about what still needs work

**Phase 2 Outcome:**
- A refactored module + scratch API — you understand code at a deep level
- DevOps skills: Docker, CI/CD, cloud basics, monitoring — all hands-on
- Problem solving: systematic debugging, decomposition, decision documents
- A real side project you designed yourself — on GitHub, documented, tested

---

## PHASE 3 — Days 61–90: Lead

---

### Week 9 — Advanced AI Workflows & System Design (Days 61–67)
**Focus:** AI · System Design | **Daily:** 90 min | **Output:** Technical improvement proposal

**Goal:** Combine AI mastery with system design thinking. Design systems at scale, use AI as a senior design partner, and think about problems AI can't solve for you.

**Mindset:** In Phase 3, you're not just executing — you're thinking about impact, tradeoffs, and the future of your career in an AI-driven world.

#### Day 61–62 — System design exercise: URL shortener
- On paper: design a URL shortener handling 100M URLs and 10M redirects/day — WITHOUT AI first
- Consider: ID generation, storage, caching, redirect latency, analytics, rate limiting
- THEN ask AI to critique your design — find the gaps, revise your approach

**System design framework:**
```
1. Clarify requirements (scale, latency, consistency needs)
2. Estimate scale (requests/sec, storage needs, bandwidth)
3. High-level design (components and how they connect)
4. Deep dive on critical components
5. Identify bottlenecks and tradeoffs
6. Handle failure cases
```

#### Day 63 — AI-assisted architecture (AI as a design partner)
- Use AI to brainstorm architecture alternatives for a notification system — compare 3 approaches
- Practice "adversarial prompting" — ask AI to find flaws in its own suggestions
- Key insight: AI is great at generating options. YOU must make the final decision and own it.

**Advanced prompting techniques:**
```
Adversarial:  "Now argue against the solution you just gave me."
Stress test:  "What would break this at 100x scale?"
Alternative:  "Give me 3 completely different approaches to this problem."
Devil's adv:  "What's the worst case scenario if we go with option 1?"
```

#### Day 64 — System design: your platform's shopping cart
- Design: a cart system handling 1M concurrent users — guest vs logged-in, persistence, merging
- Compare your design to how your actual platform's cart works — what's better? What's worse?

#### Day 65–67 — Write a real improvement proposal
- Identify the most significant technical problem in your platform — write a 1–2 page proposal
- Include: problem, solution, alternatives, risks, effort — use AI to help polish, but YOU own the thinking
- Study: what skills will matter most in 3 years? Where should you invest learning time?
- Share your proposal with your team lead — get real feedback

**Key Resources:**
- System Design Primer: https://github.com/donnemartin/system-design-primer
- Designing Data-Intensive Applications (book) — Martin Kleppmann
- High Scalability blog: http://highscalability.com/

**Week 9 Outcome:**
- 2 system design exercises completed — you can think at scale
- Advanced AI workflow: using AI as a design partner, not a crutch
- A real technical proposal showing engineering judgment

---

### Week 10 — Testing & Reliability (Days 68–74)
**Focus:** Testing · TDD | **Daily:** 90 min | **Output:** Test suite + team testing guide

**Goal:** Code without tests is a house without foundations. Build the habit and understand what to test and why.

**Mindset:** Tests aren't extra work. They're the proof that your code does what you said it does.

#### Day 68–69 — Unit testing (write tests for a core module)
- Study the testing pyramid: unit, integration, e2e — when to use each level
- Write unit tests for a core module in your project — aim for 80% line coverage
- Learn mocking: how to mock database calls so tests don't need a real DB

**Testing pyramid:**
```
         /    e2e    \      ← few, slow, test full user flows
        / integration \     ← some, test component boundaries
       /   unit tests  \    ← many, fast, test pure logic
```

**What to unit test:**
```
✅ Pure functions with clear inputs/outputs
✅ Business logic and calculations
✅ Edge cases and boundary conditions
✅ Error handling paths
❌ Don't test framework internals
❌ Don't test database queries directly (use integration tests)
```

#### Day 70 — Integration testing (test API endpoints end-to-end)
- Write integration tests for 3 API endpoints — test the full request/response cycle
- Test both happy paths AND error paths — invalid input, missing auth, edge cases
- Note: integration tests are slower but catch real wiring bugs that unit tests miss

#### Day 71–72 — TDD practice (write the test first)
- Study TDD cycle: Red → Green → Refactor
- Pick one new small feature for your side project — write the tests BEFORE the implementation
- Journal: how did TDD change how you thought about the design? Honest reaction.

**TDD cycle:**
```
Red:     Write a failing test for the behavior you want
Green:   Write the minimum code to make the test pass
Refactor: Clean up the code — the tests protect you
Repeat
```

#### Day 73–74 — Write a testing guide for your team
- Write a 1-page testing guide: what to test, what not to test, and how to write good test names
- Share with your team — propose adding tests as a PR requirement going forward
- Add your tests to CI so they run on every push — failing tests block the merge

**Good test naming convention:**
```
// Pattern: [what]_[condition]_[expected result]
test_order_total_with_discount_applied_returns_reduced_price()
test_user_login_with_wrong_password_returns_401()
test_cart_add_item_when_out_of_stock_throws_exception()
```

**Key Resources:**
- PHPUnit Docs: https://phpunit.de/documentation.html
- Jest Docs: https://jestjs.io/docs/getting-started
- Martin Fowler on TDD: https://martinfowler.com/bliki/TestDrivenDevelopment.html

**Week 10 Outcome:**
- Unit and integration tests written for real code in your project
- TDD experience — you know when it helps and when it doesn't
- A team testing guide that shows technical leadership

---

### Week 11 — Leadership & Visibility (Days 75–81)
**Focus:** Leadership · Writing | **Daily:** 60 min | **Output:** Published technical post

**Goal:** Technical skill is invisible if no one sees it. Build presence — in your team, in writing, in the developer community.

**Mindset:** Leadership at your level isn't a title. It's being the person others turn to — because you're reliable, clear, and generous with your knowledge.

#### Day 75–76 — Mentor a junior developer
- Choose a concept from your Week 1–8 learning — explain it to a junior dev on your team
- Pair-program with them on a task — observe where they struggle, help without giving answers
- Reflection: teaching something always shows you where YOUR understanding still has holes

**How to mentor without just giving answers:**
```
Instead of: "Here, use this code"
Ask:        "What have you tried so far?"
Ask:        "What do you think the problem is?"
Guide:      "If you look at [this], what does it tell you?"
Teach:      "Let me show you how I'd approach finding this"
```

#### Day 77 — Propose a process improvement
- Identify one process that slows your team down — standups, deployments, code review, planning
- Write a short proposal (calm, reasoned suggestion) and bring it up in a meeting
- Whether accepted or not: being the person who proposes improvements is senior behavior

#### Day 78–79 — Write a public technical post
- Write a short post (300–500 words) on LinkedIn or dev.to about something you learned in these 90 days
- Be honest and specific — "here's what I thought I knew, here's what I learned" resonates well
- Post it — don't wait for it to be perfect. Publishing > perfecting.

**Blog post structure for developers:**
```
Hook:    One sentence that says what changed for you
Before:  What you believed / how you worked before
The turn: What you discovered or learned
After:   How you work now and why it's better
Lesson:  One takeaway the reader can apply today
```

#### Day 80–81 — Side project: add one feature you designed yourself
- Add a meaningful new feature to your Week 8 side project — apply TDD from Week 10
- Update the README and push — your portfolio is growing

**Key Resources:**
- dev.to (developer blogging): https://dev.to/
- The Staff Engineer's Path (book) — Tanya Reilly
- Radical Candor (communication book) — Kim Scott

**Week 11 Outcome:**
- First experience mentoring — you'll find it teaches you as much as it teaches them
- A published technical post — your first public developer presence
- A process improvement proposal — visible leadership in action

---

### Week 12 — Reflect, Measure & Plan Forward (Days 82–90)
**Focus:** Reflection · Planning | **Daily:** 60 min | **Output:** Next 90-day plan

**Goal:** The last week is not a rest week. It's the most important reflection of your career so far. Measure the real change.

**Mindset:** The goal was never to finish 90 days. It was to become the kind of developer who keeps improving because they understand how. Now you do.

#### Day 82–83 — Re-do your original knowledge audit from Day 1
- Re-rate every concept from Day 1 — technical, AI, communication, soft skills — honestly
- Compare Day 1 ratings vs Day 82 ratings — write down exactly what changed
- Identify: what are your remaining top 3 gaps? Those become your next 90-day priorities.

#### Day 84–85 — Write your 90-day retrospective
- What were the 5 biggest things you learned — not topics, but insights about how you work and think
- What habits stuck? What didn't? Why?
- Write honestly: where are you still using AI as a crutch? What's one task you'll commit to doing manually from now on?

**Retrospective template:**
```
## What I'm most proud of
## What surprised me most
## What habits stuck (and which didn't)
## Where AI still does my thinking for me
## My commitment for the next 90 days
```

#### Day 86–87 — Portfolio audit (what did you build?)
- List everything you created in 90 days: code, documents, proposals, posts, tests
- Polish your side project README — make it something you'd be proud to show in an interview
- Update your LinkedIn: add the skills and projects you built. You earned them.

#### Day 88–90 — Plan your next 90 days
- Based on your retrospective: define 3 concrete goals for Days 91–180
- Options: deeper system design, open source contribution, Python/Go/Rust, team lead skills, public speaking, AI agents
- Ask AI to build you a custom plan for your next 90 days based on what you learned here
- Remember: you're no longer a developer who relies on AI to think. You use it to go further. That's the difference.

**Key Resources:**
- The Staff Engineer's Path: https://www.oreilly.com/library/view/the-staff-engineers/9781098118723/
- Developer Roadmaps 2025: https://roadmap.sh/
- Levels.fyi (career growth): https://www.levels.fyi/
- The Pragmatic Programmer: https://pragprog.com/titles/tpp20/

**Final 90-Day Outcome — the full picture:**
- A real, measurable knowledge upgrade across coding, AI skills, communication, system design, and DevOps
- AI mastery: prompt library, usage rules, AI as a design partner — intentional, not dependent
- A side project built and designed by you — tested, dockerized, documented, on GitHub
- Communication portfolio: technical docs, proposals, postmortems, decision documents, blog post
- Team visibility: code reviews, mentoring, process proposals, speaking up in meetings
- Problem-solving skills: systematic debugging, decomposition, critical thinking
- A healthy relationship with AI — as a power tool you use with judgment, not a crutch
- A clear, honest plan for the next 90 days

---

## Quick Reference: Key Topics by Skill Area

### Technical Skills
| Topic | Covered in | Key concept |
|-------|-----------|-------------|
| OOP & design patterns | Week 1, Week 4 | Understand WHY, not just syntax |
| SQL & database optimization | Week 1, Week 5 | N+1, EXPLAIN, indexes |
| API design | Week 4 | REST constraints, versioning, pagination |
| Caching & queues | Week 4 | Redis, CDN, message queues |
| Docker & containers | Week 6 | Images, volumes, docker-compose |
| CI/CD | Week 6 | GitHub Actions, automated testing |
| Cloud basics | Week 6 | AWS/GCP building blocks, secrets |
| Testing | Week 8, Week 10 | Unit, integration, TDD |
| System design | Week 4, Week 9 | Scale, tradeoffs, failure modes |
| Security | Week 1 | OWASP Top 10 |
| Async patterns | Week 1 | Callbacks, promises, concurrency |
| Algorithms | Week 7 | Big-O, practical patterns |
| Performance | Week 5 | Profiling, measurement, optimization |

### AI Skills
| Topic | Covered in | Key concept |
|-------|-----------|-------------|
| Prompt engineering | Week 2 | Role, context, constraints, examples |
| AI for code review | Week 2 | Ask for specific feedback |
| AI for debugging | Week 2 | Rubber-duck, not answer machine |
| AI ethics & limits | Week 2 | Hallucinations, security risks, what not to share |
| AI as design partner | Week 9 | Options from AI, decisions by you |
| Adversarial prompting | Week 9 | Ask AI to challenge its own answers |
| Prompt library | Week 2 | Build and maintain reusable prompts |

### Communication & Soft Skills
| Topic | Covered in | Key concept |
|-------|-----------|-------------|
| Technical writing | Week 3 | Write for humans, not machines |
| PR descriptions | Week 3 | What changed, why, how to test |
| Email & Slack | Week 3 | Subject, context, ask, close |
| Estimation | Week 3 | 3-point estimation, log actual vs predicted |
| Speaking in meetings | Week 3 | Prepare one point, say it |
| Postmortems | Week 3 | Systems not blame, structured format |
| Requirement analysis | Week 3 | Ask "why" before "what" |
| Mentoring | Week 11 | Guide, don't give answers |
| Public writing | Week 11 | 300-500 words, honest, specific |
| Process improvement | Week 11 | Propose calmly, own the outcome |

---

## How to Use This Document with AI

**Starting a study session:**
```
"I'm a PHP/JS/Node.js developer on a 90-day growth plan. I'm currently on Day [X], 
Week [Y] — [topic]. Please teach me [specific concept] from first principles. 
Then give me 3 questions to test my understanding."
```

**Getting a concept explained:**
```
"Explain [concept] at 3 levels: (1) for a complete beginner, (2) for a mid-level developer, 
(3) for a senior developer who wants to understand tradeoffs."
```

**Practicing without AI doing the work:**
```
"I want to learn [topic]. Ask me questions and let me answer. 
Don't give me the answers — point out what's wrong with my answers instead."
```

**Debugging without AI solving it:**
```
"I have a bug: [describe behavior]. Don't tell me the answer. 
Ask me 5 clarifying questions that will help me find the root cause myself."
```

**Architecture review:**
```
"Here is my design for [system]: [describe it]. 
What are the top 3 weaknesses? What would fail first under 10x load?"
```
