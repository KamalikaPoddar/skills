# Agent 6 — Cross-Sprint Pattern Recognizer

Requires data from up to 6 sprints. The current sprint in isolation tells
you what happened. Six sprints together tell you what's actually going on.

**Graceful degradation:** If only 2–3 sprints available, run what's possible
and explicitly note what patterns require more history to confirm.

---

## Pattern 1 — Velocity Trend

```
VELOCITY TREND ANALYSIS
════════════════════════

Story points delivered per sprint (oldest → most recent):
  Sprint 1: [N pts]
  Sprint 2: [N pts]
  Sprint 3: [N pts]
  Sprint 4: [N pts]
  Sprint 5: [N pts]
  Sprint 6: [N pts] ← current

6-sprint average: [X pts]
3-sprint trend:   [improving / stable / declining by X%]

Velocity trend verdict:
  [IMPROVING]  — team is accelerating; investigate what's working
  [STABLE]     — consistent performance; healthy baseline established
  [DECLINING]  — velocity is falling; investigate before assuming capacity issue
  [VOLATILE]   — high variance sprint to sprint; investigate predictability

If declining or volatile:
  Correlation check (run for each):
  □ Bug-fix % increased over same period? (quality debt slowing team)
  □ Unplanned work % increased? (reactive work crowding out productive work)
  □ Team size changed? (adds or losses that aren't reflected in planned capacity)
  □ Tech complexity increased? (new system, migration, new tech area)

📌 CONTEXT NEEDED FROM PM:
   Velocity has [declined/been volatile] over the last [N] sprints.
   What changed in this period? (Team changes, tech complexity, product area
   shift, process changes, external pressures?)
```

---

## Pattern 2 — Recurring Slips

```
RECURRING SLIP ANALYSIS
════════════════════════

Identify: ticket types, epics, or engineers associated with slippage
across multiple sprints (not just this one).

By ticket type:
  [Type] slips in [N of 6] sprints — [systemic / episodic]

By epic/theme:
  [Epic name] has had slippage in [N of 6] sprints — [systemic / episodic]

By blocker source:
  [Blocker type] appears in [N of 6] sprints — [systemic / episodic]

Most consistent slip pattern: [category] — [N sprints] — [what this implies]

Systemic vs. Episodic classification:
  SYSTEMIC  — appears in 3+ of 6 sprints; structural intervention needed
  EPISODIC  — appears in 1–2 sprints; situation-specific, monitor

📌 CONTEXT NEEDED FROM PM:
   [Slip pattern] has recurred in [N] of the last [N] sprints.
   Is there a structural reason for this that hasn't been addressed?
   (Example: a recurring external dependency, a technical area that's always
   underestimated, a process that creates consistent friction?)
```

---

## Pattern 3 — Work Composition Drift

```
COMPOSITION DRIFT OVER TIME
════════════════════════════

                Sprint 1  Sprint 2  Sprint 3  Sprint 4  Sprint 5  Sprint 6
New features:    [X%]      [X%]      [X%]      [X%]      [X%]      [X%]
Bug fixes:       [X%]      [X%]      [X%]      [X%]      [X%]      [X%]
Tech debt:       [X%]      [X%]      [X%]      [X%]      [X%]      [X%]
Unplanned:       [X%]      [X%]      [X%]      [X%]      [X%]      [X%]

Significant drifts over 6 sprints:
  [Category] went from [X%] to [Y%] — [direction] trend — [implication]
  [Category] went from [X%] to [Y%] — [direction] trend — [implication]

Most concerning drift: [finding]

Typical drift signals and what they mean:
  Bug fix % increasing over time: Quality investment is insufficient; 
    each sprint creates more bugs than the previous sprint can clear
  Unplanned % increasing over time: Reactive culture accelerating;
    team is losing ability to protect its sprint commitments
  New feature % declining over time: Team is increasingly in maintenance mode;
    if intentional, fine; if not, product velocity is stalling
  Tech debt % declining over time: Debt is accumulating; 
    the "we'll address it next sprint" is becoming "never"
```

---

## Pattern 4 — Team Health Signals From Data

**Data proxies for team dynamics.** These are signals, not conclusions.
Always pair with human context.

