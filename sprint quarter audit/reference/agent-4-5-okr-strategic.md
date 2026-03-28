# Agent 4 — OKR Impact Assessor

The hardest analytical agent. Answers: did this sprint's work actually
move the metrics, or just generate output?

---

## Step 1 — Ticket → OKR Traceability

Apply the OKR mode selected at intake.

### MODE A — Semantic Inference

For each delivered ticket, read its title + description + epic link.
Compare to each stated OKR/KR using semantic matching:

```
Matching rules:
  STRONG MATCH:   Ticket explicitly mentions the metric, user segment,
                  or specific outcome described in the KR.
                  Example: KR = "Increase transfer completion rate"
                           Ticket = "Fix drop-off on transfer confirmation screen"
                  → STRONG MATCH to KR1

  MODERATE MATCH: Ticket works on a flow or feature that plausibly
                  affects the KR, but doesn't name the metric.
                  Example: Ticket = "Redesign payment summary screen"
                  → MODERATE MATCH (contributes to transfer experience but
                    could affect other metrics too)

  WEAK MATCH:     Ticket is in the same product area but connection to
                  KR is speculative.

  NO MATCH:       Cannot plausibly connect to any stated OKR.
                  → Classified as "orphaned work"

Flag all inferences: "Inferred — [reason for match]"
```

### MODE B — Explicit Links Only

Count only tickets with:
- A custom Jira field linking to an OKR
- An epic that is explicitly named after or linked to a KR
- A label matching the OKR naming convention (ask PM what convention they use)

All other tickets → "Orphaned work (no explicit OKR link)"

---

## Step 2 — OKR Coverage Matrix

```
OKR COVERAGE MATRIX
════════════════════

For each KR:
  KR1: [statement]
  ─────────────────
  Tickets linked:        [N] ([X story points])
  Work nature:           [describe what was actually done for this KR]
  Was this KR the focus  [primary focus / secondary / incidental / not addressed]
  of the sprint?

  KR2: [statement]
  ─────────────────
  [same format]

COVERAGE SUMMARY:
  KRs with meaningful work (≥10% of sprint capacity): [N of N total KRs]
  KRs with token work (<5% capacity):                 [N] — [list which]
  KRs with no work at all:                            [N] — [list which — flag]
  Orphaned work (no OKR):                             [X%] of sprint capacity

📌 CONTEXT NEEDED FROM PM:
   [List the KRs with no work.] Were these intentionally deprioritised this
   sprint? Or did this sprint drift away from them without a deliberate decision?
```

---

## Step 3 — Output Gap Analysis

**This is the most important finding in the entire audit.**

The output gap = the distance between "we shipped X tickets" and
"the metric moved Y% toward target."

```
OUTPUT GAP ANALYSIS
════════════════════

For each KR where metric data is available:

KR1: [statement]
  Metric: [name] | Start: [X] | End: [Y] | Target: [Z]
  Movement: [+/- amount] ([X% toward target / away from target / flat])
  
  Story points delivered toward this KR: [N pts]
  Expected metric impact of that work: [PM's hypothesis or: not stated]
  Actual metric impact: [measured / unmeasurable]
  
  Output gap verdict:
    [IMPACT CONFIRMED]  — metric moved in right direction, work was relevant
    [OUTPUT ONLY]       — work shipped but metric unmeasured or unchanged
    [MISMATCH]          — metric moved but not in the direction the work targeted
    [COUNTERPRODUCTIVE] — metric moved away from target during this sprint
  
  If MISMATCH or OUTPUT ONLY:
  📌 CONTEXT NEEDED FROM PM:
     The [metric] didn't move despite [N pts] of work targeting it.
     Was the metric expected to lag (effect shows up in future sprints)?
     Was the hypothesis about what drives this metric incorrect?
     Or is the metric measurement itself the issue?
```

---

## Step 4 — The Orphaned Work Problem

```
ORPHANED WORK ANALYSIS
══════════════════════

Tickets with no OKR connection: [N] ([X%] of sprint capacity / [X pts])

Orphaned ticket list:
  [TICKET-ID] "[Title]" — [X pts] — Origin: [strategic/unplanned/reactive]
  [TICKET-ID] "[Title]" — [X pts] — Origin: [...]

Interpretation by origin:
  If strategic + no OKR link: suggests roadmap items aren't connected to OKRs
    → Is this deliberate (some work is strategically important but not measured)?
    → Or is OKR hygiene the issue?
  
  If unplanned + no OKR link: normal — reactive work often isn't OKR-tagged
    → But if this is >20% of capacity, the reactive work is crowding out OKR work

📌 CONTEXT NEEDED FROM PM:
   [X%] of this sprint's capacity went to work with no connection to stated OKRs.
   Is there a category of "strategically important but not measured" work
   that explains this? Or should we be tagging this work to OKRs?
```

---

## OKR Impact Output

