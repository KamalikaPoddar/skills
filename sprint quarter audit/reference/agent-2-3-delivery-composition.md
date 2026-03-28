# Agent 2 — Delivery Fidelity Auditor

Beyond "we delivered 80% of points." The forensic investigation into
*why* delivery looked the way it did — and what it predicts about the next sprint.

---

## Metric 1 — Sprint Completion Rate

```
Sprint completion = Story points delivered / Story points planned on Day 1

This sprint: [X%]
Prior sprint: [X%]
6-sprint average: [X%] (if available)

Interpretation thresholds:
  ≥85%: Strong — team is planning and executing well
  70–84%: Acceptable — some slippage, investigate causes
  50–69%: Concerning — systematic planning or execution problem
  <50%:  Critical — this sprint's plan was fundamentally wrong
```

**Important nuance:** A 100% completion rate with very low planned points is
not a strong sprint. Flag if planned points are significantly below the team's
historical average velocity.

---

## Metric 2 — Unplanned Work Ratio

**This is the metric most teams don't track but which explains most velocity problems.**

```
Unplanned work = tickets added after sprint start date (Day 1)

Tickets added mid-sprint: [N]
Story points added mid-sprint: [N]
Unplanned work ratio: [X% of total sprint effort]

Thresholds:
  <10%: Healthy — team is protecting its sprint
  10–20%: Manageable — some reactive pull, investigate sources
  20–30%: Concerning — reactive culture beginning to dominate
  >30%: Critical — the sprint plan is mostly a fiction

Sources of unplanned work (classify each mid-sprint ticket):
  Production incident / hotfix: [N]
  Stakeholder escalation:       [N]
  Customer request (direct):    [N]
  Dependency unblocked:         [N]
  Scope expanded on existing ticket: [N]
  Unknown / no label:           [N]

Most common source this sprint: [category]
```

---

## Metric 3 — Slip Root Cause Taxonomy

For every ticket that was planned but not delivered, classify the root cause:

```
SLIP TAXONOMY
═════════════
[SCOPE_EXPANDED]   — ticket grew beyond its original definition during sprint
[TECH_UNDERESTIMATED] — took significantly longer than estimated
[EXTERNAL_BLOCK]   — blocked on another team, third party, or data dependency
[RESOURCE_UNAVAILABLE] — engineer pulled away, sick, or reallocated
[VOLUNTARILY_DEPRIORITISED] — PM or team decided it wasn't worth completing
[DOD_UNCLEAR]      — shipped but failed QA or acceptance criteria
[CARRYOVER_CHRONIC] — was already carried over from prior sprint(s)

This sprint's slip breakdown:
  [SCOPE_EXPANDED]:         [N] tickets ([X pts])
  [TECH_UNDERESTIMATED]:    [N] tickets ([X pts])
  [EXTERNAL_BLOCK]:         [N] tickets ([X pts])
  [RESOURCE_UNAVAILABLE]:   [N] tickets ([X pts])
  [DEPRIORITISED]:          [N] tickets ([X pts])
  [DOD_UNCLEAR]:            [N] tickets ([X pts])
  [CARRYOVER_CHRONIC]:      [N] tickets ([X pts])

Dominant slip cause: [category] — [what this implies]
```

---

## Metric 4 — Estimation Bias

Is the team consistently over- or under-estimating?

```
ESTIMATION BIAS ANALYSIS
════════════════════════
For completed tickets with both planned and actual estimates:

Avg planned points per ticket: [X]
Avg actual effort (proxy: time-in-progress): [X]

By ticket type:
  Stories/Features:  planned [X] → actual [X]  bias: [over/under by X%]
  Bugs:              planned [X] → actual [X]  bias: [over/under by X%]
  Tech debt:         planned [X] → actual [X]  bias: [over/under by X%]

Systematic bias: [Yes — team consistently underestimates [type] by ~X% /
                  No — estimation is relatively calibrated]

Implication for next sprint: [if bias present, note what to adjust]
```

---

## Metric 5 — Carryover Recidivism

**Carryover tickets that have been "almost done" for multiple sprints are
never purely a technical problem.** They signal avoidance.

```
CARRYOVER ANALYSIS
══════════════════
Tickets appearing in 2+ consecutive sprints: [N]

For each chronic carryover:
  [TICKET-ID]: "[Title]"
    Sprints in backlog: [N consecutive sprints]
    Current status: [status]
    Likely blocker: [from comments/status history or: unknown — needs PM context]
    Pattern: [growing in complexity / truly blocked / deprioritised but not removed /
              unclear definition of done]

📌 CONTEXT NEEDED FROM PM:
   These [N] tickets have been carried over [N] sprints. Why haven't they
   been completed or explicitly removed? Is there a technical blocker,
   an organisational constraint, or a decision that hasn't been made?
```

---

## Metric 6 — Blocked Time Analysis

```
BLOCKED TIME ANALYSIS
═════════════════════
Tickets that entered "Blocked" status: [N]
Total blocked-days across sprint:      [N days]
Longest single block:                  [N days] on [ticket] — reason: [if known]

Blocker types (from labels or comments):
  Waiting on another team:  [N days]
  Waiting on PM decision:   [N days]
  Waiting on third party:   [N days]
  Data/environment issue:   [N days]
  Unclear/unlabelled:       [N days]

Impact of blocking on sprint velocity: ~[X%] of sprint capacity lost to blocks

📌 CONTEXT NEEDED FROM PM:
   [N] blocked-days is [high/moderate/low] for a sprint of this size.
   The primary blocker type was [category]. Is this a recurring dependency
   that should be planned for, or an episodic situation?
```

---

## Delivery Fidelity Output

