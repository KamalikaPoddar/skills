# Agent 5 — Hypothesis Generator

McKinsey/BCG hypothesis discipline applied to product. Four competing MECE
hypotheses, kill criteria for each, and a steel-man obligation on the one
the PM least believes.

---

## Why Four, and Why MECE

**Why four:** Two hypotheses is a false binary. Three is common in PM work but
tends toward "primary, secondary, and a weak third." Four forces genuine
exploration and makes the MECE discipline harder to fake.

**Why MECE:**
- Mutually Exclusive: each hypothesis explains the problem in a way that the
  others don't. If hypothesis 1 is true, it says something different about
  what to do than if hypothesis 2 is true.
- Collectively Exhaustive: together, the four hypotheses cover all the
  plausible explanations. Nothing important is missing from the set.

**Test:** If hypotheses 1, 2, 3, and 4 are all partially true at the same time
with no conflict, they're not mutually exclusive. A good set creates genuine
decision points: the evidence that supports one should cast doubt on the others.

---

## Part A — Root Cause Hypotheses

Four competing explanations for *why the problem exists*. Drawn from the
Fishbone and Five Whys output from Agent 2, but elevated to formal hypotheses.

**Template for each:**
```
HYPOTHESIS [N]: [Problem] exists primarily because [explanation].

Evidence that would CONFIRM this:
  - [Specific, observable data point or research finding]
  - [Second data point]

Evidence that would KILL this:
  - [What we'd expect to see if this is true, that we're NOT seeing]
  - [Data point that contradicts this explanation]

Fastest/cheapest way to test:
  [Specific method: data query, user interview, experiment, support analysis]
  Time to test: [hours / days / weeks]
  Cost to test: [low / medium / high]
```

**The MECE check:**
After writing all four, ask:
1. Can two of these be simultaneously true without conflict? → If yes, they overlap (not ME)
2. Is there a plausible explanation not covered by any of the four? → If yes, missing (not CE)

**Example set (for "30-day retention dropped 12 points"):**

```
H1: The problem exists because the new Q3 paid social cohort has fundamentally
    lower intent — these users never had a real use case for the product.
    (Cohort quality hypothesis)

H2: The problem exists because the onboarding flow for mobile users is broken
    since the v2.3 update, causing a specific segment to never complete setup.
    (Product regression hypothesis)

H3: The problem exists because a competitor launched a direct alternative in
    September and users who were "experimenting" have now found a replacement.
    (Competitive displacement hypothesis)

H4: The problem exists because the core value proposition is not realised
    fast enough — users who stay 90 days are fine, but users aren't getting
    to the aha moment within the current 30-day window.
    (Time-to-value hypothesis)
```

These are MECE because: if H1 is true (bad cohort), fixing onboarding (H2's
solution) won't help. If H3 is true (competitive), fixing acquisition (H1's
solution) won't help. Each implies a different action.

---

## Part B — Solution Hypotheses

Four competing approaches to *solving the problem*. Must cover different
levels of intervention, not just different features.

**Intervention levels to cover:**
1. **Tactical (quick, narrow):** A specific product change that addresses a
   surface manifestation. Low investment, limited upside.
2. **Structural (medium, broader):** A change to a core flow, feature, or
   process. Higher investment, higher upside.
3. **Strategic (large, foundational):** A change to the business model,
   positioning, or platform architecture. Highest investment, highest upside.
4. **Non-product / do-nothing alternative:** Solve via operations, sales,
   support, or education rather than product. Or: accept the current state.

**Template for each:**
```
SOLUTION HYPOTHESIS [N]: [Level]

Approach: [What we would do]

Why it would work: [Causal logic — how does this address the root cause?]

Why it might not work: [What assumption has to hold for this to succeed?]

Signal for "this is working": [What metric or behaviour change would we
                               observe within 4–8 weeks?]

Estimated investment: [S / M / L — relative, not absolute]
```

---

## The Steel Man Obligation

**For each hypothesis the PM is *least* inclined to believe:**

The PM must write the strongest possible case for why it could be true.
Not a devil's advocate exercise. An honest attempt to find the best evidence
for the hypothesis before dismissing it.

This is the single most powerful check against confirmation bias.

```
STEEL MAN for [least-favoured hypothesis]:

The strongest case for this being true:
  - [Piece of evidence that supports it, even if weak]
  - [Historical pattern or analogy that makes it plausible]
  - [What we would have missed or ignored that could support it]

If this hypothesis is right, what would we need to do differently?
  [Specific implication for the roadmap or investigation]

Verdict: [I still think this is unlikely because X — but I've honestly
          considered it and would revisit if I saw Y]
```

---

## Kill Criteria Matrix

After writing all eight hypotheses (4 root cause + 4 solution), build the
kill criteria matrix. The goal: eliminate 3 of 4 root cause hypotheses as
cheaply and quickly as possible.

```
KILL CRITERIA MATRIX
════════════════════

| Hypothesis | Kill condition | Test method | Time | Cost | Priority |
|------------|----------------|-------------|------|------|----------|
| H1 (cohort)| Retention of   | Segment     | 2    | Low  | #1       |
|            | organic users  | analysis in | days |      |          |
|            | also dropped   | Amplitude   |      |      |          |
| H2 (regres)| Mobile-only    | Funnel      | 1    | Low  | #1       |
|            | retention same | breakdown   | day  |      |          |
| H3 (comp)  | Users who      | Cancellation| 3    | Low  | #2       |
|            | churned didn't | survey +    | days |      |          |
|            | mention comp.  | interview   |      |      |          |
| H4 (value) | Users who      | Cohort      | 3    | Low  | #2       |
|            | stayed 45+ days| analysis:   | days |      |          |
|            | have same 30d  | 30d vs 90d  |      |      |          |
|            | completion rate| retention   |      |      |          |

FASTEST PATH TO CLARITY: Run H2 test first (1 day, just look at mobile
funnel data). If mobile retention is the same as desktop, H2 is eliminated
and we've saved weeks of pursuing a product regression that isn't there.
```

---

## Full Output Format

```
╔══════════════════════════════════════════════════════════╗
  HYPOTHESIS SET
  Problem: [from Agent 1]
╠══════════════════════════════════════════════════════════╣

ROOT CAUSE HYPOTHESES (MECE):
  H1: [statement] — [confirm / kill evidence]
  H2: [statement] — [confirm / kill evidence]
  H3: [statement] — [confirm / kill evidence]
  H4: [statement] — [confirm / kill evidence]

MECE CHECK: [pass / gaps identified]

SOLUTION HYPOTHESES (different intervention levels):
  S1 (Tactical): [approach + causal logic]
  S2 (Structural): [approach + causal logic]
  S3 (Strategic): [approach + causal logic]
  S4 (Non-product / Do nothing): [approach + causal logic]

STEEL MAN:
  Least-favoured hypothesis: [which one and why it was chosen]
  Best case for it: [honest argument]
  Implication if true: [what we'd need to do differently]

KILL CRITERIA MATRIX:
  [Table with fastest tests to eliminate wrong hypotheses]

RECOMMENDED FIRST TEST:
  [Single cheapest/fastest action to eliminate at least one hypothesis]
  Time: [X days] | Cost: [low] | Decision it unlocks: [which hypothesis it kills]
╚══════════════════════════════════════════════════════════╝
```
