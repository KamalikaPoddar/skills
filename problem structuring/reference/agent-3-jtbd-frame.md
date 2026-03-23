# Agent 3 — Jobs to Be Done Frame

Three layers, four forces, non-obvious competition. Most PM JTBD work stops
at layer one (functional job). The magic is almost always in layers two and three.

---

## The Three Layers

### Layer 1 — Functional Job
What task or goal is the user *literally* trying to accomplish?
This is the surface. It matters, but it's rarely the differentiating insight.

Format: `[Action verb] + [object] + [context]`
Example: "Track the status of 15 pending international transfers without
calling the bank."

### Layer 2 — Emotional Job
How does the user want to *feel* (or avoid feeling) during and after this task?
This is where loyalty and switching decisions live.

Format: `Feel [positive state] / Avoid feeling [negative state]`
Example: "Feel confident and in control of their business cash flow. Avoid
feeling anxious about whether a payment went through or is stuck somewhere."

### Layer 3 — Social Job
How does the user want to be *perceived* by others because of how they handle this task?
This drives word-of-mouth, aspiration, and status.

Format: `Be seen as [identity/quality] by [audience]`
Example: "Be seen as a reliable, organised finance manager by their team and clients —
not someone who constantly chases payment confirmations."

**The test for a good Layer 3:** Would the user mention this job to a colleague?
If yes, the social job is real. If the job is only visible to the user themselves,
it's still emotional (Layer 2), not social.

---

## The Job Story Format

Not a user story. The key difference: Job Stories focus on context and motivation,
not persona and feature.

```
USER STORY:   As a [persona], I want [feature] so I can [benefit]
JOB STORY:    When [situation/trigger], I want to [motivation/progress],
              so I can [desired outcome]
```

Why Job Stories are superior for discovery:
- The "When" forces specificity about context — when does the job arise?
- The "I want to" is about progress, not features — what are they trying to move?
- The "So I can" is the outcome, not the immediate benefit — what bigger goal does this serve?

**Example:**
```
When: "When I'm in a client meeting and they ask about the status of a payment
       I sent last Tuesday"
I want to: "instantly pull up the full transfer history with current status and
            expected settlement date"
So I can: "answer confidently without having to say 'I'll check and get back
           to you', which makes me look disorganised"
```

Notice: this Job Story surfaces the real problem (looking disorganised in front
of clients) which has almost nothing to do with "real-time payment tracking" as a
feature spec, and everything to do with confidence and professional credibility.

---

## The Four Forces

Clayton Christensen's framework for understanding the dynamics of switching behaviour.
Every hiring decision (switching to a new solution) is a tug-of-war between four forces:

```
PUSH                              PULL
────────────────────              ─────────────────────
What's wrong with the             What attracts them to
current situation?                the new solution?
(driving them away)               (drawing them forward)

        ↑ SWITCH ↓

ANXIETY                           HABIT
────────────────────              ─────────────────────
What are they worried about       What keeps them using
with the new solution?            the current solution
(slowing them down)               even though it's not great?
                                  (pulling them back)
```

**How to use the Four Forces:**

For the user to switch (adopt your solution), PUSH + PULL must outweigh ANXIETY + HABIT.

Most product teams only focus on Pull (making their product attractive).
The insight is in the other three forces:
- **Push** reveals what users are suffering through — the problem severity
- **Anxiety** reveals what objections must be pre-empted at adoption
- **Habit** reveals what behavioural change is required — the switching cost

**Format:**
```
FOUR FORCES ANALYSIS
════════════════════

PUSH (what's wrong with current solution):
  - [Specific frustration 1]
  - [Specific frustration 2]
  - [The last-straw moment — when users finally decide to look for something better]

PULL (what a new solution would need to offer):
  - [Desired outcome 1]
  - [Desired outcome 2]
  - [The "wow" that makes them feel the switch was worth it]

ANXIETY (what makes them hesitate):
  - [Fear 1 about the new solution]
  - [Fear 2 — often: will this actually work / will I lose my data / is this secure]
  - [Trust barrier: why would I believe this new thing is better?]

HABIT (what keeps them on the old solution):
  - [Current behaviour 1 that's comfortable even if suboptimal]
  - [Switching cost: what they'd lose or have to rebuild]
  - [Social/organisational inertia: who else depends on the current way?]
```

