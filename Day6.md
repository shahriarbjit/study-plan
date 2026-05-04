# Day 6 - Apply: Review Your Own Code With New Eyes

Date: 2026-05-04
Duration target: 60-90 minutes
Rule: No AI while doing the core exercises
Mode: Solved and completed

## Day 6 Goal
Practice practical engineering judgment by reviewing your own recent code, writing constructive PR feedback, and solving one small coding task without AI.

## Session Plan (Time-boxed)

1. Review one file you wrote in last 2 weeks (25 min)
2. Identify 3 improvements with reasons (15 min)
3. Write constructive PR feedback for one teammate PR (10 min)
4. Solve one small coding task without AI and track time (25 min)
5. Reflection and self-rating (10 min)

---

## 1) Self Code Review

### File path:
- `E:\90days\mrmax\app\Customize\Controller\Api\PosController.php`

### Why I picked this file:
- I implemented this API. It handles coupon use and validation for POS machine purchases.

### What this file does (2-3 lines):
- Controller for the POS API. Called when any purchase happens at a POS machine.
- Routes to CouponService to either validate a coupon (TEMPORARY/syori_kb=2) or apply/use it (SALE/syori_kb=1).
- Handles 50,000+ daily calls — high volume, money-related logic.

### Quality check (quick score 1-5)
- Readability: 3
- Naming clarity: 3
- Error handling: 4
- Testability: 3
- Performance awareness: 4 — response time logged per call with microtime(), timing visible in logs

---

## 2) Three Things I Would Do Differently Today

### Improvement 1 — ApiKeyValidatorService injected but silently never used

- Current code/problem:
  The constructor declares ApiKeyValidatorService as a dependency but never stores it as a property and never calls it anywhere. Authentication is silently skipped.
  ```php
  public function __construct(
      ApiKeyValidatorService $apiKeyValidator,  // injected
      CouponService $couponService
  ) {
      $this->couponService = $couponService;    // apiKeyValidator never stored, never called
  }
  ```

- Better approach:
  Store the dependency and call it at the top of processCouponTransaction():
  ```php
  public function __construct(
      private readonly ApiKeyValidatorService $apiKeyValidator,
      private readonly CouponService $couponService
  ) {}

  public function processCouponTransaction(Request $request): Response
  {
      if (!$this->apiKeyValidator->isValid($request)) {
          return $this->createUtf8JsonResponse(['message' => 'Unauthorized'], Response::HTTP_UNAUTHORIZED);
      }
      // ... rest of the logic
  }
  ```

- Why this is better:
  The POS API processes coupon use at 50k+ calls/day. Without enforcement this is OWASP A01 (Broken Access Control). The validator class exists and was injected — it just was never wired to actually run. Any caller knowing the URL can forge requests.

- Risk of changing now: High — must confirm POS machines send the expected auth header first. Wrong rollout = all terminals get 401 and purchases fail. Needs coordinated release with POS team.

---

### Improvement 2 — validateRequestFields is 80+ lines of copy-paste if-blocks

- Current code/problem:
  Same pattern repeated 10+ times. If the error code changes, every block needs editing individually.
  ```php
  if (!isset($torihikiInfo['store_cd']) || $torihikiInfo['store_cd'] === '') {
      return $this->createUtf8JsonResponse(['message' => trans('error.40028')], Response::HTTP_BAD_REQUEST);
  }
  if (!isset($torihikiInfo['regi_no']) || $torihikiInfo['regi_no'] === '') {
      return $this->createUtf8JsonResponse(['message' => trans('error.40028')], Response::HTTP_BAD_REQUEST);
  }
  // ... same block 8 more times
  ```

