# Day 5 - Security Fundamentals (OWASP Top 10)

Date: 2026-05-01
Duration target: 60-90 minutes
Rule: Study first, AI second
Mode: Template only (no pre-solved answers)

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
- What it is (own words):
- Typical vulnerable code pattern:
- Safe pattern:
- One place to check in your project:

### XSS (Cross-Site Scripting)
- What it is (own words):
- Typical vulnerable code pattern:
- Safe pattern:
- One place to check in your project:

### CSRF
- What it is (own words):
- Typical vulnerable code pattern:
- Safe pattern:
- One place to check in your project:

### Broken Authentication
- What it is (own words):
- Typical vulnerable code pattern:
- Safe pattern:
- One place to check in your project:

---

## 2) User Input Audit (From /mrmax)

Find one real flow where user input enters your system.

### File path:

### Endpoint/form route:

### Input fields:

### Validation seen:

### Sanitization/encoding seen:

### Risk level (Low/Medium/High):

### Why:

### Improvement idea:

---

## 3) Token Strategy Study

### Sessions
- Best for:
- Pros:
- Cons:

### JWT
- Best for:
- Pros:
- Cons:

### API Keys
- Best for:
- Pros:
- Cons:

### Decision rule for your project:
- Web user login:
- Internal service-to-service:
- Public API consumer:

---

## 4) Prepared Statements Check

Goal: verify whether SQL queries use parameter binding/prepared statements everywhere.

### Search summary
- Files checked:
- Total risky raw SQL spots found:

### Potential risky examples (if any)
1. File:
   Code:
   Why risky:

2. File:
   Code:
   Why risky:

### Safe examples found
1. File:
   Code:
   Why safe:

2. File:
   Code:
   Why safe:

### Conclusion
- Prepared statements everywhere? Yes/No/Not sure
- If no, top fix priority:

---

## 5) Security Mini Checklist for Daily Work

- [ ] Validate all incoming user input
- [ ] Escape output in templates/views
- [ ] Use CSRF protection for state-changing requests
- [ ] Use parameterized queries/prepared statements
- [ ] Never trust client-side validation alone
- [ ] Log suspicious behavior without logging secrets

---

## 6) End-of-Day Reflection

Write 3 things I understand better now:
1.
2.
3.

Write 2 places I got stuck:
1.
2.

Write 1 question for Day 6:
1.

---

## Day 5 Self-Rating

Rate each area:
- OWASP Top 10 practical understanding: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Input sanitization review skill: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Token strategy decision making: Explain to anyone / Use but cannot explain deeply / Mostly AI-copied
- Prepared statement verification in project: Completed / Not completed

Confidence score today (0-10):

One commitment for Day 6:

---

## Day 5 Completion Checklist

- [ ] SQL injection, XSS, CSRF, broken auth reviewed with examples
- [ ] One real user-input flow audited in /mrmax
- [ ] Sessions vs JWT vs API keys comparison completed
- [ ] Prepared statements checked in real project files
- [ ] Reflection and self-rating completed
