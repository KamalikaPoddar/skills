# Pass 3 — C5 — Retro Accountability & Sprint-over-Sprint Improvement

**Question: Did the improvement points from last sprint's retrospective
actually change anything this sprint? And are we improving over time?**

This is the most important agent for compounding improvement. A retro that
produces action items nobody acts on is a ceremony, not a learning system.
This agent closes the loop.

Requires: prior sprint retro output (pasted at intake by PM).
If no prior retro provided: skip retro accountability; run improvement
trend analysis only (from 6-sprint history).

---

## C5a — Retro Accountability Check

**Input: Last sprint's retro action items (pasted by PM)**

For each action item from the prior retro, find evidence in this sprint's
Pass 1, Pass 2, and Pass 3 data of whether it was addressed.

**Evidence mapping framework:**

```
For each retro action item, answer:

ACTION ITEM: "[Statement from prior retro]"
Category: [process / artifact quality / execution / communication / tooling]

Evidence check:
  What metric or data point from this sprint would confirm improvement?
  What metric would confirm the problem persists?
  
VERDICT:
  [DEMONSTRABLY IMPROVED]  — specific data shows change
  [DIRECTIONALLY IMPROVED] — data suggests progress but not conclusive
  [NO CHANGE]              — data shows same pattern as prior sprint
  [WORSE]                  — data shows the problem increased
  [UNVERIFIABLE]           — no data point in this sprint speaks to this item
  [NOT YET ACTIONED]       — item requires structural change not yet started
```

**Common retro action items and how to verify them:**

```
"Improve grooming quality"
  Verify via: Pass 1 A2/A3/A4 scores vs prior sprint
  IMPROVED if: average description + AC scores rose by ≥0.5 points
  NO CHANGE if: scores same or lower

"Reduce spillage"  
  Verify via: Pass 3 C1 (delivery fidelity)
  IMPROVED if: completion rate increased or spillage causes shifted from
               SPEC_GAP / SCOPE_EXPANDED toward EXTERNAL_DEPENDENCY
               (structural causes > PM-controllable causes = real progress)
  NO CHANGE if: completion rate flat or same slip categories

"Fix our code review process"
  Verify via: Pass 2 B4 review metrics
  IMPROVED if: avg review wait decreased, substantiveness rate increased,
               regression rate from review misses decreased
  NO CHANGE if: same wait times, same rubber-stamp rate

"Reduce reactive/unplanned work"
  Verify via: Pass 3 C2 composition — unplanned work %
  IMPROVED if: unplanned % lower this sprint
  NO CHANGE if: unplanned % same or higher

"Better bug classification / less regression"
  Verify via: Pass 2 B1 bug classification
  IMPROVED if: regression count lower, functional bug rate lower
  NO CHANGE if: same or higher rates

"Write better AC"
  Verify via: Pass 1 A3 (AC Coverage) scores
  IMPROVED if: average AC score rose, "missing AC" bug type rate lower
  NO CHANGE if: AC scores flat

"Improve estimation accuracy"
  Verify via: Pass 1 A5 estimation scores
  IMPROVED if: estimation process score rose, accuracy improved
  NO CHANGE if: same calibration error patterns
```

**Retro accountability output:**

```
╔══════════════════════════════════════════════════════════════╗
  RETRO ACCOUNTABILITY REPORT
  Prior sprint retro date: [date]
  Action items: [N total]
╠══════════════════════════════════════════════════════════════╣

ACTION ITEM [1]: "[Statement]"
  Evidence from this sprint: [specific metric or finding]
  Verdict: [DEMONSTRABLY IMPROVED / DIRECTIONALLY / NO CHANGE / WORSE / UNVERIFIABLE]
  
  If IMPROVED: "[What specifically changed — with data]"
  If NO CHANGE: "[The same pattern persists — specific evidence]"
  If WORSE: "[The problem increased — specific evidence + possible reason]"

[Repeat for each action item]

RETRO EFFECTIVENESS SCORE:
  Demonstrably improved: [N/N] ([X%])
  Directionally improved: [N/N]
  No change or worse: [N/N]

EFFECTIVENESS VERDICT:
  [HIGH]   — >60% demonstrably improved
  [MEDIUM] — 30–60% demonstrably improved  
  [LOW]    — <30% demonstrably improved
  [PERFORMATIVE] — 0% improved — retro produced action items nobody acted on

📌 CONTEXT NEEDED FROM PM:
   [For NO CHANGE items]: Was this action item assigned to someone with
   a clear completion date? Or did it remain as a vague intention?
   
   [For WORSE items]: What happened this sprint that pushed this metric
   backward despite the prior commitment to improve it?
╚══════════════════════════════════════════════════════════════╝
```

---

## C5b — Sprint-over-Sprint Improvement Analysis

**Question: Across 6 sprints, are we getting better at the things that matter?**

This requires the 6-sprint history from Agent 1A, enriched with Pass 1 and
Pass 2 scores if available for prior sprints (they won't be for the first audit
run — note this limitation and offer to establish the baseline now).

**First audit session handling:**

```
If this is the first time running this audit:
  - Current sprint establishes the baseline across all dimensions
  - Prior sprint data from Jira establishes delivery metrics (C1/C2/C3)
  - Pass 1 and Pass 2 scores CANNOT be retroactively calculated without
    ticket content (not available in Jira metadata alone)
  
  Tell PM:
  "This sprint establishes your artifact quality and execution quality
   baseline. Starting next sprint, I'll track improvement across all
   dimensions. The longer we run this audit, the richer the trends."
```