---

## Non-Obvious Competition Map

The most powerful JTBD insight: your competition is not who you think it is.

The product is competing against *everything else that gets hired for the same job*
— not just other products in the same category.

**Framework:**
1. State the job the user needs done
2. Ask: what else could do this job?
3. Include: other products, manual workarounds, asking someone else, not doing the job, waiting

**Example — "Track international transfer status":**
```
OBVIOUS competitors: [other payment platforms, SWIFT tracking portals]

NON-OBVIOUS competitors:
  - Calling/WhatsApp messaging the bank's relationship manager
  - Asking the finance team member who sent the transfer
  - Building a custom Google Sheet with manual updates
  - Accepting uncertainty and only following up if the client complains
  - Choosing to only use domestic payments to avoid the problem entirely

INSIGHT: The real competition is the WhatsApp message to the RM — because it
gives immediate, trusted answers. Any product solution must be faster and more
trustworthy than a human response to win.
```

---

## The Firing Question

When do users actively *fire* the current solution? This reveals the emotional
threshold any new solution must clear — what has to go wrong for someone to
commit to changing behaviour.

```
FIRING ANALYSIS
═══════════════
The last straw: "The moment users decided 'I can't keep doing it this way' was when..."
[Specific scenario — from user interviews or inference]

What that moment reveals about the emotional threshold: [insight]

Implication for minimum bar: "A new solution must at minimum prevent [that moment]
from happening — or users will never feel the switch was worth it."
```

---

## Hiring Frequency and Satisfaction Assessment

```
JOB FREQUENCY & SATISFACTION
═════════════════════════════

How often does this job arise?
  [ ] Multiple times daily
  [ ] Daily
  [ ] Weekly
  [ ] Monthly
  [ ] Ad hoc / situational
  Estimated frequency for target segment: [X times per month]

How well does the current solution do the job?
  Scale: 1 (completely fails) → 10 (perfect)
  Current solution score: [X/10]
  Evidence: [what tells us this]

Opportunity gap = Frequency × (10 - Satisfaction) / 10
  = [X] × ([10 - Y] / 10)
  = [Z] ← higher = better opportunity

Benchmarks:
  > 0.6 = Strong opportunity (frequent job, poorly served)
  0.3–0.6 = Moderate opportunity
  < 0.3 = Weak opportunity (rare job or well-served already)
```

---

## Full Output Format

```
╔══════════════════════════════════════════════════════════╗
  JTBD FRAME
  User segment: [segment from Agent 1]
╠══════════════════════════════════════════════════════════╣

THREE LAYERS:
  Functional job: [what task]
  Emotional job:  [how they want to feel / avoid feeling]
  Social job:     [how they want to be perceived]

JOB STORY:
  When [situation/trigger],
  I want to [motivation/progress],
  so I can [desired outcome].

FOUR FORCES:
  Push:    [what's driving them away from current solution]
  Pull:    [what they'd want from a new solution]
  Anxiety: [what makes them hesitate to switch]
  Habit:   [what keeps them on the current solution]

NON-OBVIOUS COMPETITION:
  [List of what else is hired for this job — include workarounds]
  Key insight: [what this tells us about the real competition]

FIRING QUESTION:
  The last straw: [specific scenario]
  Implication: [minimum bar any solution must meet]

FREQUENCY & SATISFACTION:
  Frequency: [X per month]
  Satisfaction with current: [X/10]
  Opportunity gap score: [X]

KEY INSIGHT:
[One paragraph. The non-obvious thing this analysis reveals about
what users actually need — which couldn't have been found by asking
"what features do you want?"]
╚══════════════════════════════════════════════════════════╝
```