```
╔══════════════════════════════════════════════════════╗
  OKR IMPACT REPORT — [Sprint Name]
╠══════════════════════════════════════════════════════╣

HEADLINE:
[X%] of delivered work connected to stated OKRs. Of [N] key results,
[N] received meaningful effort. [N] had no work directed at them this sprint.

OKR LINKAGE:
  OKR-connected work:    [X%]
  Orphaned work:         [X%]
  OKR mode used:         [Semantic / Explicit]

METRIC MOVEMENT:
  KR1: [moved +X% toward target / flat / moved away]
  KR2: [moved +X% toward target / flat / moved away]
  [etc.]

OUTPUT GAP: [Large / Moderate / Small / Verified impact]

📌 CONTEXT NEEDED: [3 most important questions]
╚══════════════════════════════════════════════════════╝
```

---

# Agent 5 — Strategic Coherence Checker (QUARTER AUDIT ONLY)

Quarter-level question: does this quarter's work, taken in aggregate,
advance the stated strategic objective — or did tactical reactive work
dilute the quarter's intent?

---

## Roadmap Drift Score

```
ROADMAP DRIFT ANALYSIS
══════════════════════

Commitments on roadmap for this quarter: [N features]
Delivered from roadmap:                  [N] ([X%])
Planned but not delivered:               [N] ([X%])
Delivered but not on roadmap:            [N] ([X%])

Drift by dimension:
  Feature drift:  [N features different from committed] — [high/med/low]
  Timing drift:   [N features from prior quarter finally delivered] — [high/med/low]
  Priority drift: [N high-priority items deferred, lower-priority shipped] — [high/med/low]

Roadmap fidelity score: [X%]
  ≥80%: Strong — team delivered on its commitments
  60-79%: Moderate — meaningful drift, investigate causes
  40-59%: Concerning — less than half of roadmap delivered as planned
  <40%: Critical — the roadmap bore little relationship to what shipped
```

---

## Theme Coherence Test

**Could you write a two-sentence quarter summary a customer would care about?**

```
THEME COHERENCE TEST
════════════════════

Themes present in quarter's shipped work (derived from epics/features):
  Theme 1: [name] — [N features / X pts]
  Theme 2: [name] — [N features / X pts]
  Theme 3: [name] — [N features / X pts]
  Other/miscellaneous: [X pts]

Theme coherence:
  [COHERENT]   — shipped work tells one clear story
  [FRAGMENTED] — work spans multiple disconnected themes
  [SCATTERED]  — no discernible thematic pattern

Draft quarter summary (coherent narrative test):
  "This quarter, [team] focused on [theme 1] to [outcome 1].
   Additionally, [theme 2] work improved [outcome 2]."

Does this sentence describe the actual work accurately? [yes / partially / no]
If no: the quarter's work lacks coherent narrative — likely reactive dilution.
```

---

## The "What We Didn't Build" Analysis

Most audits only look at what slipped. This agent examines what was never started.

```
UNSTARTED ROADMAP COMMITMENTS
══════════════════════════════

Features on Q roadmap that were neither delivered nor carried over:
[Feature 1] — Priority: [H/M/L] — OKR link: [yes/no]
[Feature 2] — Priority: [H/M/L] — OKR link: [yes/no]

For each unstarted high-priority item:
  Was there an explicit decision to deprioritise it? [yes/no/unknown]
  Was it crowded out by reactive work? [evidence]
  Is it now on next quarter's roadmap? [yes/no/unknown]

📌 CONTEXT NEEDED FROM PM:
   [Feature X] was on the Q[N] roadmap at [H/M] priority but was never started.
   Was there a deliberate decision to defer it, or did it get crowded out?
   If deferred — is there a record of that decision, or did it just quietly drop?
```

---

## Quarter Narrative Integrity

```
QUARTER NARRATIVE INTEGRITY
════════════════════════════

Stated objective at quarter start: "[objective statement if provided]"

Narrative delivery assessment:
  Work toward stated objective: [X%] of quarter capacity
  Reactive work (not toward objective): [X%]
  Work toward other objectives: [X%]

Integrity verdict:
  [DELIVERED]   — quarter's work clearly advances the stated objective
  [DILUTED]     — objective partially advanced, reactive work consumed >30% of capacity
  [DRIFTED]     — objective not meaningfully advanced despite it being stated
  [PIVOTED]     — team deliberately shifted focus (this is fine if explicit)

📌 CONTEXT NEEDED FROM PM:
   The data shows [X%] of Q capacity went toward [objective]. The remaining
   [X%] was [reactive / toward other objectives / unclassified]. Is this
   drift intentional (market changed, priority shifted) or unintentional
   (reactive work accumulated without a deliberate decision)?
```

---

## Strategic Coherence Output

```
╔══════════════════════════════════════════════════════╗
  STRATEGIC COHERENCE REPORT — Q[N]
╠══════════════════════════════════════════════════════╣

ROADMAP FIDELITY: [X%] ([status])
THEME COHERENCE: [Coherent / Fragmented / Scattered]
NARRATIVE INTEGRITY: [Delivered / Diluted / Drifted / Pivoted]

KEY FINDINGS:
  🔴 [Critical strategic drift if any]
  🟡 [Pattern worth watching]
  ✅ [Where the quarter held together strategically]

WHAT WE DIDN'T BUILD:
  [Top 3 unstarted high-priority items with context questions]

📌 HUMAN MOAT CONTEXT NEEDED:
  [The 2–3 questions that only org-aware PM judgment can answer]
╚══════════════════════════════════════════════════════╝
```