```
TEAM HEALTH INDICATORS
══════════════════════

Churned tickets (status changed 5+ times):
  [N] tickets this sprint vs prior sprint average: [N]
  High churn = rework, unclear requirements, or indecision signal

PR review participation (if GitHub data available):
  Average reviewers per PR this sprint: [N] vs prior avg: [N]
  Declining = team isolating, rushing, or losing code review culture

Sprint carry rate (carryover as % of next sprint's capacity):
  Last 3 sprints: [X%] → [X%] → [X%]
  Increasing carry rate = planning is getting worse OR work is getting harder

Ticket-level commentary (from Jira comments, if accessible):
  Tickets with no comments from assignee: [N] — possible disengagement signal
  (Note: absence of comments could also mean clear requirements — context needed)

HEALTH SIGNAL SUMMARY:
  [GREEN] — no concerning patterns in the data
  [AMBER] — [specific signal] worth a conversation
  [RED]   — [specific signal] suggests a structural team issue

📌 CONTEXT NEEDED FROM PM:
   The data shows [signal]. Is this reflecting something real in the team's
   experience right now? (These are data proxies — human context is essential
   before drawing conclusions.)
```

---

## Pattern 5 — OKR Coverage Consistency

```
OKR COVERAGE OVER TIME
══════════════════════

For each OKR/KR, what % of sprint capacity was directed at it each sprint:

         Sprint 1  Sprint 2  Sprint 3  Sprint 4  Sprint 5  Sprint 6
OKR1:     [X%]      [X%]      [X%]      [X%]      [X%]      [X%]
OKR2:     [X%]      [X%]      [X%]      [X%]      [X%]      [X%]
Orphaned: [X%]      [X%]      [X%]      [X%]      [X%]      [X%]

OKRs consistently underfunded (< 5% per sprint for 3+ sprints):
  [OKR name] — appears on the OKR list but has never gotten meaningful work
  
📌 CONTEXT NEEDED FROM PM:
   [OKR] has received less than 5% of sprint capacity across [N] sprints.
   Is this OKR still a real commitment? Or has it become an aspirational
   objective that the team isn't actually pursuing?
```

---

## Cross-Sprint Pattern Output

```
╔══════════════════════════════════════════════════════╗
  CROSS-SPRINT PATTERNS — Last [N] Sprints
╠══════════════════════════════════════════════════════╣

VELOCITY: [Improving / Stable / Declining / Volatile]
RECURRING SLIPS: [Systemic patterns found / None detected]
COMPOSITION DRIFT: [Significant drifts identified / Stable]
TEAM HEALTH: [GREEN / AMBER / RED — key signal]
OKR CONSISTENCY: [Consistent / Inconsistent — which OKRs underfunded]

TOP 3 PATTERNS:
  1. [Most significant pattern + what it implies]
  2. [Second pattern]
  3. [Third pattern]

SYSTEMIC vs EPISODIC:
  Systemic (3+ sprints): [list]
  Episodic (1–2 sprints): [list]

📌 HUMAN MOAT CONTEXT NEEDED: [Top questions]
╚══════════════════════════════════════════════════════╝
```

---

# Agent 7 — Uncomfortable Truth Generator

**This agent does what retros don't.**

The official sprint/quarter narrative is almost always partially true.
This agent looks at what the data shows that the narrative omits, softens,
or contradicts — and names it precisely.

---

## How It Works

