# Day 3 - Database & SQL

Date: 2026-04-28
Duration target: 60-90 minutes
Rule: Study first, AI second. Document first, fix later.

## Day 3 Goal
Understand the N+1 query problem, read EXPLAIN output, and know when to use index types.
Document one slow page in your project without touching any code yet.

## Session Plan (Time-boxed)

1. N+1 query study + find one example in mrmax (20 min)
2. Run EXPLAIN on a complex query + understand output (20 min)
3. Index types study (10 min)
4. Document one slow page with all queries it fires (15 min)
5. Reflection (10 min)

---

## 1) N+1 Query Problem

### Definition in your own words:


### Why is it bad:


### Simple pseudocode example:

```
// N+1 BAD example:
orders = getOrders()           // 1 query
foreach order:
    order.customer = getCustomer(order.id)   // N queries (one per order)
```

```
// Fixed with eager loading:
orders = getOrders().withCustomer()   // 1 query with JOIN
```

### Real example from /mrmax project:

The following queries in your project are potential N+1 risks.

**Risk 1 — CustomerRepository.php (line 288)**

File: `src/Eccube/Repository/CustomerRepository.php`
```php
->leftJoin('c.Orders', 'o')
->leftJoin('o.OrderItems', 'oi')
```
- This joins Orders and OrderItems in the search query.
- Risk: if Orders is lazy-loaded elsewhere in a loop (e.g. admin order list), each order fires a separate query to load items.

**Risk 2 — CategoryRepository.php (lines 77-80)**

File: `src/Eccube/Repository/CategoryRepository.php`
```php
->leftJoin('c1.Children', 'c2')
->leftJoin('c2.Children', 'c3')
->leftJoin('c3.Children', 'c4')
->leftJoin('c4.Children', 'c5')
```
- This pre-joins category children up to 5 levels deep.
- This is actually a GOOD pattern that avoids N+1 by eager loading the tree in one query.
- Without this, each call to `getChildren()` in a template loop would fire a separate query.

Action: Look for templates that call `$Category->getChildren()` inside a loop WITHOUT the repository pre-loading them.
File to check: `src/Eccube/Resource/template/default/Block/category_nav_pc.twig`

### N+1 candidate I found myself:

File:
Code:
Explanation of why this is N+1:

---

## 2) EXPLAIN Practice

### What EXPLAIN output columns mean:

| Column | What it tells you |
|---|---|
| id | Step number in query execution |
| select_type | Type of SELECT (SIMPLE, SUBQUERY, etc.) |
| table | Which table is being accessed |
| type | Join method — `ALL` is worst (full table scan), `ref`/`const` is good |
| possible_keys | Indexes MySQL considered |
| key | Index MySQL actually used |
| key_len | Bytes used from the index |
| rows | Estimated rows MySQL will scan — lower is better |
| Extra | `Using index` = good, `Using filesort` or `Using temporary` = potential problem |

### The most dangerous signs in EXPLAIN output:
- `type = ALL` → full table scan, no index used
- `Extra = Using filesort` → sorting without an index, slow on large tables
- `Extra = Using temporary` → MySQL created a temp table, expensive
- `rows` is very large → MySQL is scanning many rows

### Query I ran EXPLAIN on:

Write the query here:
```sql

```

Paste EXPLAIN output:
```
id | select_type | table | type | possible_keys | key | key_len | rows | Extra
```

What I noticed (is there a full scan? missing index? filesort?):

### How to run EXPLAIN in your project:

Connect to the MySQL container:
```bash
docker exec -it <mysql_container_name> mysql -u root -p <database_name>
```

Then run:
```sql
EXPLAIN SELECT c.*, o.*, oi.*
FROM dtb_customer c
LEFT JOIN dtb_order o ON o.customer_id = c.id
LEFT JOIN dtb_order_item oi ON oi.order_id = o.id
WHERE c.discriminator_type = 'customer'
ORDER BY c.update_date DESC
LIMIT 20;
```

This matches the join pattern in `CustomerRepository.php` line 288.

---

## 3) Index Types Study

### B-tree index
- When to use:
- Best for:
- Example from project:

### Hash index
- When to use:
- Best for:
- Example from project:

### Composite index
- When to use:
- Best for:
- Example from project:

### Index tradeoff rule:
```
Indexes SPEED UP:  SELECT / WHERE / JOIN / ORDER BY
Indexes SLOW DOWN: INSERT / UPDATE / DELETE (because index must be updated)
```

### My notes after reading:

---

## 4) Slow Page Documentation

Choose one page in your EC-CUBE project that you suspect is slow (the admin order list or product list are good candidates).

### Page I chose:


### URL or route name:


### List every query this page fires (check the Symfony profiler or logs):

1.
2.
3.
4.
5.

### How to check all queries fired:

In Symfony/EC-CUBE dev mode, use the web profiler toolbar at the bottom of the page.
Click the database icon to see all queries.

Or check Doctrine logs in `var/log/dev.log`:
```bash
docker exec -it <app_container> tail -f var/log/dev.log | grep "SELECT\|INSERT\|UPDATE"
```

### What I noticed (duplicate queries? suspicious counts?):


---

## 5) End-of-Day Reflection

Write 3 things I understand better now:
1.
2.
3.

Write 2 places I got stuck:
1.
2.

Write 1 question for Day 4:
1.

---

## Day 3 Self-Rating

Rate each area:
- N+1 understanding: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- EXPLAIN output reading: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Index types: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Slow page documented: Yes / No

Confidence score today (0-10):

One commitment for Day 4:

---

## Day 3 Completion Checklist

- [ ] N+1 definition written in own words
- [ ] One real N+1 candidate found in mrmax
- [ ] EXPLAIN run on at least one real query
- [ ] EXPLAIN output analyzed and written down
- [ ] All 3 index types studied and noted
- [ ] One slow page queries documented
