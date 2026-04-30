# Day 5 - Security Fundamentals (OWASP Top 10)

Date: 2026-05-01
Duration target: 60-90 minutes
Rule: Study first, AI second
Mode: Solved and completed

## Day 5 Goal
Build practical security awareness at code level: SQL injection, XSS, CSRF, broken authentication, token tradeoffs, and prepared statement checks in your project.

## Session Plan (Time-boxed)

1. OWASP Top 10 focused study (20 min)
2. Find one user-input flow in project and inspect sanitization (15 min)
3. Compare Sessions vs JWT vs API keys (15 min)
4. Check prepared statements usage in project (20 min)
5. Reflection and action items (10 min)

---

## 1) OWASP Top 10 Focus (Code-Level)

### SQL Injection
- What it is (own words): attacker injects SQL text into input so DB runs unintended query.
- Typical vulnerable code pattern:
   - Building SQL by string concatenation with user input.
   - Example bad idea: SELECT * FROM users WHERE email = '" + email + "'
- Safe pattern:
   - Use prepared statements with placeholders and bound parameters.
- One place to check in your project:
   - e:/90days/mrmax/src/Eccube/Controller/Install/InstallController.php
   - This file shows safe prepared usage with placeholders and execute array.

### XSS (Cross-Site Scripting)
- What it is (own words): attacker injects script/HTML that runs in another user's browser.
- Typical vulnerable code pattern:
   - Rendering untrusted DB text with raw output in templates.
- Safe pattern:
   - Default escaping in Twig, sanitize rich text before storage/output, avoid raw unless trusted.
- One place to check in your project:
   - e:/90days/mrmax/src/Eccube/Resource/template/default/Product/list.twig
   - e:/90days/mrmax/src/Eccube/Resource/template/default/Block/news.twig
   - Both render description with raw filter, so source data trust matters.

### CSRF
- What it is (own words): attacker tricks logged-in user browser to send unwanted state-changing request.
- Typical vulnerable code pattern:
   - POST/DELETE action without CSRF token validation.
- Safe pattern:
   - Validate token for every state-changing action.
- One place to check in your project:
   - e:/90days/mrmax/src/Eccube/Controller/AbstractController.php
   - isTokenValid checks token from request/header and throws on invalid token.

### Broken Authentication
- What it is (own words): weak login/session handling that allows account takeover.
- Typical vulnerable code pattern:
   - Weak password policy, no rate limit, poor session/token handling.
- Safe pattern:
   - Strong password hashing, MFA where needed, secure session controls, login throttling.
- One place to check in your project:
   - e:/90days/mrmax/src/Eccube/Form/Type/Admin/LoginType.php
   - Admin login form has csrf_protection false at form type level, so authentication flow must rely on framework-level security checks and route protections.

---

## 2) User Input Audit (From /mrmax)

Find one real flow where user input enters your system.

### File path:
- e:/90days/mrmax/src/Eccube/Controller/ContactController.php
- e:/90days/mrmax/src/Eccube/Form/Type/Front/ContactType.php

### Endpoint/form route:
- /contact

### Input fields:
- name, kana, postal_code, address, phone_number, email, contents

### Validation seen:
- NotBlank on email and contents
- Email validation with strict mode option
- Structured field types for address/name/phone/postal

### Sanitization/encoding seen:
- Input sanitization helper exists:
   - e:/90days/mrmax/src/Eccube/Form/EventListener/HTMLPurifierListener.php
   - Replaces < > & in submitted data
- Output encoding: Twig auto-escapes by default unless raw is used.

### Risk level (Low/Medium/High):
- Medium

### Why:
- Validation is present and helpful.
- But raw output exists in some templates, so data trust boundary must be controlled.

### Improvement idea:
- Apply strict sanitize policy for fields that can contain free text.
- Review every raw usage and keep only trusted/admin-curated content in raw output.
- Add centralized review checklist for raw usage in Twig.

---

## 3) Token Strategy Study

### Sessions
- Best for: browser web login and server-rendered app flows.
- Pros: simple revoke/logout control, server-side authority, mature security controls.
- Cons: server memory/storage dependency, scaling needs shared session store.