Take the official story (explicitly stated by PM, or reconstructed from
the audit's positive findings). Then compare it to what the data from
Agents 2–6 actually shows.

```
THE CONTRAST FORMAT:

Official narrative:  "[What the PM or team said / would say about this sprint]"
Data narrative:      "[What Agents 2–6 actually show]"
The gap:             "[What the official story omits or softens]"
The question:        "[What the PM needs to answer before this can be resolved]"
```

---

## Category 1 — Output vs. Outcome Gaps

```
FINDING: [Sprint/quarter] produced [N] tickets / [N pts] of output.
  OKR metric [KR1] moved [flat / away from target / unmeasured].
  
  Official story: "We had a productive sprint."
  Data story:     "The sprint produced output. We don't know if it produced outcomes."
  The gap:        The team is measuring sprint health by ticket closure,
                  not by metric movement. These are not the same thing.
  The question:   Is the team's hypothesis about what drives [metric] correct?
                  Or is the work being done in good faith but not the right work?

📌 CONTEXT NEEDED FROM PM: [Specific question]
```

---

## Category 2 — Strategic Drift Without a Decision Record

```
FINDING: [Feature / OKR / Initiative] was a committed priority for [period].
  It has now [not been started / been deferred N times / received < 5%
  of sprint capacity across N sprints].
  
  Official story: "[Feature] is on the roadmap for Q[N]."
  Data story:     "[Feature] has not had a single ticket in the last [N] sprints."
  The gap:        The roadmap says one thing. The sprint history says another.
                  There is no recorded decision explaining the gap.
  The question:   Was there a deliberate decision to deprioritise this?
                  If yes, where is that decision documented?
                  If no, this is silent scope creep by omission.

📌 CONTEXT NEEDED FROM PM: [Specific question]
```

---

## Category 3 — Reactive Work Camouflaged as Strategic

```
FINDING: [X%] of sprint capacity was unplanned or reactive.
  These tickets are not on the roadmap and don't link to any OKR.
  The sprint completion rate is reported as [X%].
  
  Official story: "The team completed [X%] of the sprint."
  Data story:     "[X%] of what was completed was reactive work that
                  entered mid-sprint and displaced [Y pts] of planned work."
  The gap:        The completion metric looks healthy, but it's partly
                  because the denominator (planned work) shrank when
                  reactive work entered and planned work was quietly dropped.
  The question:   Is the team aware of this pattern? Is there a mechanism
                  to make the trade-off explicit when reactive work enters?

📌 CONTEXT NEEDED FROM PM: [Specific question]
```

---

## Category 4 — Chronic Avoidance

```
FINDING: [Ticket / Feature / Tech debt item] has been in "In Progress"
  or carried over for [N] consecutive sprints.
  
  Official story: "It's almost done, just a few more things to sort out."
  Data story:     "[N] sprints is not 'almost done.' Something is preventing
                  completion that the data cannot explain."
  The gap:        Chronic carryover is almost never purely technical.
                  It is usually: unclear definition of done, a decision
                  nobody wants to make, an external dependency nobody wants
                  to escalate, or a piece of work nobody actually owns.
  The question:   What specifically is preventing closure? What decision
                  or action would unstick this?

📌 CONTEXT NEEDED FROM PM: [Specific question]
```

---

## Category 5 — The Metric That Didn't Move

```
FINDING: [X pts] of work targeted [KR metric]. The metric moved [flat / wrong direction].
  
  Official story: "We invested heavily in [area] this sprint."
  Data story:     "Investment confirmed. Impact unconfirmed. The metric
                  didn't respond the way the hypothesis predicted."
  The gap:        The team shipped. The metric didn't move. One of three
                  things is true: (1) The hypothesis was wrong about what
                  drives this metric. (2) The effect lags (will show up
                  in future sprints). (3) The metric is being measured wrong.
                  All three are important. Only one of them is comfortable.
  The question:   Which of these three explains the gap? And what changes
                  in next sprint if the hypothesis was wrong?

📌 CONTEXT NEEDED FROM PM: [Specific question]
```

---

## Tone and Framing Rules

These findings are stated as data observations, not accusations.
Every uncomfortable truth is:

1. **Grounded in specific data** — "X sprints," "Y% of capacity," not vague claims
2. **Paired with a question** — the data shows the pattern; the PM provides the org context
3. **Framed as "the data says X — what's the explanation?"** not "you failed at Y"
4. **Accompanied by the human moat acknowledgement** — Claude sees the data pattern;
   the PM sees the organisational reality that explains it

```
UNCOMFORTABLE TRUTH OUTPUT FORMAT
═══════════════════════════════════

FINDING [N]: [Title]
─────────────────────
Official narrative:  [What the team would say]
What the data shows: [What agents 2–6 actually found]
The gap:             [What's being omitted or softened]
Evidence:            [Specific data points]

📌 CONTEXT NEEDED FROM PM:
   [The specific question that only org-aware PM judgment can answer]
   
   Once you provide context, I can either: (a) incorporate your explanation
   into the final report, or (b) flag this as an open issue with the context
   noted for the record.
```

---

## UPDATED — C7 Uncomfortable Truths: Cross-Pass Additions

The following truth categories are new in the three-pass rebuild.
They draw from Pass 1 and Pass 2 findings that the original skill didn't have.

---

## Pass 1 Sourced Truths

### "The Tickets Were the Problem, Not the Engineers"

```
FINDING: Bug rate and spillage rate are [high], but Pass 1 scores show
  AC coverage averaging [X/5] and description quality averaging [X/5].
  
  Official story: "We need better engineering discipline."
  Data story:     "The tickets didn't specify edge cases. They didn't have
                  failure states. The engineers built what was written.
                  The problem is upstream of engineering."
  The gap:        Blaming execution when artifacts are the root cause.
                  The right intervention is in grooming, not in retrospective
                  pressure on engineers.
  The question:   Who writes the AC for these tickets? Who reviews it for
                  completeness before sprint planning?

📌 CONTEXT NEEDED FROM PM:
   Pass 1 shows [X%] of tickets had AC coverage below 3/5.
   Who is responsible for AC quality — PM, tech lead, or shared?
   Is there a review step before tickets enter sprint planning?
```

### "The Estimation Process Doesn't Match the Description"

```
FINDING: Story points are consistently [under/over]-estimated for [ticket type],
  and estimation was set [before/after] development began on [X%] of tickets.
  
  Official story: "Estimation is hard. It's more of an art."
  Data story:     "[X%] of this sprint's estimates were set after development
                  started. Estimation after you've started is not planning —
                  it's recording history."
  The gap:        Estimation being treated as a process requirement to fill in
                  rather than a planning tool that forces scope clarity.
  The question:   Is estimation happening in grooming sessions with engineers
                  before sprint planning, or is it a PM-assigned field?
```

---

## Pass 2 Sourced Truths

### "The Code Review Isn't Working as a Quality Gate"

```
FINDING: [X%] of bugs raised this sprint are REGRESSION type (B1).
  Pass 2 B4 shows [X%] of reviews were classified as SHALLOW or RUBBER STAMP.
  
  Official story: "We do code reviews on every PR."
  Data story:     "Code reviews happened. They didn't catch [X] regressions
                  that then required separate bug fixes costing [N] additional
                  story points. The reviews are a ceremony without effect."
  The gap:        Conflating the presence of reviews with the quality of reviews.
  The question:   What is the review checklist? Is there a specific step where
                  reviewers check the AC against what the diff shows?

📌 CONTEXT NEEDED FROM PM:
   Is there a review template or checklist? Do reviewers have access to
   the Jira ticket and AC when they review the PR?
```

### "The Implementation Diverged From the Spec Without a Record"

```
[Only generated if B5 found CONTRADICTED or SIGNIFICANT DEVIATION items]

FINDING: [N] AC items in [PROJ-ID] show a contradiction between what was
  specified and what CodeRabbit describes as implemented.
  
  Official story: "We shipped [feature]."
  Data story:     "The feature was shipped. [Specific AC item] says [X].
                  The implementation does [Y]. There is no record of a
                  decision to change this."
  The gap:        Implementation decisions made during development not
                  communicated back to the spec or PM.
  The question:   Was this deviation intentional? If yes, why wasn't the
                  AC updated? If no, this is a functional gap that needs fixing.

📌 CONTEXT NEEDED FROM PM:
   [Quote the specific contradiction.]
   Was this a deliberate design decision during development?
   If so: update the AC to match. If not: this needs to be fixed.
```

### "The Board Shows Stop-Start, Not Smooth Delivery"

```
FINDING: [X%] of sprint tickets had 3+ status regressions (B2).
  Average board flow efficiency: [LOW].
  
  Official story: "Development moved forward. Some iteration happened."
  Data story:     "[X] tickets moved backwards [N] times. The sprint board
                  shows a stop-start pattern, not continuous flow.
                  Stop-start has a direct cost: context switching,
                  re-ramp time, and morale drain."
  The gap:        Board metrics showing friction that the retro didn't discuss.
  The question:   What caused the repeated regressions on [specific tickets]?
                  Was it review feedback? Unclear requirements? Changing scope?
```

---

## The Retro Accountability Truth

```
[Generated when retro effectiveness score is LOW or PERFORMATIVE]

FINDING: [X of N] retro action items from last sprint show NO CHANGE or
  WORSE in this sprint's data (C5).
  
  Official story: "We do regular retrospectives to continuously improve."
  Data story:     "[X%] of last sprint's commitments didn't produce
                  measurable change. The retro created action items;
                  the data shows they weren't acted on."
  The gap:        The retrospective as a comfort ritual rather than an
                  improvement engine. Generating action items and
                  implementing action items are different activities.
  The question:   Were action items assigned to named owners with
                  specific completion dates? Were they checked at
                  sprint start, not just sprint end?

📌 CONTEXT NEEDED FROM PM:
   Are retro action items tracked anywhere between retros?
   Who is accountable for following up on them before the next sprint?
```