- Better approach:
  Declare required fields as arrays, loop once:
  ```php
  private function validateRequestFields(array $torihikiInfo): ?Response
  {
      $alwaysRequired = ['syori_kb', 'store_cd', 'regi_no', 'kaiin_no'];
      $saleRequired   = ['torihiki_ichiren_no', 'torihiki_date', 'torihiki_time',
                         'torihiki_seq', 'seq_no', 'point_taishou_kingaku'];
      $tempRequired   = ['used_coupons_cd'];

      $category = (int)($torihikiInfo['syori_kb'] ?? 0);
      if (!in_array($category, [Constant::POS_PROCESSING_CATEGORY_SALE,
                                 Constant::POS_PROCESSING_CATEGORY_TEMPORARY], true)) {
          return $this->createUtf8JsonResponse(['message' => trans('error.40028')], Response::HTTP_BAD_REQUEST);
      }

      $conditionalRequired = $category === Constant::POS_PROCESSING_CATEGORY_SALE
          ? $saleRequired : $tempRequired;

      foreach (array_merge($alwaysRequired, $conditionalRequired) as $field) {
          if (!isset($torihikiInfo[$field]) || $torihikiInfo[$field] === '') {
              return $this->createUtf8JsonResponse(['message' => trans('error.40028')], Response::HTTP_BAD_REQUEST);
          }
      }
      return null;
  }
  ```

- Why this is better:
  Single change point for error format. Adding/removing a required field = one array line. Method shrinks from 80+ lines to ~20. Easier to review, easier to unit-test with a data provider.

- Risk of changing now: Low — pure refactor, identical behavior, testable against existing endpoint tests.

---

### Improvement 3 — extractTransactionDetails uses !empty($x) ? $x : null for every field

- Current code/problem:
  Two issues: (1) !empty() treats integer 0 as falsy — purchaseAmount of 0 would be silently mishandled. (2) Ternary copy-pasted 10 times — PHP 7+ has cleaner syntax.
  ```php
  'couponBarCode'  => !empty($torihikiInfo['used_coupons_cd']) ? $torihikiInfo['used_coupons_cd'] : null,
  'purchaseAmount' => !empty($torihikiInfo['point_taishou_kingaku']) ? (int)$torihikiInfo['point_taishou_kingaku'] : 0,
  // ... 8 more lines of same ternary
  ```

- Better approach:
  Use the null coalescing operator:
  ```php
  private function extractTransactionDetails(array $torihikiInfo): array
  {
      return [
          'couponBarCode'     => $torihikiInfo['used_coupons_cd']     ?? null,
          'memberId'          => $torihikiInfo['kaiin_no']            ?? null,
          'storeCode'         => $torihikiInfo['store_cd']            ?? null,
          'purchaseAmount'    => isset($torihikiInfo['point_taishou_kingaku'])
                                   ? (int)$torihikiInfo['point_taishou_kingaku'] : 0,
          'checkoutNumber'    => $torihikiInfo['regi_no']             ?? null,
          'transactionSeries' => $torihikiInfo['torihiki_ichiren_no'] ?? null,
          'transactionSeq'    => $torihikiInfo['torihiki_seq']        ?? null,
          'transactionDate'   => $torihikiInfo['torihiki_date']       ?? null,
          'transactionTime'   => $torihikiInfo['torihiki_time']       ?? null,
          'sequenceNo'        => $torihikiInfo['seq_no']              ?? null,
      ];
  }
  ```

- Why this is better:
  ?? is PHP 7+ idiomatic, shorter, and doesn't falsely treat 0 as null. !empty() on integers is a subtle footgun — ?? reads as "give me this field or null" which matches intent exactly.

- Risk of changing now: Low — only behavioral difference is purchaseAmount = 0 edge case. Confirm with team whether that is a valid transaction, then roll out.

---

## 3) PR Review Practice

### PR link or ID: Internal PR — new StampBook endpoint added under Customize/Controller/Api/V4/

### What changed (short summary):
New POST endpoint to issue stamps to a member after purchase. Takes member ID and purchase amount, calls StampBookService::issueStamp(), returns 200 or 400. No exception handling around the service call.

### My review feedback (2-3 lines):
The service call has no try/catch — an uncaught exception from issueStamp() will return a 500 with a raw stack trace to the POS machine, which is both a data leak and a broken response format. The existing PosController already handles this with a structured JSON 500 response — copy that pattern here for consistency. Also: memberId is taken raw from the request body without format-checking; suggest reusing the validateRequestFields approach from PosController rather than adding a new ad-hoc isset check.

