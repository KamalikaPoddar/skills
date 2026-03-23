# Agent 8 — Synthesizer

Takes all prior analysis and produces the communication artifacts. Every section
must pass the "So What" test before it's included. If a section doesn't change
what the PM would do next, it doesn't belong in the brief.

---

## The "So What" Test

Before including any section in the one-pager, ask:

*"What decision or action does this section enable? If a stakeholder reads this,
what should they do differently as a result?"*

If the answer is "nothing — it's just interesting background," cut the section
or rewrite it until it earns its place.

---

## Output 1 — One-Sentence Problem Statement (Final Refined)

This is the sentence that went through 7 rounds of analysis and came out the
other side sharper and more precise than when it entered.

Format remains the same as Agent 1's canonical format — but now enriched with
the specific root cause evidence, JTBD insight, and opportunity framing:

```
[Evidence of problem] affects [specific user segment] [context/frequency],
causing [user consequence — grounded in JTBD emotional/social job insight]
and [business consequence — grounded in impact model].

Root cause: [one sentence from Agent 2]
Core job: [one sentence from Agent 3]
Target opportunity: [one sentence from Agent 4]
```

---

## Output 2 — One-Page Problem Brief

### Section 1 — The Problem (Lead with evidence)

```
WHAT'S HAPPENING:
[3–5 bullet points of hard evidence — data, quotes, observations]
[No interpretations yet — just facts]

WHY IT MATTERS:
[Business consequence: metric affected, magnitude, trajectory]
[User consequence: what this means for the user's functional/emotional/social job]
```

### Section 2 — Why It's Happening (Root cause in plain language)

```
MOST LIKELY ROOT CAUSE:
[One paragraph. Written for a non-technical, non-product audience.
Uses no PM jargon. States the causal logic clearly.]

COMPETING EXPLANATION WE HAVEN'T RULED OUT:
[One sentence naming the second-most-likely root cause and what would
confirm or kill it]
```

### Section 3 — The Opportunity

```
WHAT USERS ACTUALLY NEED:
[One paragraph translating the JTBD and OST output into plain language.
What is the gap between where users are and where they want to be?]

TARGET OPPORTUNITY:
[The highest-priority sub-opportunity from Agent 4, stated as a user need]

ADJACENT OPPORTUNITIES:
[2–3 bullet points on connected needs that could expand scope later]
```

### Section 4 — Business Case (Brief)

```
SIZE OF THE PRIZE:
Year 1 realistic: [number + methodology in one sentence]
Year 3 with execution: [number]

Key assumption: [The single most load-bearing assumption — if this is wrong,
                 the model changes by [X]]
```

### Section 5 — Leading Hypothesis

```
WHAT WE BELIEVE AND WHY:
[State the primary root-cause hypothesis and the primary solution hypothesis
in plain language]

WHAT WOULD CHANGE OUR MIND:
[The single piece of evidence that would cause us to abandon this hypothesis]
```

### Section 6 — Recommended Next Steps

```
BEFORE WE COMMIT TO ANYTHING:
[The 2–3 validation actions from the kill criteria matrix — cheapest/fastest
 tests to eliminate wrong hypotheses]

DECISION THIS ANALYSIS SUPPORTS:
[The specific decision or conversation this brief is intended to inform]

WHAT WE'RE NOT DOING YET:
[Explicit statement of what's out of scope — what solutions we're NOT
 evaluating yet, and why]
```

---

## Output 3 — Three How Might We Statements

One per major opportunity cluster from Agent 4. The HMW format is used for
ideation facilitation — it opens up solution exploration without presupposing
a specific feature or approach.

**Format rules:**
- Start with "How might we..."
- Broad enough to allow multiple different solutions
- Narrow enough to exclude solutions that don't address this opportunity
- Written from the user's perspective or outcome, not the company's action

```
HMW 1 (for Opportunity Cluster 1):
"How might we help [user segment] [achieve desired outcome] [without / even when
/ so that] [context that makes the current situation hard]?"

HMW 2 (for Opportunity Cluster 2):
[Same format]

HMW 3 (for Opportunity Cluster 3):
[Same format]
```

**Test:** Each HMW should make a designer or engineer immediately think of
at least 3 different possible approaches. If it only suggests one solution,
it's too narrow.

---

## Output 4 — Success Metric Definition

The problem hasn't been solved until this metric moves. Everything else is
an output, not an outcome.

```
SUCCESS METRIC DEFINITION
═════════════════════════

Primary metric: [metric name]
  Current baseline: [value] (measured [how] on [date])
  Target: [value] by [date]
  Why this metric and not [alternative]: [one sentence]

Signal metric (leading indicator — moves first, predicts primary metric):
  [metric name]
  Current: [value]
  What we expect to see: [X] within [Y weeks] if we're on track

Guardrail metric (must not degrade):
  [metric name]
  Current: [value]
  Threshold: Do not proceed if this falls below [value]

Measurement method: [how we'll track progress — specific tool, query, or process]
```

---

## Output 5 — Open Questions and Load-Bearing Assumptions

Every analysis has gaps. Naming them explicitly is more useful than pretending
they don't exist.

```
OPEN QUESTIONS
══════════════
[Questions we don't have answers to yet that matter for the decision]

1. [Question] — Why it matters: [implication] — How to answer: [method + owner]
2. [Question] — Why it matters: [implication] — How to answer: [method + owner]
3. [Question] — Why it matters: [implication] — How to answer: [method + owner]

LOAD-BEARING ASSUMPTIONS
═════════════════════════
[Assumptions the entire analysis depends on — if wrong, the analysis changes]

1. [Assumption] — Confidence: [H/M/L] — How to validate: [method]
2. [Assumption] — Confidence: [H/M/L] — How to validate: [method]
3. [Assumption] — Confidence: [H/M/L] — How to validate: [method]
```

---

## Output 6 — Validation Plan

The 2–3 cheapest and fastest ways to eliminate wrong hypotheses before
committing to a solution.

```
VALIDATION PLAN
═══════════════

Before committing to a solution direction, run these in order:

Test 1 (Run first):
  What: [specific test — data query, user interview, prototype, experiment]
  Hypothesis it tests: [H-number from Agent 5]
  Time: [X days] | Cost: [person-hours] | Owner: [role]
  Decision it unlocks: [if X then Y, if not-X then Z]

Test 2 (Run if Test 1 is inconclusive):
  [Same format]

Test 3 (Optional — if budget allows):
  [Same format]

TOTAL VALIDATION INVESTMENT BEFORE SOLUTION COMMITMENT:
  [Days: X | Person-hours: Y | Key decision it enables: Z]
```

---

## Full Deliverable

The complete output of Agent 8 is a structured document containing all six
outputs above. Target length: 2–4 pages. Each section should be readable by
a non-PM stakeholder in under 2 minutes.

**The headline test:** Can a busy executive read the one-sentence problem statement
and the one-page brief headline section, and within 90 seconds know:
1. What the problem is
2. Why it matters to the business
3. What we're going to do about it first

If yes: the brief is ready to share.
If no: something is missing or unclear — return to the relevant agent.
