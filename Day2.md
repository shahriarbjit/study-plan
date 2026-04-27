# Day 2 - Core Programming Concepts (Language-Agnostic)

Date: 2026-04-25
Duration target: 60-90 minutes
Rule: Study first, AI second

## Day 2 Goal
Understand OOP fundamentals and practical data structure usage well enough to explain clearly and implement a small example from memory.

## Session Plan (Time-boxed)

1. OOP pillars review (15 min)
2. Composition vs inheritance (20 min)
3. Data structures refresh (20 min)
4. Hands-on coding from memory, no AI (20 min)
5. Reflection and self-rating (10 min)

---

## 1) OOP Pillars Review

### Encapsulation
- Definition in your own words: keep data protected inside a class and control access through methods.
- One real project example:
    - /mrmax/src/Eccube/Controller/Admin/AdminController.php uses class properties and keeps internal state like private `$excludes` inside the class.
    - /mrmax/src/Eccube/Entity/Category.php uses private fields (`$id`, `$name`, `$Children`, `$Parent`) and exposes them via getter/setter methods.

### Abstraction
- Definition in your own words: define what should be done, without forcing callers to know internal details.
- One real project example:
    - /mrmax/src/Eccube/Service/Payment/PaymentMethodInterface.php defines methods like `verify`, `checkout`, `apply`.
    - /mrmax/src/Eccube/Service/Payment/Method/Cash.php provides one concrete implementation.

### Inheritance
- Definition in your own words: child class extends parent class to reuse shared behavior.
- One real project example:
    - /mrmax/src/Eccube/Controller/Admin/Product/CategoryController.php extends `AbstractController`.
    - Many admin/front controllers in EC-CUBE use this same inheritance chain.

### Polymorphism
- Definition in your own words: same interface/contract, different implementations.
- One real project example:
    - /mrmax/src/Eccube/Service/Composer/ComposerServiceInterface.php is implemented by:
        - /mrmax/src/Eccube/Service/Composer/ComposerApiService.php
        - /mrmax/src/Eccube/Service/Composer/ComposerProcessService.php
    - Caller can work with `ComposerServiceInterface` and switch implementation without changing caller logic.

Checkpoint:
- Can I explain all 4 pillars to a junior in simple language? Yes/No

--- Yes

## 2) Composition vs Inheritance
- Composition = has-a relation (inject/use other objects)
- Inheritance = is-a relation (child extends parent)

Write 5 rules for when to prefer composition:
1. When behavior may change often (example: payment methods/processors).
2. When you want to swap implementations without modifying existing code.
3. When a class is getting too big and needs smaller focused collaborators.
4. When you want easier unit testing using mocks/stubs.
5. When inheritance would create a deep/fragile class hierarchy.

Find one place in your project where composition is better than inheritance:
- Current design:
    - /mrmax/src/Eccube/Service/OrderStateMachine.php composes `PointProcessor` and `StockReduceProcessor` through constructor DI.
- Better composition idea:
    - If new business rules come (coupon rollback, loyalty adjust), inject another processor/service instead of creating a new subclass of `OrderStateMachine`.
- Why it is better:
    - Less coupling, easier testing, and safer extension for new behaviors.

---

## 3) Data Structures Refresh

For each structure, write when to use it and one backend use case.

### Array/List
- When to use: ordered collection and iteration.
- Time complexity intuition: access by index O(1), iterate/search O(n), append usually O(1).
- Backend use case:
    - /mrmax/src/Eccube/Controller/CartController.php uses `$Carts` list and loops through cart entries to compute totals.

### Hash Map/Dictionary
- When to use: find value by key
- Time complexity intuition: insert/find by key is average O(1).
- Backend use case:
    - /mrmax/src/Eccube/Controller/CartController.php uses associative arrays keyed by cart key:
        - `$least[$Cart->getCartKey()]`
        - `$quantity[$Cart->getCartKey()]`
        - `$isDeliveryFree[$Cart->getCartKey()]`

### Tree
- When to use: for parent child relationship
- Time complexity intuition: traversal is O(n); lookup depends on indexing/structure.
- Backend use case:
    - /mrmax/src/Eccube/Entity/Category.php has `Parent` and `Children` relations and methods like `getPath()`/`getDescendants()`.
    - /mrmax/src/Eccube/Controller/Admin/Product/CategoryController.php handles category tree navigation by `parent_id`.

### Graph
- When to use: for complex relation
- Time complexity intuition: traversal commonly O(V + E), where V = nodes, E = edges.
- Backend use case:
    - /mrmax/src/Eccube/Service/OrderStateMachine.php models order status transitions (state machine is graph-like workflow).

---

## 4) Hands-On (No AI)

Task:
- Implement one interface
- Implement one class using that interface
- Implement one service with dependency injection

Language used: PHP

What I implemented:
- I traced a real project pattern instead of writing new code yet:
    - Interface: /mrmax/src/Eccube/Service/Composer/ComposerServiceInterface.php
    - Class implementing interface: /mrmax/src/Eccube/Service/Composer/ComposerApiService.php
    - Service with DI in constructor: /mrmax/src/Eccube/Controller/Admin/AdminController.php

Where I got stuck:
- Finding concrete polymorphism and mapping it to my own words.
- Differentiating tree and graph examples in a real ecommerce codebase.

How I solved it (docs/manual thinking only):
- Searched project classes by `implements`, `extends`, and `__construct`.
- Read files and connected concept to code step by step.

---

## 5) End-of-Day Reflection

Write 3 things I understand better now:
1. I understand OOP 4 pillars with real project examples.
2. I understand when to use array/list, map, tree, and graph-style modeling.
3. I can now identify DI and polymorphism in existing production code.

Write 2 places I got stuck:
1. I initially could not find clear project examples for each OOP pillar.
2. I am still not fully confident explaining complexity tradeoffs quickly in interviews.

Write 1 question for Day 3:
1. How do I reliably detect and fix N+1 query problems in my current project?

---

## Day 2 Self-Rating

Rate each area:
- OOP pillars explanation: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
    Use but cannot explain deeply
- Composition vs inheritance decision: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
    Use but cannot explain deeply
- Data structure selection: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
    Use but cannot explain deeply
- Coding from memory: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
    Use but cannot explain deeply

Confidence score today (0-10): 6

One commitment for Day 3: before start day 3 i want to clear day 2

## Day 2 Completion Checklist

- [x] OOP pillars written with project examples
- [x] Composition vs inheritance completed
- [x] Data structures section completed
- [x] Reflection completed
- [ ] Write one small code snippet from memory (interface + implementation + DI) in a scratch file
