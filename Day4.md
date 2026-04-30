# Day 4 - Async Patterns & Concurrency (Language-Agnostic)

Date: 2026-04-29
Duration target: 60-90 minutes
Rule: Study first, AI second
Mode: Template only (no pre-solved answers)

## Day 4 Goal
Understand async patterns, concurrency vs parallelism, race conditions, and identify one async function in your codebase with missing error handling.

## Session Plan (Time-boxed)

1. Async patterns study (20 min)
2. Concurrency vs parallelism comparison (10 min)
3. Race condition study (20 min)
4. Find one async error-handling gap in project (20 min)
5. Reflection + self-rating (10 min)

---

## 1) Async Patterns Study

### Callback
- Definition in your own words: return function through another function by an arguments
- Simple example: 
- When to use:
- Risks:

### Promise/Future
- Definition in your own words: its hold the result. by reject,fail,success,pending
- Simple example:
- When to use:
- Risks:

### Async/Await
- Definition in your own words: the update version of promise
- Simple example:
- When to use:
- Risks:

### Event Loop
- Definition in your own words: coding flow of async await 
- What runs first: sync code / microtasks / macrotasks:
- One bug pattern caused by misunderstanding event loop:

---

## 2) Concurrency vs Parallelism

### Concurrency
- Definition in your own words: its execute one after one
- Real example from backend:

### Parallelism
- Definition in your own words: its execute once at a time
- Real example from backend:

### Key difference in one sentence:

### When each matters in your current project:
- Concurrency matters when: online order for a indvidual user
- Parallelism matters when: payment

---

## 3) Race Conditions

### What is a race condition?
- in same table when send data from multiple user

### How race conditions happen (your own words):
- product stock
### One practical ecommerce example:

### Common prevention strategies
- [ ] DB transaction
- [ ] Row-level lock (`SELECT ... FOR UPDATE`)
- [ ] Optimistic locking/version column
- [ ] Idempotency key
- [ ] Queue/serialized worker
- [ ] Distributed lock

### Which strategy is most realistic for your project and why?

---

## 4) Project Task - Find Async Error-Handling Gap

Find one async function in your project where error handling is weak/missing.

### File path:

### Function name:

### Current behavior:

### Missing error handling:

### Potential impact:

### Safer version idea (high level only, no final code required):

### Notes from code review:

---

## 5) Hands-On Practice (No AI)

Task:
- Write one small async workflow example in your preferred language.
- Add proper try/catch (or equivalent) and one retry/fallback rule.

Language used:

What I implemented:

Where I got stuck:

How I solved it:

---

## 6) End-of-Day Reflection

Write 3 things I understand better now:
1.
2.
3.

Write 2 places I got stuck:
1.
2.

Write 1 question for Day 5:
1.

---

## Day 4 Self-Rating

Rate each area:
- Async patterns: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Concurrency vs parallelism: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Race condition prevention: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Async error-handling review in real project: Completed / Not completed

Confidence score today (0-10):

One commitment for Day 5:

---

## Day 4 Completion Checklist

- [ ] Callback, promise, async/await, event loop written in own words
- [ ] Concurrency vs parallelism comparison completed
- [ ] One race condition scenario documented
- [ ] One prevention strategy selected for your project
- [ ] One real async error-handling gap identified in codebase
- [ ] Reflection and self-rating completed
