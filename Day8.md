# Day 8 - Prompt Engineering Fundamentals

Date: 2026-05-06
Duration target: 60-90 minutes
Rule: Study the theory first without AI — then use AI to test and compare prompts
Mode: Solved and completed

## Day 8 Goal
Week 2 starts. Learn prompt engineering fundamentals so you can get 10x better output from AI — not just "ask and accept" but "design and verify."

## Session Plan (Time-boxed)

1. Study prompt structure theory (15 min — no AI)
2. Write definitions in your own words (10 min)
3. Pick one real vague prompt you used recently and rewrite it 3 times (25 min)
4. Compare the 3 outputs (10 min)
5. Reflection and self-rating (10 min)

---

## 1) Core Concepts — Write in Your Own Words

Study these 5 concepts, then write a 1-2 sentence definition in your own words without looking.

### Role
- What it is (own words): Role tells the AI what kind of expert it should act as. It sets the persona so the AI answers from that person's experience and knowledge level.
- Why it matters in a prompt: Without a role, AI gives a generic answer. With "Act as a senior PHP backend engineer," it uses language, patterns, and assumptions that match that expertise — more specific, more useful output.

### Context
- What it is (own words): Context is the background information AI needs to understand your situation — the project, the problem, what already exists, what you already tried.
- Why it matters in a prompt: Without context, AI makes assumptions that may be wrong. "I have a Symfony 4.4 project with 50k daily API calls" immediately tells AI which framework version, scale, and constraints apply — so it stops suggesting things that do not fit.

### Constraints
- What it is (own words): Constraints tell AI what NOT to do, what format to use, how long the answer should be, or what assumptions to avoid.
- Example of a useful constraint: "Reply with code only, no explanation. Use PHP 7.4 syntax. Do not add new dependencies." This prevents AI from adding a 200-line essay when you only need a function.

### Zero-shot prompting
- What it is (own words): Zero-shot means you give AI a task with NO examples — just the instruction. You rely entirely on AI's pre-trained knowledge to figure out the format and style.
- When to use it (vs few-shot): Use zero-shot for simple, clear tasks where the expected output format is obvious (e.g., "Explain what CSRF is in 2 sentences"). Use few-shot instead when the output format is non-standard or when AI keeps misunderstanding what you want.

### Few-shot prompting
- What it is (own words): Few-shot means you give AI 1-3 examples of input → output pairs inside the prompt itself, so AI learns the exact pattern and format you want from the examples.
- When to use it (vs zero-shot): Use few-shot when zero-shot gives you the wrong format or style. Example: if you want commit messages in a specific format like "[BUGFIX] Short title — Body detail", show 2 examples and AI will follow that pattern consistently.

### Chain-of-thought prompting
- What it is (own words): Chain-of-thought prompting asks AI to reason step by step before giving the final answer, by adding phrases like "think step by step" or "explain your reasoning first." This forces AI to show its logic, which catches mistakes and gives more accurate answers for complex problems.
- When to use it: Use for complex reasoning tasks — debugging a tricky bug, comparing architecture choices, explaining WHY a security vulnerability exists. For simple factual questions, chain-of-thought is overkill.

---

## 2) The Standard Prompt Structure

Write the 5-part prompt structure template in your own words (do not copy — reconstruct from memory after studying):

```
1. Role:       Act as a senior PHP backend engineer with Symfony experience.
2. Context:    I am building a REST API for a Japanese e-commerce platform (EC-CUBE/Symfony 4.4).
               The CouponController already exists. I need a new GET endpoint to list all active coupons.
3. Task:       Write a paginated GET /api/v1/coupons endpoint. Return JSON with items array and pagination meta (total, page, per_page).
4. Constraints: PHP 7.4 syntax only. No new Composer dependencies. Follow existing AbstractController patterns in the codebase. Code only — no explanation unless I ask.
5. Example:    Expected response format:
               { "items": [...], "meta": { "total": 100, "page": 1, "per_page": 20 } }
```

---

## 3) Rewrite a Real Prompt — 3 Versions

Pick one real prompt you have used recently at work or during Week 1.
It should be a vague one — something that got a mediocre or generic result.

### Original vague prompt (paste it here):
```
why is my coupon api slow
```
(This is the kind of prompt I would have typed during a production incident — pasted the question with no code, no context, no numbers. I would have gotten a generic answer listing 10 possible causes with no relevance to my actual code.)