### JWT
- Best for: stateless APIs and mobile clients.
- Pros: no server session lookup needed, easy cross-service propagation.
- Cons: revocation is harder, short-expiry + rotation design needed.

### API Keys
- Best for: server-to-server integration and fixed partner APIs.
- Pros: simple to implement and rotate.
- Cons: coarse access control if not scoped, key leakage risk.

### Decision rule for your project:
- Web user login:
   - Session (best default for EC-CUBE web flow)
- Internal service-to-service:
   - API key or signed token with strict scope and rotation
- Public API consumer:
   - JWT (short expiry) or scoped API key depending on API style

---

## 4) Prepared Statements Check

Goal: verify whether SQL queries use parameter binding/prepared statements everywhere.

### Search summary
- Files checked:
  - e:/90days/mrmax/src/Eccube/Controller/Install/InstallController.php
  - e:/90days/mrmax/src/Eccube/DependencyInjection/EccubeExtension.php
  - e:/90days/mrmax/src/Eccube/Doctrine/Common/CsvDataFixtures/CsvFixture.php
- Total risky raw SQL spots found:
  - 1 medium-risk candidate for review

### Potential risky examples (if any)
1. File:
   - e:/90days/mrmax/src/Eccube/Doctrine/Common/CsvDataFixtures/CsvFixture.php
   Code:
   - SQL built from table/column names (from CSV metadata) before prepare
   Why risky:
   - Values are bound safely, but dynamic identifiers should come from trusted source only.

2. File:
   - e:/90days/mrmax/src/Eccube/DependencyInjection/EccubeExtension.php
   Code:
   - conn->query('select * from dtb_plugin')
   Why risky:
   - Not user input driven, so low practical risk; still a raw query style.

### Safe examples found
1. File:
   - e:/90days/mrmax/src/Eccube/Controller/Install/InstallController.php
   Code:
   - prepare('SELECT id FROM dtb_member WHERE login_id = :login_id') and execute bound params
   Why safe:
   - Uses placeholder and parameter binding.

2. File:
   - e:/90days/mrmax/src/Eccube/Doctrine/Common/CsvDataFixtures/CsvFixture.php
   Code:
   - prepare($sql) then bindValue for each value
   Why safe:
   - Value injection risk reduced via binding.

### Conclusion
- Prepared statements everywhere? Yes/No/Not sure
  - Not sure (mostly good usage found, but dynamic SQL identifier path needs careful trust control)
- If no, top fix priority:
  - Add whitelist validation for dynamic table/column names in CSV import pipeline.

---

## 5) Security Mini Checklist for Daily Work

- [x] Validate all incoming user input
- [x] Escape output in templates/views
- [x] Use CSRF protection for state-changing requests
- [x] Use parameterized queries/prepared statements
- [x] Never trust client-side validation alone
- [x] Log suspicious behavior without logging secrets

---

## 6) End-of-Day Reflection

Write 3 things I understand better now:
1. SQL safety is mostly about parameter binding and trusted query structure.
2. Raw template output is powerful but must be tightly controlled.
3. CSRF protection should be mandatory for state-changing requests.

Write 2 places I got stuck:
1. Distinguishing low-risk internal raw query from real injection risk.
2. Deciding when raw output is acceptable in Twig.

Write 1 question for Day 6:
1. When reviewing my own file, how do I prioritize what to refactor first?

---

## Day 5 Self-Rating

Rate each area:
- OWASP Top 10 practical understanding: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
   - Use but cannot explain deeply
- Input sanitization review skill: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
   - Use but cannot explain deeply
- Token strategy decision making: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
   - Use but cannot explain deeply
- Prepared statement verification in project: Completed / Not completed
   - Completed

Confidence score today (0-10):
   - 7

One commitment for Day 6:
   - I will review one file I wrote recently and identify 3 concrete improvements with reasons.

---

## Day 5 Completion Checklist

- [x] SQL injection, XSS, CSRF, broken auth reviewed with examples
- [x] One real user-input flow audited in /mrmax
- [x] Sessions vs JWT vs API keys comparison completed
- [x] Prepared statements checked in real project files
- [x] Reflection and self-rating completed