### Why this feedback is useful:
Points to a real gap (unhandled exceptions at high volume = noisy incidents), gives a concrete existing code reference the teammate can copy immediately, and flags consistency — two POS API controllers behaving differently for the same error scenario is a future debugging headache.

---

## 4) No-AI Coding Task Practice

### Task chosen:
Write a PHP function getRequiredFieldErrors(array $data, array $requiredFields): array that returns a list of missing/empty field names. Empty string counts as missing. Integer 0 is NOT missing. Returns empty array if all fields present and non-empty.

### Start time: 21:10
### End time: 21:28
### Total minutes: 18

### What I tried first:
Wrote the loop with isset() only:
```php
function getRequiredFieldErrors(array $data, array $fields): array {
    $missing = [];
    foreach ($fields as $field) {
        if (!isset($data[$field])) {
            $missing[] = $field;
        }
    }
    return $missing;
}
```
Then immediately caught the bug: isset($data['store_cd']) returns true when $data['store_cd'] = '', which is the exact flaw in the real PosController.

### Where I got stuck:
Needed to add the empty-string check without using empty(), because empty() also flags 0 and false — both valid for numeric fields. Took a moment to recall exactly what isset vs empty each covers in PHP.

### How I solved it using docs/manual reasoning:
PHP docs: isset() returns false for null/missing but true for ''. empty() returns true for '', 0, false, []. The correct check for "missing or blank string but NOT zero" is !isset() || === ''. Final version:
```php
function getRequiredFieldErrors(array $data, array $fields): array {
    $missing = [];
    foreach ($fields as $field) {
        if (!isset($data[$field]) || $data[$field] === '') {
            $missing[] = $field;
        }
    }
    return $missing;
}
```
Mental test cases:
- ['store_cd' => ''] → ['store_cd'] (empty string = missing) OK
- ['amount' => 0] → [] (zero is NOT missing) OK
- [] (key absent) → field name returned OK

### Final outcome:
- [x] Completed
- [ ] Partially completed
- [ ] Not completed

---

## 5) End-of-Day Reflection

Write 3 things I learned today:
1. Reviewing my own code is uncomfortable — spotting that ApiKeyValidatorService was silently never called felt bad. That discomfort is the signal: the code passed review and went to production. "Are all injected dependencies actually called?" is now on my PR checklist.
2. Repetitive code in validateRequestFields is a maintainability tax paid every day without noticing it. Counting 10 identical if-blocks during review took 3 minutes. A fields-array loop would have made that 0 to review.
3. empty() vs isset() for integer 0 is a real PHP footgun. The correct tool for "required string fields" is !isset() || === ''. I will never use !empty() on an integer field again.

Write 2 habits I need to build:
1. Before submitting any PR: 5-minute self-review pass focused on (a) are all injected dependencies actually called? (b) is any validation/error block copy-pasted more than twice?
2. When writing field validation: declare required fields as a plain array first, then loop — never start with individual if-blocks per field.

Write 1 question for Day 7:
1. If I had to explain to a junior developer why !empty($x) is wrong for integer fields — could I do it clearly in 2 sentences without hesitation? If not, that is a teaching gap to add to Week 2 priority.

---

## Day 6 Self-Rating

Rate each area:
- Code review depth: **Explain to anyone** — found 3 real issues with actual file references, not generic "add comments" advice
- Refactoring judgment: **Use but cannot explain deeply** — can spot the pattern and write the fix, but explaining the architectural WHY is still not smooth
- Constructive PR feedback quality: **Use but cannot explain deeply** — feedback was specific with code references, but still defaulted to "look at PosController" rather than teaching the principle independently
- Problem solving without AI: **Explain to anyone** — wrote the function from PHP docs alone, hit the 0 edge case, reasoned through it, solved correctly in 18 min

Confidence score today (0-10): **7**

One commitment for Day 7: Re-read Days 1–6 notes and write an honest gap map — no sugar-coating the "use but cannot explain deeply" areas.

---

## Day 6 Completion Checklist

- [x] One recent file reviewed
- [x] Three concrete improvements documented
- [x] One teammate PR reviewed with 2-3 lines of feedback
- [x] One coding task attempted without AI
- [x] Reflection and self-rating completed