### Why this prompt is weak (1-2 sentences):
No role, no context about the framework or code, no data about how slow or when, no specific question. AI cannot know whether this is a PHP performance issue, an N+1 query, a network problem, or a locking issue — so it gives a useless generic list of possibilities.

---

### Rewrite Version 1 — Add Role and Context only
```
You are a senior PHP backend engineer experienced with Symfony and high-traffic APIs.

I have a POST endpoint at /api/v1/pos/coupon in a Symfony 4.4 application. It receives POS machine requests
(50,000+ per day) and calls CouponService::useCouponWithProcessingTimeValidation(). Response times have
increased from ~80ms to ~400ms over the past week with no code changes.

Why might this endpoint be getting slower, and what should I investigate first?
```

**What you expect to be better:**
AI now knows: Symfony 4.4 (not Laravel, not Node), specific endpoint, specific service method name, real traffic volume, and the symptom (gradual slowdown with no code change). It can now answer specifically — likely suspects: database query plans, index degradation, external service timeout, connection pool exhaustion. Far more targeted than the original.

---

### Rewrite Version 2 — Add Constraints (format, length, what to avoid)
```
You are a senior PHP backend engineer experienced with Symfony and high-traffic APIs.

I have a POST endpoint at /api/v1/pos/coupon in a Symfony 4.4 application. It receives POS machine requests
(50,000+ per day) and calls CouponService::useCouponWithProcessingTimeValidation(). Response times have
increased from ~80ms to ~400ms over the past week with no code changes.

Why might this endpoint be getting slower, and what should I investigate first?

Constraints:
- List only the top 3 most likely causes ranked by probability
- For each cause: give one specific thing to check (a command, a query, or a log to look at)
- Do NOT suggest rewriting the architecture or adding caching unless I ask
- Reply in bullet points, max 150 words total
```

**What you expect to be better:**
Output is now focused and actionable — 3 ranked causes with concrete next steps, not a 500-word essay. The constraint "do NOT suggest rewriting the architecture" stops AI from proposing a Redis cache overhaul when I only want to understand the current degradation.

---

### Rewrite Version 3 — Add an Example of the output you want
```
You are a senior PHP backend engineer experienced with Symfony and high-traffic APIs.

I have a POST endpoint at /api/v1/pos/coupon in a Symfony 4.4 application. It receives POS machine requests
(50,000+ per day) and calls CouponService::useCouponWithProcessingTimeValidation(). Response times have
increased from ~80ms to ~400ms over the past week with no code changes.

Why might this endpoint be getting slower, and what should I investigate first?

Constraints:
- List only the top 3 most likely causes ranked by probability
- For each cause: give one specific thing to check
- Do NOT suggest architecture rewrites
- Reply in this format:

**#1 [Cause name] — Probability: High**
What to check: [specific command or query]

**#2 [Cause name] — Probability: Medium**
What to check: [specific command or query]

**#3 [Cause name] — Probability: Low**
What to check: [specific command or query]
```

**What you expect to be better:**
AI now has a rigid output template — the format example removes all ambiguity about how to structure the answer. AI cannot decide to put everything in a paragraph or add 5 extra causes. The output is copy-pasteable into a Slack message or incident report immediately.

---

## 4) Output Comparison

Run all 3 versions in your AI tool and compare results.

### Version 1 result (short summary):
AI gave a relevant, specific list: N+1 query in CouponService, database lock contention from concurrent coupon updates, and slow external service calls. Already 10x better than the vague prompt — named the actual service and gave Symfony-specific suggestions like checking the Doctrine profiler and slow query log.

### Version 2 result (short summary):
Output was structured into exactly 3 ranked causes with a concrete check command for each. Example: "#1 Database query slowdown — run EXPLAIN on the coupon status UPDATE query, check if index on coupon_code column is still used." No architecture suggestions appeared at all. Much more useful during an actual incident.

### Version 3 result (short summary):
Output matched the exact template — 3 entries with probability label and "What to check" line. Output was ready to paste into Slack. The format example was the single biggest quality jump — AI stopped adding context paragraphs and just gave me the table I asked for.

### Which version gave the best output, and why?
**Version 3** — The example output format was the highest-leverage addition. Role + Context (V1) told AI WHAT I needed. Constraints (V2) told AI what to AVOID. The example format (V3) told AI exactly HOW to structure the answer. All three layers compound — each one removes a different type of ambiguity.

