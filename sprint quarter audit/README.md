# PM Sprint & Quarter Audit

> **A forensic investigation into sprint and quarter delivery. Not a feelings
> retrospective. A data-grounded audit that finds what retros miss.**

A multi-agent skill that cross-references sprint execution data, roadmap commitments,
OKRs, and 6 sprints of history to surface: what was actually delivered, whether it
moved the metrics, whether the quarter's work adds up to anything coherent, and the
uncomfortable patterns the official narrative tends to omit.

Built by [Kamalika Poddar](https://github.com/kamalikap)

---

## Why This Skill Exists

The image that sparked it says it perfectly:

> *"I find the assumption hole your PRD is quietly built on. Most PMs never
> stress-test their own bets at all."*
> *"I run RICE, Kano, MoSCoW simultaneously and show where they conflict."*

The audit skill does the same thing for delivery:

- **Cross-references 6 sprints of data simultaneously** — without the fatigue
  or anchoring bias that affects human retrospectives
- **Separates output from outcome** — "we shipped 47 tickets" vs "the metric
  moved 8% toward target" are not the same statement
- **Generates uncomfortable data-grounded observations** — the patterns the data
  shows that the official narrative doesn't say
- **Respects the human moat** — every major finding is paired with a specific
  question only the PM can answer (org context, team dynamics, decisions that
  weren't captured in Jira)

---

## Two Modes

### Sprint Audit
Deep forensics on a single sprint. Use: weekly retro, mid-sprint health check,
or when something felt off but you can't name what.

Runs: Ingestion (1A + 1B + 1C + optional 1D) → Delivery Fidelity (2) →
Work Composition (3) → OKR Impact (4) → Patterns if history available (6) →
Uncomfortable Truths (7) → Team Brief (8A) + Next Sprint Inputs (8C)

### Quarter Audit
Full strategic health assessment of the quarter. Use: quarterly business review,
board prep, annual planning, or when the quarter felt busy but you're not sure
what it added up to.

Runs: Everything. All 8 agents. Produces 8A + 8B + 8C + 8D.

---

## The Five Things This Audit Finds That Retros Miss

| Finding | Why retros miss it |
|---|---|
| **Unplanned work ratio** | Teams don't count tickets that entered mid-sprint when calculating "how much we delivered" |
| **OKR orphaned work** | Nobody explicitly asks "what % of this sprint had nothing to do with our stated objectives?" |
| **Carryover recidivism** | Retros address the current sprint; chronic carryover requires looking across sprints |
| **The output gap** | Retros celebrate shipping; the gap between shipping and moving metrics is rarely examined |
| **Strategic drift without a decision record** | Items quietly drop off the roadmap without being explicitly deferred — the data shows it, the conversation doesn't |

---

## Data Sources Supported

### Sprint Data
| Tool | Connection |
|---|---|
| Jira | MCP (auto) or CSV export |
| Linear | MCP (auto) or CSV export |
| GitHub Projects | Export or paste |
| Any other | Paste / manual summary |

### Roadmap Data
| Tool | Connection |
|---|---|
| Aha! | MCP or CSV export |
| Confluence | MCP or paste page content |
| Excel / Google Sheets | File upload or Google Sheets MCP |
| Notion | MCP or paste database |
| Linear roadmap | MCP or paste |
| Productboard | CSV export or paste |
| No tool / prose | Paste directly — skill normalises any format |

### OKR Data
| Mode | Method |
|---|---|
| Semantic inference | No setup — skill reads ticket descriptions |
| Explicit links | Requires Jira→OKR tagging in your workflow |
| Manual OKR input | Paste your OKRs with metric baselines |

---

## File Structure

```
pm-sprint-audit/
├── SKILL.md                                    # Orchestrator + mode routing
├── README.md                                   # This file
└── references/
    ├── agent-1a-sprint-ingestion.md            # Jira / Linear / GitHub / paste
    ├── agent-1b-roadmap-ingestion.md           # All 6 roadmap tool types
    ├── agents-1c-1d-okr-quality.md             # OKR intake + quality signals
    ├── agents-2-3-delivery-composition.md      # Delivery fidelity + work mix
    ├── agents-4-5-okr-strategic.md             # OKR impact + strategic coherence
    ├── agents-6-7-patterns-truths.md           # 6-sprint patterns + uncomfortable truths
    └── agent-8-output-artifacts.md             # Team brief + exec report + calibration + Q retro
```

---

## The Human Moat Protocol

Every significant finding in this audit ends with:

```
📌 CONTEXT NEEDED FROM PM:
   The data shows [finding]. What's the explanation?
```

Claude sees:
- That the enterprise feature slipped for the 4th sprint in a row
- That OKR2 received 2% of sprint capacity across 6 sprints despite being Priority 1
- That velocity declined 22% over the quarter while bug-fix % rose 18%

Only the PM knows:
- That the CTO and CPO haven't aligned on the enterprise feature's direction
- That OKR2 was effectively deprioritised in an informal leadership conversation that
  wasn't captured anywhere
- That two senior engineers left the team in Q2 and the replacement ramp took 6 weeks

The audit is only complete when both layers are present. Claude provides the
data skeleton. The PM provides the org-aware tissue.

---

## OKR Mode Explained

At the start of every audit, you choose:

**Semantic Inference (Mode A):** Claude reads ticket descriptions and infers OKR
connections using language matching. No setup required. Good for teams without
formal OKR tagging in Jira. Higher coverage, some noise — all inferences are
explicitly flagged.

**Explicit Links Only (Mode B):** Claude counts only tickets with a documented
OKR field, matching epic label, or explicit initiative link. Everything else is
"orphaned work." Lower noise, reveals exactly how disciplined OKR tagging is.
Good for teams that claim strong OKR hygiene — the audit will confirm or challenge that.

You can use Mode A to get started and switch to Mode B as OKR hygiene improves.

---

## Example: What a Quarter Audit Might Find

**Input:** Q2 sprint data from Jira, roadmap from Confluence, OKRs from Notion.

**What the team said:** "Q2 was mostly on track. We hit our major milestones."

**What the audit found:**

- Roadmap fidelity: 54% — the two features that shipped were planned for Q1; Q2's
  flagship commitment (the enterprise tier) was not started
- OKR2 ("Improve API developer experience"): received 3% of quarter capacity across
  4 sprints — effectively unfunded despite being stated Priority 1
- Unplanned reactive work: averaged 34% of sprint capacity — above the 20% threshold
  where reactive culture is classified as "concerning" for 3 of 4 sprints
- Output gap on KR1: 28 pts of work shipped toward the metric; metric moved +2% vs
  target of +15% — hypothesis about what drives this KR requires revisiting

**Comfortable story:** "We had a productive quarter."
**Data story:** "The quarter produced output. Strategic commitments were not delivered.
The metrics tell a different story than the ticket count."

📌 **Context needed:** Was the enterprise tier deliberately deferred after a
leadership conversation? Was there a customer situation that drove the reactive
work spike? The data raises the question; only the PM can answer it.

---

## Author

**Kamalika Poddar**
12 years in fintech infrastructure — core banking, UPI, payment aggregators,
account aggregators, wealth tech, and cross-border payment rails.

[GitHub](https://github.com/kamalikap) · [LinkedIn](https://linkedin.com/in/kamalikap)

---

## License
MIT — free to use, fork, and build on. Attribution appreciated.