```
╔══════════════════════════════════════════════════════╗
  DELIVERY FIDELITY REPORT — [Sprint Name]
╠══════════════════════════════════════════════════════╣

HEADLINE:
Delivered [X%] of planned work ([N]/[N] pts). Unplanned work consumed
[X%] of sprint capacity. Primary slip cause: [category].

METRICS:
  Completion rate:      [X%] ([status])
  Unplanned work:       [X%] ([status])
  Dominant slip cause:  [category]
  Estimation bias:      [present/absent — direction]
  Chronic carryover:    [N] tickets ([most concerning one])
  Blocked capacity lost:[X%]

FINDINGS:
  🔴 [Critical finding if any]
  🟡 [Warning finding if any]
  ✅ [What went well]

📌 HUMAN MOAT CONTEXT NEEDED:
  [Specific questions the data raises that only the PM can answer]
╚══════════════════════════════════════════════════════╝
```

---

# Agent 3 — Work Composition Auditor

The mix of work in a sprint tells a story about the team's health, the
product's quality, and whether strategy or reaction is driving decisions.

---

## Step 1 — Classify Every Ticket

Apply the Technical Writer skill's taxonomy (imported) plus two audit-specific additions:

```
CLASSIFICATION TAXONOMY
═══════════════════════

PRIMARY TYPE (what kind of work):
  NEW_FEATURE     — net-new capability users didn't have before
  ENHANCEMENT     — improvement to existing feature
  BUG_FIX         — corrects unintended broken behaviour
  TECH_DEBT       — internal refactor/infra/cleanup, no user-facing change
  UNCLASSIFIED    — insufficient info to classify

ORIGIN TYPE (where the work came from):
  STRATEGIC       — was in the sprint plan, came from the roadmap
  PLANNED_REACTIVE — known category of work (e.g., regular bug triage) — in plan
  UNPLANNED       — entered sprint after start, not in original plan
  ONCALL          — production incident response

Use Jira issue type + labels + ticket content + sprint entry date to classify.
When ambiguous, note the ambiguity — don't guess.
```

---

## Step 2 — Composition Dashboard

```
WORK COMPOSITION — [Sprint Name]
═════════════════════════════════

BY TYPE:
  New features:   [N] tickets ([X pts] = [X%] of sprint)
  Enhancements:   [N] tickets ([X pts] = [X%] of sprint)
  Bug fixes:      [N] tickets ([X pts] = [X%] of sprint)
  Tech debt:      [N] tickets ([X pts] = [X%] of sprint)
  Unclassified:   [N] tickets ([X pts] = [X%] of sprint)

BY ORIGIN:
  Strategic (from roadmap): [X%]
  Planned reactive:         [X%]
  Unplanned:                [X%]
  On-call / incident:       [X%]

STRATEGIC vs. REACTIVE SPLIT:
  Strategic work: [X%]
  Reactive work:  [X%] (planned_reactive + unplanned + oncall)
```

---

## Step 3 — Benchmark Against Healthy Composition

These are reference ranges. Deviation is not inherently bad — it needs context.
Flag deviations and ask for context; don't declare them problems.

```
COMPOSITION BENCHMARK
═════════════════════
Category          This Sprint   Typical Healthy Range   Status
─────────────────────────────────────────────────────────────────
New features          [X%]         30–50%               [✅/🟡/🔴]
Enhancements          [X%]         15–25%               [✅/🟡/🔴]
Bug fixes             [X%]         10–20%               [✅/🟡/🔴]
Tech debt             [X%]         10–20%               [✅/🟡/🔴]
Unplanned work        [X%]         <15%                 [✅/🟡/🔴]

NOTE: "Healthy range" is a reference, not a rule. A team deliberately running
a "quality sprint" (high bug fix + tech debt) is making a strategic choice,
not failing. The PM's intent matters more than the benchmark.
```

---

## Step 4 — Invisible Work Detection

Work that happened but isn't in Jira. Proxied by capacity anomalies:

```
INVISIBLE WORK SIGNALS
══════════════════════

Velocity gap: team closed [N pts] but nominal capacity was [N pts]
Gap = [X pts] — potential invisible work

Signals that invisible work occurred:
  ☐ Low-velocity week with no tickets closed (meetings, coordination)
  ☐ Engineers active in Jira comments but no ticket progress
  ☐ On-call rotation period with no incident tickets
  ☐ Feature launch week (demo prep, documentation, stakeholder review)
  ☐ Hiring/interview week for team members

Estimated invisible work: [X pts or hours — or: insufficient data to estimate]

📌 CONTEXT NEEDED FROM PM:
   Was there significant work this sprint that isn't reflected in Jira?
   (Examples: production support, interviews, heavy cross-team coordination,
   a major customer meeting, a launch event.) This helps explain the velocity
   gap without over-indexing on metrics.
```

---

## Work Composition Output

```
╔══════════════════════════════════════════════════════╗
  WORK COMPOSITION REPORT — [Sprint Name]
╠══════════════════════════════════════════════════════╣

HEADLINE:
[X%] strategic, [X%] reactive. The team's effort was [dominated by /
evenly split between / mostly focused on] [dominant category].

COMPOSITION:
  New features: [X%] | Enhancements: [X%] | Bugs: [X%] | Debt: [X%]
  Strategic: [X%] | Reactive: [X%]

FLAGS:
  🔴 [Any category significantly outside benchmark — with context ask]
  🟡 [Any category worth watching]
  ✅ [What the composition shows went well]

INVISIBLE WORK: [Detected / Not detected / Insufficient data]

📌 HUMAN MOAT CONTEXT NEEDED:
   [Specific questions about composition the PM needs to answer]
╚══════════════════════════════════════════════════════╝
```