**Improvement trend dimensions (when history available):**

```
ARTIFACT QUALITY TREND (Pass 1 scores over time):
  A2 Description quality:  Sprint 1→6: [X.X → X.X → X.X → X.X → X.X → X.X]
  A3 AC Coverage:          Sprint 1→6: [X.X → X.X → X.X → X.X → X.X → X.X]
  A4 Grooming depth:       Sprint 1→6: [X.X → X.X → X.X → X.X → X.X → X.X]
  Trend: [Improving / Stable / Declining]

EXECUTION QUALITY TREND (Pass 2 metrics over time):
  Bug density (bugs/story pt): Sprint 1→6: [X → X → X → X → X → X]
  Board flow efficiency:       Sprint 1→6: [% smooth → → → → → X%]
  Review substantiveness:      Sprint 1→6: [% substantive → → → → → X%]
  Regression rate:             Sprint 1→6: [X → X → X → X → X → X]
  Trend: [Improving / Stable / Declining]

DELIVERY TREND (Pass 3 metrics over time):
  Completion rate:    Sprint 1→6: [X% → → → → → X%]
  Unplanned work %:  Sprint 1→6: [X% → → → → → X%]
  OKR-linked work %: Sprint 1→6: [X% → → → → → X%]
  Trend: [Improving / Stable / Declining]

RETRO EFFECTIVENESS TREND:
  Last 3 retro effectiveness scores: [HIGH / MEDIUM / LOW / PERFORMATIVE]
  Trend: [Improving / Stable / Declining / First audit]
```

**Improvement velocity assessment:**

```
IMPROVEMENT VELOCITY
════════════════════

Fastest improving dimension: [dimension] — [X → X over N sprints]
Slowest improving dimension: [dimension] — [flat or declining despite retro items]

Areas of consistent strength (top quartile across 6 sprints): [list]
Areas of persistent weakness (bottom quartile across 6 sprints): [list]

SYSTEMIC PROBLEMS (not improving despite multiple retro cycles):
[A finding that has appeared in every retro but data shows no improvement
 is no longer a "team issue to work on" — it's a structural or incentive
 problem that requires a different type of intervention.]

For each systemic persistent weakness:
  How many sprints has this appeared as an issue: [N]
  Has it been a retro action item: [yes / no / yes but no owner]
  Recommendation: [escalate / structural change / reframe / accept as baseline]
```

---

## C5c — Retro Quality Auditor

**Question: Were the retro points themselves grounded in data, or were they
feelings and impressions?**

A retro produces better action items when it's grounded in actual data from
Pass 1, Pass 2, and Pass 3. A retro that runs on vibes produces vague action
items that are hard to verify and easy to ignore.

This agent audits the retro *itself* — not just whether the actions were taken.

**Retro quality scoring:**

```
RETRO QUALITY DIMENSIONS (score each 1–5):

1. EVIDENCE GROUNDING (are retro points supported by data?):
5 — Every "what went wrong" point is traceable to a specific metric,
    a ticket pattern, a code review finding, or a delivery data point.
3 — Some points are data-grounded, others are impressions.
1 — All points are feelings-based. ("The sprint felt heavy." "Reviews
    were slow." — without any data behind these statements.)

2. SPECIFICITY OF ACTION ITEMS (are action items actionable?):
5 — Each action item has: a specific owner, a measurable outcome,
    and a deadline or next-sprint check-in.
    Example: "Kamalika to add AC edge case template to Jira ticket
    template by Sprint 15 start."
3 — Action items name a direction but lack owner or measurement.
    Example: "We should improve our AC writing."
1 — Action items are vague intentions.
    Example: "We need to communicate better."

3. BALANCE (both positive and negative findings):
5 — Retro includes specific evidence of what went well AND what didn't.
    Both are grounded in data, not just the bad things.
3 — Mostly covers problems; wins mentioned briefly without evidence.
1 — Pure complaint session or pure celebration — no balance.

4. ROOT CAUSE DEPTH (do action items address root causes or symptoms?):
5 — Action items address the systemic root cause found in Pass 1/2/3.
    Example: "AC gaps causing bugs" → fix: update Jira ticket template
    to require edge case section before grooming.
3 — Action items address the symptom.
    Example: "AC gaps causing bugs" → fix: "write better AC."
1 — Action items don't connect to identified root causes at all.
```

**Retro quality output:**

```
RETRO QUALITY AUDIT
════════════════════
Evidence grounding: [X/5]
Action item specificity: [X/5]
Balance: [X/5]
Root cause depth: [X/5]
RETRO QUALITY SCORE: [avg X/5]

GAPS IN THIS RETRO'S APPROACH:
  [Specific things the data shows that the retro didn't discuss]
  [Action items that address symptoms not root causes — with better alternative]

SUGGESTED RETRO ADDITIONS (based on this sprint's audit):
  [Item 1 from Pass 1/2/3 that deserved retro attention but didn't get it]
  [Item 2]

BETTER-FRAMED ACTION ITEMS:
  Original: "[vague retro action item]"
  Better:   "[specific, owned, measurable version]"
```
