# Day 3 - Database & SQL

Date: 2026-04-28
Duration target: 60-90 minutes
Rule: Study first, AI second. Document first, fix later.

## Day 3 Goal
Understand the N+1 query problem, read EXPLAIN output, and know when to use index types.
Document one slow page in your project without touching code yet.

## Session Plan (Time-boxed)

1. N+1 query study + find one example in mrmax (20 min)
2. Run EXPLAIN on a complex query + understand output (20 min)
3. Index types study (10 min)
4. Document one slow page with all queries it fires (15 min)
5. Reflection (10 min)

---

## 1) N+1 Query Problem

### Definition in your own words:
N+1 query happens when the app first runs 1 query to fetch a list (for example 20 customers), then runs one more query per item (20 more queries) to fetch related data. Total becomes 21 queries instead of 1-2 optimized queries.

### Why is it bad:
It increases DB round trips, slows page response, and becomes much worse when data grows.

### Simple SQL example:

```sql
-- N+1 BAD pattern:
SELECT * FROM posts LIMIT 20;
-- then for each post id, another query:
SELECT * FROM comments WHERE post_id = ?;
```

```sql
-- Better approach with JOIN:
SELECT p.id, p.title, c.id AS comment_id, c.body
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
WHERE p.status = 'published'
ORDER BY p.created_at DESC
LIMIT 20;
```

### Real example from /mrmax project:

Potential N+1 candidate in customer search:

File: src/Eccube/Repository/CustomerRepository.php
```php
->leftJoin('c.Orders', 'o')
->leftJoin('o.OrderItems', 'oi')
```

Why it can become N+1:
- This query itself is not N+1.
- N+1 appears if another layer loops over customers and lazily loads Orders or OrderItems per row.

Good anti-N+1 pattern in category load:

File: src/Eccube/Repository/CategoryRepository.php
```php
->leftJoin('c1.Children', 'c2')
->leftJoin('c2.Children', 'c3')
->leftJoin('c3.Children', 'c4')
->leftJoin('c4.Children', 'c5')
```

Why this is good:
- It preloads tree relations in one query to avoid child-by-child lazy queries.

### N+1 candidate I found myself:

File: src/Eccube/Resource/template/default/Block/category_nav_pc.twig

Code pattern to watch:
- Category loop that reads `Category.children` recursively.

Why it is risky:
- If categories are not preloaded by CategoryRepository::getList(), each recursive children call may trigger extra queries.

---

## 2) EXPLAIN Practice

### What EXPLAIN output columns mean:

| Column | Meaning |
|---|---|
| id | Query step sequence |
| select_type | Query type (SIMPLE, SUBQUERY, etc.) |
| table | Table used in this step |
| type | Access method (`ALL` worst, `ref`/`eq_ref`/`const` better) |
| possible_keys | Candidate indexes |
| key | Actual chosen index |
| key_len | Index bytes used |
| rows | Estimated scanned rows |
| Extra | Extra operations (`Using filesort`, `Using temporary`, `Using index`) |

### Dangerous signs in EXPLAIN:
- `type = ALL` (full table scan)
- `Using filesort`
- `Using temporary`
- very high `rows`

### Query for EXPLAIN (solution query):

```sql
EXPLAIN
SELECT c.id, c.update_date, o.id AS order_id, oi.id AS order_item_id
FROM dtb_customer c
LEFT JOIN dtb_order o ON o.customer_id = c.id
LEFT JOIN dtb_order_item oi ON oi.order_id = o.id
WHERE c.discriminator_type = 'customer'
ORDER BY c.update_date DESC
LIMIT 20;
```

### Example EXPLAIN analysis (template answer):

```
id | select_type | table | type | possible_keys         | key               | rows | Extra
1  | SIMPLE      | c     | ref  | idx_discriminator,... | idx_discriminator | 200  | Using where; Using filesort
1  | SIMPLE      | o     | ref  | idx_customer_id       | idx_customer_id   | 20   |
1  | SIMPLE      | oi    | ref  | idx_order_id          | idx_order_id      | 40   |
```

What I noticed:
- JOIN indexes are used for order and order_item (good).
- If `Using filesort` appears on customer ordering, consider index tuning for filter + sort columns.

### How to run EXPLAIN in project:

```bash
docker ps
docker exec -it <mysql_container_name> mysql -u root -p <database_name>
```

Then run the EXPLAIN query above.

---

## 3) Index Types Study

### B-tree index
- When to use: `=`, `<`, `>`, `BETWEEN`, prefix matches, sorting.
- Best for: general purpose OLTP read queries.
- Example from project: join keys like `o.customer_id`, `oi.order_id` should be B-tree indexed for JOIN performance.

### Hash index
- When to use: exact equality lookup only.
- Best for: key-value style exact match.
- Example note: usually not the main choice in InnoDB app tables; B-tree covers most ecommerce queries.

### Composite index
- When to use: frequent filtering/sorting by multiple columns in fixed order.
- Best for: reducing scans on multi-condition queries.
- Example from customer search pattern:
	- filter: `c.discriminator_type = 'customer'`
	- sort: `ORDER BY c.update_date DESC`
	- candidate composite index: `(discriminator_type, update_date)`

### Index tradeoff rule:

```text
Indexes SPEED UP: SELECT / WHERE / JOIN / ORDER BY
Indexes SLOW DOWN: INSERT / UPDATE / DELETE
```

### My notes after reading:
- Add indexes based on real query patterns, not assumptions.
- Validate with EXPLAIN before and after index changes.

---

## 4) Slow Page Documentation

### Page I chose:
Admin Order List page

### URL or route name:
- Route: `admin_order`
- Controller: `Eccube\Controller\Admin\Order\OrderController::index`

### Queries this page likely fires (first-pass documentation):

1. Search orders with filters and sort (main list query)
2. Join/order status related data
3. Payment-related relation lookups
4. Product stock/status lookups for row display
5. Pagination count query

### How to capture exact query list:

Use Symfony profiler in dev mode and open DB query tab.

Or stream logs:

```bash
docker exec -it <app_container> tail -f var/log/dev.log | grep "SELECT\|INSERT\|UPDATE"
```

### What I noticed:
- Large list pages are the best place to find N+1 and sort/index issues.
- Query count and repeated similar SELECT patterns are key warning signs.

---

## 5) End-of-Day Reflection

Write 3 things I understand better now:
1. N+1 query means query explosion from loops + lazy loading.
2. EXPLAIN tells me whether indexes are used or full scan happens.
3. Composite index should match actual filter and sort order.

Write 2 places I got stuck:
1. Finding the best first query to profile in a large codebase.
2. Mapping ORM joins to raw SQL performance behavior.

Write 1 question for Day 4:
1. In async/background processing, how do I prevent duplicate jobs and race conditions safely?

---

## Day 3 Self-Rating

Rate each area:
- N+1 understanding: Use but cannot explain deeply
- EXPLAIN output reading: Use but cannot explain deeply
- Index types: Use but cannot explain deeply
- Slow page documented: Yes

Confidence score today (0-10): 7

One commitment for Day 4:
I will open one real slow query from profiler and explain its EXPLAIN result in my own words.

---

## Day 3 Completion Checklist

- [x] N+1 definition written in own words
- [x] One real N+1 candidate found in mrmax
- [x] EXPLAIN query prepared for a real project case
- [x] EXPLAIN output analysis template completed
- [x] All 3 index types studied and noted
- [x] One slow page documented