### One thing that surprised you about how the output changed:
Adding the example format in Version 3 eliminated all the "let me explain what I mean by..." preamble that AI added in Versions 1 and 2. I did not expect format examples to have that much impact on removing filler text. The constraint "do NOT suggest architecture rewrites" in Version 2 worked perfectly — AI never mentioned Redis or caching once.


---

## 5) Prompt Library — First Entry

Start your personal prompt library today. Based on today's rewriting exercise, save one tested, working prompt for future reuse.

### Prompt name / use case: API performance investigation — "why is X slow"

### Final prompt text:
```
You are a senior [LANGUAGE] backend engineer experienced with [FRAMEWORK] and high-traffic APIs.

I have a [HTTP_METHOD] endpoint at [ENDPOINT_PATH] in a [FRAMEWORK VERSION] application.
It receives [TRAFFIC_VOLUME] per day and calls [SERVICE_CLASS]::[METHOD_NAME]().
[DESCRIBE THE SYMPTOM: response times, error rate, etc.]

Why might this be happening, and what should I investigate first?

Constraints:
- List only the top 3 most likely causes ranked by probability
- For each cause: give one specific thing to check (a command, a query, or a log)
- Do NOT suggest architecture rewrites or new dependencies unless I ask
- Reply in this format:

**#1 [Cause name] — Probability: High**
What to check: [specific command or query]

**#2 [Cause name] — Probability: Medium**
What to check: [specific command or query]

**#3 [Cause name] — Probability: Low**
What to check: [specific command or query]
```

### What it is good for:
Fast triage during production incidents or performance investigations. Gives ranked, actionable next steps in a format ready to paste into Slack or an incident report. Works for any language/framework — just fill in the placeholders.

### What to watch out for (known limitations):
- AI does not know your actual query plans or execution times — it is guessing from context. Always verify the top cause with real data (EXPLAIN query, actual log timestamps) before acting.
- If the symptom is very unusual (e.g., slowdown only on specific member IDs), the top causes AI suggests may all be wrong. Add the unusual pattern as context.
- Do not paste actual production data, real member IDs, or real API keys into the prompt.

---

## 6) End-of-Day Reflection

Write 3 things I learned today:
1. Zero-shot, few-shot, and chain-of-thought are not about how many words are in the prompt — they are about how much pattern guidance you give. Zero-shot = no examples, trust AI's training. Few-shot = show the pattern via examples. Chain-of-thought = force visible reasoning before the final answer.
2. The output format example (Version 3) was the single highest-leverage change in the rewriting exercise. I expected Role and Context to matter most — they helped a lot, but the format template removed filler text and preamble in a way that constraints alone could not.
3. A real vague prompt ("why is my coupon api slow") is dangerous not because it gets no answer — it gets an answer, which looks reasonable, and you act on it without realising it is generic advice not tailored to your actual code. The risk is confidence in a mediocre output.

Write 1 thing I want to test tomorrow with AI:
Use AI as a code reviewer on PosController.php — but with a structured prompt that specifies which dimensions to review (security, naming, error handling) rather than just "review this code." Compare structured vs unstructured code review prompts.

---

## Day 8 Self-Rating

Rate each area (Explain to anyone / Use but cannot explain deeply / Mostly AI-copied):
- Zero-shot vs few-shot vs chain-of-thought: **Explain to anyone** — the definitions were wrong at the start of the day (zero-shot is NOT "one word prompts"). Now I can state each one clearly in 2 sentences.
- Prompt structure (Role/Context/Task/Constraints/Example): **Explain to anyone** — I can write each layer, name it, and explain why it improves output.
- Ability to diagnose a weak prompt and improve it: **Use but cannot explain deeply** — I can improve a vague prompt when I sit down and think carefully. But in the middle of an incident I would still probably write a vague prompt under pressure. Need more reps.

Confidence score today (0-10): **8**

One commitment for Day 9: When asking AI to review code tomorrow, write the prompt using today's structure first — Role, Context, Task, Constraints, Example — before hitting send. No more "review this code" as a full prompt.

---

## Day 8 Completion Checklist

- [x] Core concepts defined in own words (no copy-paste)
- [x] 5-part prompt structure written from memory
- [x] One real vague prompt identified
- [x] Prompt rewritten 3 times with each improvement named
- [x] All 3 versions tested and output compared
- [x] First prompt library entry saved
- [x] Reflection completed
