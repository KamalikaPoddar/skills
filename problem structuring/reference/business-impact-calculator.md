# Business Impact Calculator

**Shared Agent — importable by any PM skill.**

Builds a causally-connected business impact model that ties a specific
problem → solution → metric movement → business value. Not a TAM slide.
A living equation that can be stress-tested and updated as assumptions change.

**Input interface:** Problem statement + target user segment + industry context
**Output:** Impact equation, TAM/SAM/SOM with methodology, sensitivity analysis,
            time horizon, and brutal reality checks

---

## Why This Is Different From "Calculate Our TAM"

A TAM is a market ceiling. An impact model is a causal argument.

The difference:

| TAM approach | Impact model approach |
|---|---|
| "The market is $5B" | "If we solve X for Y users, metric M moves by Z%" |
| Top-down from analyst reports | Bottom-up from unit economics |
| Answers: how big is the sky? | Answers: how much can we reach? |
| No causal chain | Full causal chain, testable at every link |
| Weak under investor scrutiny | Holds up to "how did you get there?" |

Both matter. This agent produces both — but the impact model is the primary output.

---

## Step 1 — Build the Impact Equation

Before any numbers, write the causal equation in plain English.

**Template:**
```
[Business metric] is driven by:
  [Driver 1] × [Driver 2] × [Conversion/rate] × [Frequency]

Where solving [problem] primarily affects [which driver(s)].

Therefore: solving [problem] for [user segment] should move [metric]
by approximately [X]% if [key assumption holds].
```

**Examples by metric type:**

Revenue:
```
Revenue = Active users × Conversion rate × Average order value × Purchase frequency

Solving "users can't find what they searched for" affects:
  Conversion rate (directly) and Purchase frequency (indirectly via satisfaction)
```

Retention:
```
Retention = 1 - (Churned users / Total users)
Churned users = Users who hit [pain point] × Churn probability given that pain

Solving [pain point] reduces churned users by X%, improving retention by Y%
```

Activation:
```
Activated users = Signups × % who reach aha moment × % who return within 7 days

Solving "new users don't understand how to do [core task]" affects:
  % who reach aha moment — the direct lever
```

---

## Step 2 — Size the Opportunity (Top-Down)

**TAM — Total Addressable Market**
```
Definition: Total revenue opportunity if every potential customer used your solution
Method: Industry analyst report OR (total potential customers × average revenue/customer)
Source: [Cite specific report, year, methodology]
Confidence: [High if from authoritative source / Low if extrapolated]

TAM = [number] ([source], [year])
```

**SAM — Serviceable Addressable Market**
```
Definition: Portion of TAM reachable with current product, model, and geography
Method: Filter TAM by: geography + customer segment + product capability limits
Constraints applied: [list each filter and its effect on the number]

SAM = TAM × [geography filter %] × [segment filter %] × [product filter %]
    = [number]
```

**SOM — Serviceable Obtainable Market (3-year)**
```
Definition: What you can realistically capture in 3 years
Method: Bottom-up model (see Step 3) anchored to TAM/SAM for sanity
Inputs: current traction + growth rate + sales capacity + CAC

SOM (Year 1) = [number] ([assumptions])
SOM (Year 3) = [number] ([assumptions])
```

**Reconciliation:**
```
Top-down implies: [X customers at Y ARPU] = [SOM figure]
Bottom-up implies: [X customers at Y ARPU] = [SOM figure]
Gap: [difference and why]
Conclusion: [which number to use and why]
```

---

## Step 3 — Size the Opportunity (Bottom-Up)

This is the number that matters for planning. TAM is context. SOM is the plan.

**Unit economics model:**
```
Affected users = [Total users] × [% who face this problem] × [% for whom it's frequent]
                = [number]

Value per user per year = [frequency of problem] × [value of solving it once]
                        = [number]

Annual opportunity     = Affected users × Value per user × [your capture rate]
                       = [number]
```

**User-level value estimation:**
```
How to estimate "value of solving it once":
  Option A — Time saved: [minutes saved] × [user hourly rate] × [frequency]
  Option B — Revenue unlocked: [transaction value] × [increase in conversion %]
  Option C — Cost avoided: [cost of current workaround] × [frequency]
  Option D — Willingness to pay: [what users currently pay for alternatives]
```

---

## Step 4 — Sensitivity Analysis

Identify the three assumptions that change the model by 2x or more if wrong.
These are the load-bearing assumptions. Everything else is noise.

```
SENSITIVITY TABLE
═════════════════
Assumption              | Base case | Bear case | Bull case | Impact of being wrong
─────────────────────── | ───────── | ───────── | ───────── | ─────────────────────
% of users with problem | 35%       | 15%       | 55%       | 2.3x swing on SOM
Frequency per month     | 8×        | 3×        | 15×       | 1.9x swing
Capture rate Year 3     | 8%        | 3%        | 15%       | 2.1x swing

Highest-risk assumption: [which one and why]
How to validate it cheapest: [specific method — survey, cohort analysis, etc.]
```

---

## Step 5 — Time Horizon

