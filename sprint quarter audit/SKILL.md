---
name: pm-sprint-audit
description: >
  The PM Sprint & Quarter Audit skill. Invoke this skill whenever a product
  manager needs to rigorously audit a completed sprint or quarter — not as a
  feelings-based retrospective, but as a forensic data investigation. Triggers
  on: "audit this sprint", "do a sprint retro", "review this quarter",
  "why did we miss our OKRs", "what did we actually ship", "did we deliver
  on our roadmap", "how is the team's velocity trending", "write the quarterly
  review", "analyse our sprint data", "what patterns do you see across sprints",
  "stress-test our delivery narrative", "what are we not talking about in retro",
  or any variation where a PM needs to compare what was planned vs delivered,
  connect shipped work to business outcomes, or surface patterns across multiple
  sprints. This skill runs in two modes: SPRINT AUDIT (single sprint forensics)
  and QUARTER AUDIT (strategic health across the full quarter + 6-sprint history).
  Always invoke at the start of any retrospective or audit session.
---

# PM Sprint & Quarter Audit

A multi-agent skill that forensically audits sprint and quarter delivery.
Not a feelings retrospective. A data-grounded investigation that answers:
Did we build what we said? Was it the right work? Did it move the metrics?
Does the quarter's work add up to anything coherent?

Runs in two modes:
- **SPRINT AUDIT** — deep dive on one sprint. Delivery fidelity, composition,
  OKR linkage, and immediate calibration for next sprint.
- **QUARTER AUDIT** — everything in sprint audit × the full quarter, plus
  strategic coherence analysis, 6-sprint pattern recognition, and the
  uncomfortable truths the data shows that the official narrative doesn't.

---

## Architecture

```
╔══════════════════════════════════════════════════════════════╗
║  LAYER 1 — INGESTION                                         ║
║  1A: Sprint Ingestion    ← Jira / Linear / GitHub Projects   ║
║  1B: Roadmap Ingestion   ← Aha! / Confluence / Excel /      ║
║                             Notion / Linear / paste          ║
║  1C: OKR & Metric Intake ← OKR tools / docs / manual        ║
║  1D: Quality Signals     ← Bug backlog / PRs / support       ║
╠══════════════════════════════════════════════════════════════╣
║  LAYER 2 — FOUR AUDIT LENSES                                 ║
║  2: Delivery Fidelity Auditor                                ║
║  3: Work Composition Auditor                                 ║
║  4: OKR Impact Assessor                                      ║
║  5: Strategic Coherence Checker  ← QUARTER AUDIT only       ║
╠══════════════════════════════════════════════════════════════╣
║  LAYER 3 — PATTERN INTELLIGENCE                              ║
║  6: Cross-Sprint Pattern Recognizer  ← needs 6-sprint data  ║
║  7: Uncomfortable Truth Generator                            ║
╠══════════════════════════════════════════════════════════════╣
║  LAYER 4 — OUTPUT ARTIFACTS                                  ║
║  8A: Team Retro Brief     8C: Next Sprint Calibration        ║
║  8B: Exec Audit Report    8D: Quarter Report (Q-mode only)   ║
╚══════════════════════════════════════════════════════════════╝
```

---

## Step 0 — Mode Selection & Intake

**Ask in ONE message:**

```
1. AUDIT SCOPE:
   "Sprint audit (one sprint deep-dive) or quarter audit (full quarter + patterns)?"

2. SPRINT DATA SOURCE:
   "Where does your sprint data live? Jira / Linear / GitHub Projects / other?
   If Jira is connected via MCP, I'll pull it automatically.
   Otherwise, please paste a sprint export or summary."

3. ROADMAP SOURCE:
   "Where is your roadmap? Aha! / Confluence / Notion / Excel or Sheets /
   Linear roadmap view / paste it here. I'll normalise whatever you give me."

4. OKR MODE:
   "For OKR linkage analysis, which approach:
   A) Semantic inference — I read ticket descriptions and infer OKR connections.
      Faster, no setup needed, some noise.
   B) Explicit links — I only count tickets with a documented OKR link in Jira.
      Cleaner, but unlinked tickets all become 'orphaned work.'
   Which fits how your team actually works?"

5. FOR QUARTER AUDIT ONLY:
   "How many sprints of history can you provide? I'll use up to 6 for pattern
   recognition. If fewer, I'll note the analysis depth limitation."

6. CURRENT METRIC BASELINES:
   "What are your OKRs for this period, and what were the metric values at
   sprint/quarter start? Even rough numbers help. If you don't have them,
   I'll flag OKR impact as 'unverifiable' rather than guess."
```

---

## Mode Routing

### SPRINT AUDIT MODE

Runs: 1A → 1B (current sprint context only) → 1C → 1D (optional) →
      2 → 3 → 4 → 6 (if prior sprint data available) → 7 → 8A → 8C

Skip: Agent 5 (Strategic Coherence — quarter-level only)
Skip: Agent 8D (Quarter Report)

### QUARTER AUDIT MODE

Runs: ALL agents in sequence
Requires: data from the full quarter (all sprints within it)
Ideal: 6 sprints of historical data for Agent 6
Produces: 8A + 8B + 8C + 8D

---

## The Five Things This Audit Finds That Retros Miss

1. **The unplanned work ratio** — what % of sprint effort was reactive,
   never in the plan. Most teams don't track this. They should.

2. **OKR orphaned work** — tickets that shipped but connect to no stated
   objective. Common. Usually uncomfortable. Always worth naming.

3. **Carryover recidivism** — tickets that have been "almost done" for
   3+ sprints. This is never a technical problem.

4. **The output gap** — the difference between "we shipped 47 tickets"
   and "the metric moved 8% toward target." Most sprints have a large gap.

5. **Strategic drift** — whether the quarter's work, taken in aggregate,
   advances the stated strategic objective or diluted it with reactive work.

---

## The Human Moat Protocol

Every major finding from Agents 4, 5, 6, and 7 ends with:

```
📌 CONTEXT NEEDED FROM PM:
   The data shows [finding]. What's the explanation?
   [Is there org context, a decision that wasn't captured in Jira,
    a customer situation, a team dynamic that explains this?]
```

Claude provides the data pattern. The PM provides the org-aware context.
The audit is only complete when both are present.

---

## Reference Files

| File | Agents |
|---|---|
| `references/agent-1a-sprint-ingestion.md` | 1A |
| `references/agent-1b-roadmap-ingestion.md` | 1B |
| `references/agent-1c-okr-metric-intake.md` | 1C |
| `references/agent-1d-quality-signals.md` | 1D |
| `references/agent-2-delivery-fidelity.md` | 2 |
| `references/agent-3-work-composition.md` | 3 |
| `references/agent-4-okr-impact.md` | 4 |
| `references/agent-5-strategic-coherence.md` | 5 |
| `references/agent-6-cross-sprint-patterns.md` | 6 |
| `references/agent-7-uncomfortable-truths.md` | 7 |
| `references/agent-8-output-artifacts.md` | 8A–8D |
