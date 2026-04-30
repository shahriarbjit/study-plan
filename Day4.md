# Day 4 - Async Patterns & Concurrency (Language-Agnostic)

Date: 2026-04-29
Duration target: 60-90 minutes
Rule: Study first, AI second
Mode: Solved and completed

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
- Definition in your own words: pass a function into another function so it can run later when work is finished.
- Simple example:
```js
function loadUser(id, callback) {
	db.findUser(id, function (err, user) {
		callback(err, user);
	});
}
```
- When to use: event handlers, old Node-style APIs, simple async flows.
- Risks: callback hell (deep nesting), hard error flow, poor readability.

### Promise/Future
- Definition in your own words: a Promise represents a future result of async work, either fulfilled or rejected.
- Simple example:
```js
fetch('/api/orders')
	.then((res) => res.json())
	.then((data) => console.log(data))
	.catch((err) => console.error(err));
```
- When to use: chaining async steps and centralizing error handling.
- Risks: unhandled rejections, broken chain when return is forgotten.

### Async/Await
- Definition in your own words: cleaner syntax on top of Promise that makes async flow look synchronous.
- Simple example:
```js
async function loadOrders() {
	try {
		const res = await fetch('/api/orders');
		const data = await res.json();
		return data;
	} catch (err) {
		console.error(err);
		return [];
	}
}
```
- When to use: readable multi-step async flows.
- Risks: forgetting try/catch, awaiting sequentially when parallel execution is possible.

### Event Loop
- Definition in your own words: runtime mechanism that executes sync code first, then queued async tasks by priority.
- What runs first: sync code first, then microtasks (Promise callbacks), then macrotasks (setTimeout, I/O callbacks).
- One bug pattern caused by misunderstanding event loop: assuming setTimeout(..., 0) runs before Promise.then, which is false.

---

## 2) Concurrency vs Parallelism

### Concurrency
- Definition in your own words: managing multiple tasks in overlapping time, not necessarily at the same CPU instant.
- Real example from backend: handling many user HTTP requests via non-blocking I/O while a small thread/process pool serves them.

### Parallelism
- Definition in your own words: executing multiple tasks literally at the same time on different CPU cores/workers.
- Real example from backend: multiple queue workers processing emails/payments in parallel.

### Key difference in one sentence:
Concurrency is about task coordination, parallelism is about simultaneous execution.

### When each matters in your current project:
- Concurrency matters when: many customers browse products, update carts, and submit requests at the same time.
- Parallelism matters when: background jobs (mail sending, export, report generation) are processed by multiple workers.

---

## 3) Race Conditions

### What is a race condition?
- A race condition is when the final result depends on unpredictable timing of two or more operations on shared data.

### How race conditions happen (your own words):
- Two requests read the same old value and both update it, causing one update to overwrite the other.

### One practical ecommerce example:
- Product stock is 1. Two users place order at the same moment. Both read stock=1, both reduce it, and both checkout succeed unless locking/transaction logic is used.

### Common prevention strategies
- [x] DB transaction
- [x] Row-level lock (`SELECT ... FOR UPDATE`)
- [x] Optimistic locking/version column
- [x] Idempotency key
- [x] Queue/serialized worker
- [ ] Distributed lock

### Which strategy is most realistic for your project and why?
- Most realistic core strategy: DB transaction + row-level lock for stock/order write path.
- Why: this is reliable with current relational DB flow and does not require extra infrastructure.
- Secondary strategy: idempotency key for payment callback APIs to prevent duplicate charge/order updates.

---

## 4) Project Task - Find Async Error-Handling Gap

Find one async function in your project where error handling is weak/missing.

### File path:
- e:/90days/mrmax/src/Eccube/Resource/template/default/Product/list.twig

### Function name:
- jQuery click handler for `.add-cart` with nested `$.ajax` call for cart block refresh

### Current behavior:
- First AJAX call (add to cart) has `.done`, `.fail`, `.always`.
- Nested AJAX call (GET block_cart) inside `.done` has only `.done` and no `.fail`.

### Missing error handling:
- Missing fail branch for nested cart-block refresh request.
- If refresh request fails, UI can show outdated cart summary without user feedback.

### Potential impact:
- User thinks add-to-cart failed or cart count is wrong.
- Inconsistent UI state and support issues.

### Safer version idea (high level only, no final code required):
- Add `.fail()` to nested AJAX call.
- Show non-blocking message like: "Item added, but cart summary refresh failed."
- Optionally retry refresh once with short backoff.

### Notes from code review:
- This is a real async error-handling gap in production template JS.
- Outer request handles failure, inner request should match same reliability standard.

---

## 5) Hands-On Practice (No AI)

Task:
- Write one small async workflow example in your preferred language.
- Add proper try/catch (or equivalent) and one retry/fallback rule.

Language used: JavaScript

- What I implemented:
- Wrote a small async add-to-cart flow with try/catch equivalent and fallback UI update path.
- Added one retry rule for cart summary refresh when first attempt fails.

- Where I got stuck:
- Deciding whether retry should be immediate or delayed.
- Making sure user does not see duplicate alerts.

- How I solved it:
- Used one retry only and a silent fallback message.
- Kept error surface minimal: one user message, one internal log.

---

## 6) End-of-Day Reflection

Write 3 things I understand better now:
1. Async pattern choice depends on readability and error control.
2. Concurrency and parallelism are related but not the same.
3. Race conditions must be prevented at data-write boundaries, not only in UI logic.

Write 2 places I got stuck:
1. Finding a real async gap in a large codebase quickly.
2. Choosing the best prevention strategy for stock/payment race scenarios.

Write 1 question for Day 5:
1. In EC-CUBE templates and controllers, where is user input most vulnerable to XSS and SQL injection?

---

## Day 4 Self-Rating

Rate each area:
- Async patterns: Use but cannot explain deeply
- Concurrency vs parallelism: Use but cannot explain deeply
- Race condition prevention: Use but cannot explain deeply
- Async error-handling review in real project: Completed

Confidence score today (0-10): 7

One commitment for Day 5:
I will identify one real user-input path and verify sanitization plus prepared statement usage.

---

## Day 4 Completion Checklist

- [x] Callback, promise, async/await, event loop written in own words
- [x] Concurrency vs parallelism comparison completed
- [x] One race condition scenario documented
- [x] One prevention strategy selected for your project
- [x] One real async error-handling gap identified in codebase
- [x] Reflection and self-rating completed
