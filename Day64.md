# Day 64 - System Design: Shopping Cart

Date: 2026-07-01
Duration target: 60-90 minutes
Mode: Prefill (fill this before AI review)

## Goal
Design a shopping cart system for an e-commerce platform like mrmax. Handle concurrency and consistency.

## Session Plan

1. Requirements + data model (20 min)
2. Concurrency and consistency design (25 min)
3. Failure modes and recovery (20 min)
4. Reflection (10 min)

---

## 1) Requirements + Data Model

### Functional requirements:
-
-
-

### Cart data model:
```
cart: { user_id, items: [{product_id, quantity, price_at_add_time}], updated_at }
```

### Key question: Where does the cart live? (Session / DB / Redis / hybrid?)

---

## 2) Concurrency Design

### Scenario: two browser tabs, same user, add different items at the same time. What happens?

### How you prevent cart corruption:

### Do you lock, use optimistic concurrency, or last-write-wins? Why?

---

## 3) Failure Modes

### What happens if the user adds an item but the page crashes before save?

### What happens if the stock check passes but the item sells out between check and checkout?

### Your solution for each:

---

## 4) mrmax Connection

### How does mrmax currently handle this?

### One improvement you would make based on today's thinking:

---

## Day 64 Completion Checklist

- [ ] Requirements and data model defined
- [ ] Concurrency strategy chosen with reasoning
- [ ] Failure modes identified and solutions designed
- [ ] Compared to mrmax current implementation
- [ ] Reflection completed
