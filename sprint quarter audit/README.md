# PM Sprint & Quarter Audit

> **A three-pass forensic audit. Not a feelings retro. A data investigation
> that tells you whether your team is actually getting better.**

A multi-agent skill that audits sprint and quarter delivery across three
sequential passes: artifact quality (did we write good tickets?), execution
quality (did we run the sprint well?), and outcomes (did the work add up?).

Now includes CodeRabbit PR summary integration for implementation delta
analysis — crossing AC against what was actually built.

Built by [Kamalika Poddar](https://github.com/kamalikap)

---

## Three Passes, One Truth

```
PASS 1 — ARTIFACT QUALITY          PASS 2 — EXECUTION QUALITY
────────────────────────            ──────────────────────────
A1: Ticket classification           B1: Bug classification
A2: Description depth scoring           (functional/technical/regression)
A3: AC edge case coverage           B2: Sprint board flow analysis
A4: Grooming depth                  B3: Spillage root cause (per-ticket)
A5: Estimation calibration          B4: Review checkpoint quality
                                    B5: Implementation delta (CodeRabbit)

                    PASS 3 — OUTCOMES & IMPROVEMENT
                    ────────────────────────────────
                    C1: Delivery fidelity
                    C2: Work composition
                    C3: OKR impact
                    C4: Strategic coherence (quarter only)
                    C5: Retro accountability + sprint-over-sprint
                    C6: Cross-sprint patterns (6-sprint history)
                    C7: Uncomfortable truths (all 3 passes)
```

---

## What's New vs Previous Version

| Capability | Previous | This version |
|---|---|---|
| Ticket type accuracy check | ✗ | ✓ A1 |
| Description depth scoring | ✗ | ✓ A2 |
| AC edge case coverage | ✗ | ✓ A3 |
| Technical design depth | ✗ | ✓ A4 |
| Estimation process + accuracy | Partial | ✓ A5 |
| Bug type classification | ✗ | ✓ B1 (functional/technical/regression) |
| Board flow + regressions | ✗ | ✓ B2 |
| Per-ticket spillage root cause | Partial | ✓ B3 (MECE taxonomy) |
| Code review substantiveness | ✗ | ✓ B4 |
| AC vs implementation delta | ✗ | ✓ B5 (CodeRabbit) |
| Retro accountability | ✗ | ✓ C5 — did last retro's actions land? |
| Sprint-over-sprint trends | Partial | ✓ C5 — all dimensions tracked |
| Retro quality audit | ✗ | ✓ C5c — were retro items data-grounded? |

---

## CodeRabbit Integration

Pass 2 B5 cross-references your AC against what was actually implemented,
using the CodeRabbit PR summary as the implementation source of truth.

**Why CodeRabbit summaries (not raw diffs):**
Raw diffs are noisy and hundreds of lines. CodeRabbit summaries are already
translated into plain English — directly comparable to AC statements.

**How to provide them:**
At the audit intake, paste the CodeRabbit summary from the **merged PR**
for each ticket you want checked. Copy from the PR page after merge.
Takes 20–30 seconds per ticket — worth it for the findings it surfaces.

**Also works with:** GitHub Copilot PR summaries, Graphite, LinearB,
manually written PR descriptions (lower confidence).

**Future:** Full automation via Jira→GitHub→CodeRabbit API chain is
documented in the implementation delta reference file.

---

## Retro Accountability

Paste last sprint's retro action items at intake.
The audit will cross-reference each item against this sprint's data and
tell you exactly which items produced measurable change, which produced
no change, and which made things worse.

A retro effectiveness score is produced:
- HIGH: >60% of action items demonstrably improved
- MEDIUM: 30–60% improved  
- LOW: <30% improved
- PERFORMATIVE: 0% improved — the retro produced items nobody acted on

---

## File Structure

```
pm-sprint-audit/
├── SKILL.md                                    # Orchestrator + 3-pass routing
├── README.md                                   # This file
└── references/
    ├── agent-1a-sprint-ingestion.md            # Extended: ticket content + changelog
    ├── agent-1b-roadmap-ingestion.md           # All roadmap tool types
    ├── agents-1c-1d-okr-quality.md             # OKR intake + quality signals
    ├── pass-1-artifact-quality.md              # A1–A5 rubric engine (NEW)
    ├── pass-2-execution-quality.md             # B1–B4 board flow + bugs (NEW)
    ├── pass-2-implementation-delta.md          # B5 CodeRabbit integration (NEW)
    ├── agents-2-3-delivery-composition.md      # C1, C2 — delivery + composition
    ├── agents-4-5-okr-strategic.md             # C3, C4 — OKR + strategic coherence
    ├── pass-3-retro-improvement.md             # C5 — retro accountability (NEW)
    ├── agents-6-7-patterns-truths.md           # C6, C7 — patterns + truths (updated)
    └── agent-8-output-artifacts.md             # 8A–8F outputs (updated with 8A, 8B)
```

---

## Output Artifacts

| Artifact | Audience | When produced |
|---|---|---|
| 8A Ticket Quality Report | PM + tech lead + engineers | Every sprint |
| 8B Board Flow Report | PM + tech lead | Every sprint |
| 8C Team Retro Brief | Engineering team | Every sprint |
| 8D Exec Audit Report | CPO / VP Product | Quarter audit |
| 8E Next Sprint Calibration | PM + team | Every sprint |
| 8F Quarter Report | PM + leadership | Quarter audit |

---

## Author

**Kamalika Poddar**
12 years in fintech — core banking, UPI, payment aggregators, account aggregators,
wealth tech, and cross-border payment rails.

[GitHub](https://github.com/kamalikap) · [LinkedIn](https://linkedin.com/in/kamalikap)

---

## License
MIT — free to use, fork, and build on. Attribution appreciated.
