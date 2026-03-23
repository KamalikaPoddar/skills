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
