# Day 23 - Caching, Queues & Scalability Patterns

Date: 2026-05-21
Duration target: 60-90 minutes
Mode: Prefill (fill this before AI review)

## Goal
Understand and explain caching strategies, message queues, and when to use each scalability pattern.

## Session Plan

1. Study and explain 3 cache invalidation strategies (20 min)
2. Study message queues — when to use async vs sync (20 min)
3. Map scalability patterns to real mrmax scenarios (15 min)
4. Reflection (10 min)

---

## 1) Cache Invalidation Strategies

### TTL (Time-to-live):
- How it works:
- Good for:
- Bad for:

### Event-based invalidation:
- How it works:
- Good for:
- Bad for:

### Cache-aside pattern:
- How it works:
- Good for:
- Bad for:

### Which strategy does mrmax use (or should use)?

---

## 2) Message Queues — Sync vs Async

### When to use synchronous (direct call):
-
-

### When to use async with a queue:
-
-

### Queue concepts to know:
- Dead letter queue:
- At-least-once delivery:
- Idempotency (why it matters for queues):

### One task in mrmax that should probably be async but isn't:

---

## 3) Scalability Patterns Applied to mrmax

| Pattern | What it solves | Does mrmax need this? Why? |
|---|---|---|
| Database read replicas | | |
| Horizontal scaling | | |
| CDN for static assets | | |
| Session storage offload | | |

---

## 4) Reflection

3 things I learned:
1.
2.
3.

---

## Day 23 Completion Checklist

- [ ] 3 cache invalidation strategies explained in own words
- [ ] Sync vs async decision criteria written
- [ ] Scalability patterns mapped to mrmax
- [ ] Reflection completed