```
IMPACT TIMELINE
═══════════════
Year 1 (Conservative):
  Users reached: [n] | Revenue/retention/activation impact: [X]
  Key constraint: [what limits Year 1 capture]
  Assumption: [what has to be true]

Year 3 (Base case):
  Users reached: [n] | Revenue/retention/activation impact: [X]
  Key constraint: [what limits Year 3]
  What changes between Y1 and Y3: [distribution, product maturity, awareness]

Year 5 (Tailwind case):
  Users reached: [n] | Revenue/retention/activation impact: [X]
  What tailwinds drive this: [market growth, platform effects, ecosystem]
```

---

## Step 6 — Reality Checks (Non-Negotiable)

Run every model through these four tests before finalising:

**Test 1 — The 1% Rule**
```
Question: Does your Year 1 SOM require converting more than 1% of the SAM?
If yes: the model is probably wrong unless you have exceptional distribution
        or a viral/platform mechanic.

[Calculate: SOM Year 1 / SAM = X%]
[Pass / Fail — if fail, explain why the exception applies]
```

**Test 2 — The CAC Sanity Check**
```
Question: Does your capture model require a CAC that your margin can support?
LTV:CAC should be ≥3:1 for a sustainable business.

Implied CAC = [sales & marketing cost to acquire 1 customer]
Implied LTV = [value per customer × average lifetime]
LTV:CAC ratio = [number] — [healthy / concerning / broken]
```

**Test 3 — The "So What" Test**
```
Question: Does solving this problem move a metric the business actually
          cares about and tracks? Or is this a proxy metric nobody acts on?

Primary metric moved: [name]
Who in the company owns this metric: [team/person]
Is it in the company OKRs or board reporting: [yes/no]
If no: reconsider whether this is the right problem to size
```

**Test 4 — The Competitive Deflation Test**
```
Question: Does your model assume you capture users who are currently
          served by a direct competitor? If yes, competitive response
          will shrink your capture rate.

Market is: [greenfield / competitor-served / split]
If competitor-served: apply 50% deflation to SOM unless you have
                      a 10x advantage on a dimension users care about
```

---

## Output Format

Deliver the full model in this structure:

```
╔══════════════════════════════════════════════════════════╗
  BUSINESS IMPACT MODEL
  Problem: [one-line problem statement]
  User segment: [segment]
  Primary metric: [metric]
╠══════════════════════════════════════════════════════════╣

IMPACT EQUATION:
[Causal equation in plain language]
[Which drivers are affected by solving this problem]

MARKET SIZE:
  TAM: [number] ([source])
  SAM: [number] ([methodology])
  SOM Year 1: [number] ([key assumptions])
  SOM Year 3: [number] ([key assumptions])

BOTTOM-UP CHECK:
  [Affected users] × [Value/user/year] × [Capture rate] = [SOM]
  Top-down / bottom-up reconciliation: [gap and explanation]

SENSITIVITY (top 3 load-bearing assumptions):
  1. [Assumption]: [base / bear / bull] — [impact of being wrong]
  2. [Assumption]: [base / bear / bull] — [impact of being wrong]
  3. [Assumption]: [base / bear / bull] — [impact of being wrong]

REALITY CHECKS:
  1% Rule: [Pass / Fail — explanation]
  CAC sanity: [LTV:CAC ratio and health]
  So What test: [metric owner and business relevance]
  Competitive deflation: [applied / not applicable — why]

HEADLINE:
[One paragraph that a non-financial stakeholder can read and say
"I understand why this problem is worth solving". Written in plain
English. Numbers present but not leading. Outcome-first.]
╚══════════════════════════════════════════════════════════╝
```

---

## Reuse Instructions

**From PM Problem Structuring (Agent 6):**
Run this agent after root causes and JTBD are established.
Input: the sharpened problem statement from Agent 1 + JTBD output from Agent 3.
Output feeds directly into Agent 8 (Synthesizer).

**From PRD Writer (Business Impact section):**
Run this agent after the problem is defined in the PRD.
Input: problem statement + target user from PRD header.
Output: paste the Impact Model output into the PRD's "Business Impact" section.

**From PM Rapid Prototype Builder (stakeholder prep):**
Run before the stakeholder meeting to give the PM numbers to defend the prototype.
Input: Prototype Brief from Agent 1.
Output: use the Headline paragraph in the prototype demo narrative.

---

## Fintech-Specific Additions

For payment, banking, or financial services problems, add:

**Regulatory risk deflation:**
```
If solving this problem requires regulatory approval or changes to
compliant workflows, apply a 12-18 month delay to Year 1 SOM and
deflate by 30% to account for implementation drag.
```

**Settlement cycle impact:**
```
For problems that affect transaction volume, size in:
  - Transaction value (not just user count)
  - Settlement frequency (daily/T+1/T+2 etc.)
  - Float economics if applicable
```

**Network effects multiplier:**
```
For problems in two-sided markets (payer + payee, sender + recipient):
  - Solving for one side has multiplier effect on the other
  - Model both sides separately, then apply network effect factor (1.3-2x
    depending on market maturity)
```
