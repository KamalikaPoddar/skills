---
name: pm-problem-structuring
description: >
  The PM Problem Structuring skill. Invoke this skill whenever a product manager
  needs to rigorously define, decompose, or structure a product problem before
  deciding what to build. Triggers on: "help me structure this problem", "I need
  to define the problem", "what is the root cause of", "help me frame this
  opportunity", "I need to build a hypothesis", "write a problem statement",
  "what jobs does the user need done", "size this opportunity", "create a 2x2",
  "help me think through this problem", "build an issue tree", "what are
  competing hypotheses for", "I have a fuzzy problem I need to sharpen",
  "I need to present a problem to stakeholders", "what is the JTBD here",
  or any variation where a PM is trying to understand a problem deeply before
  committing to a solution. This skill is NOT for writing PRDs or building
  prototypes — it is exclusively for the problem-definition and
  opportunity-structuring phase of PM work. Always invoke at the start of
  any discovery or strategy session.
---

# PM Problem Structuring

A multi-agent skill that takes a fuzzy signal — a metric drop, a customer
complaint cluster, a strategic bet, a stakeholder request — and turns it into
a rigorously structured, evidence-grounded problem brief ready for solution work.

This skill applies McKinsey-grade hypothesis discipline, Teresa Torres'
opportunity mapping, Clayton Christensen's JTBD, and causal business impact
modelling — in the right sequence, with stress tests baked in at every stage.

**The skill enforces the sequence.** You cannot generate hypotheses before you
have root causes. You cannot size the opportunity before you have a real problem.
Every agent's output quality depends on the prior agent having done its job.

---

## What This Skill Produces

```
INPUT                         AGENTS                              OUTPUT
──────────────────────        ──────────────────────────────      ─────────────────────────────
Fuzzy signal:            →   1. Problem Definer              →   Sharp problem statement
metric drop / complaint       2. Root Cause Analyst          →   Causal chain + fishbone map
/ stakeholder ask /      →   3. JTBD Frame                  →   Job stories + four forces
strategic bet            →   4. Opportunity Mapper           →   OST + ranked opportunity space
                         →   5. Hypothesis Generator         →   4 MECE hypotheses + kill tests
                         →   6. Business Impact Tree         →   Impact equation + sized model
                         →   7. 2×2 Strategist               →   Decision matrix (derived axes)
                         →   8. Synthesizer                  →   One-page brief + HMW + metrics
```

---

## Step 0 — Intake

When invoked, ask in ONE message:

1. **What is the signal?** (metric, complaint, stakeholder ask, or strategic question)
2. **What do you already know?** (data, research, prior hypotheses — even rough ones)
3. **What decision does this analysis need to support?** (roadmap, go/no-go, investment case)
4. **What is the user segment and industry/domain?**

Then confirm: *"I'll run the problem through 8 structured agents in sequence.
Each builds on the last. You can stop after any agent if you have what you need,
or run the full sequence for a complete one-page brief."*

---

## The Five Failure Modes This Skill Prevents

Before running any agent, check for these and flag them immediately:

| Failure mode | Signal | Fix |
|---|---|---|
| **Symptom treated as problem** | Statement describes an observable metric, not a root cause | Run Agent 1 before anything else |
| **Solution in problem disguise** | Problem statement implies a specific product change | Reframe to what user needs, not what to build |
| **Single hypothesis tunnel** | PM has already decided the cause | Force Agent 5 to generate 3 more competing hypotheses |
| **Sizing without causality** | Market size quoted with no connection to metric movement | Run Agent 6 full model before accepting any numbers |
| **Generic 2×2 axes** | "Impact vs Effort" used without interrogating whether Effort is the right axis | Run Agent 7 with axis justification required |

---

## Agent 1 — Problem Definer

**Read:** `references/agent-1-problem-definer.md`

The hardest and highest-leverage agent. Challenges the framing itself.

Produces:
- SCQA breakdown (Situation → Complication → Question → Answer/hypothesis)
- Symptom vs. problem test
- Solution-in-disguise test
- One-sentence sharpened problem statement in the canonical format
- Counterfactual check: "What would the world look like if this didn't exist?"

**Hard gate:** If the problem statement is still a symptom or solution after
Agent 1, do NOT proceed to Agent 2. Return to Agent 1 and sharpen further.

---

## Agent 2 — Root Cause Analyst

**Read:** `references/agent-2-root-cause-analyst.md`

Two complementary techniques: depth (Five Whys — one causal chain followed all
the way down) and breadth (Fishbone — all causal categories mapped simultaneously).

Produces:
- Five Whys chain (3–5 levels, each step as a testable claim)
- Fishbone map across 6 product-adapted categories
- Root cause ranking by likelihood, impact, and actionability
- Correlation vs. causation flags
- Pre-mortem on the root cause: "If we're wrong about this, what evidence is missing?"

---

## Agent 3 — JTBD Frame

**Read:** `references/agent-3-jtbd-frame.md`

Three layers: functional (what task), emotional (how they want to feel),
social (how they want to be perceived). Most PM work stops at layer one.

Produces:
- Functional + emotional + social job decomposition
- Job story: `When [situation], I want to [motivation], so I can [outcome]`
- Four Forces: Push + Pull + Anxiety + Habit
- Non-obvious competition map (what else is hired for this job)
- Hiring frequency and current solution satisfaction
- The "firing" question: when do users actively abandon the current solution?

---

## Agent 4 — Opportunity Mapper

**Read:** `references/agent-4-opportunity-mapper.md`

Teresa Torres' OST discipline applied strictly: opportunities are user needs,
not features. The agent enforces this framing throughout.

Produces:
- Opportunity Solution Tree: Outcome → Opportunity clusters → Sub-opportunities
- Opportunity framing check: each stated as a gap, not a solution
- Opportunity ranking on 4 dimensions (sizing, market, company fit, satisfaction)
- Adjacent opportunity space: connected problems that could become platform plays
- Breadth test: what's missing from the opportunity space?

---

## Agent 5 — Hypothesis Generator

**Read:** `references/agent-5-hypothesis-generator.md`

McKinsey/BCG hypothesis discipline: 4 competing MECE hypotheses, kill criteria
for each, and a steel-man obligation on the hypothesis the PM least believes.

Produces (root cause hypotheses):
- 4 MECE hypotheses for why the problem exists
- Evidence that would confirm vs. kill each
- Kill criteria matrix: cheapest/fastest way to eliminate 3 of 4

Produces (solution hypotheses):
- 4 MECE hypotheses at different intervention levels
- Including one non-obvious hypothesis, one "do nothing" hypothesis
- Steel man for the least-favoured hypothesis

---

## Agent 6 — Business Impact Tree

**Read:** `references/agent-6-business-impact-tree.md`
**Also read:** `shared-agents/business-impact-calculator.md`

Runs the full Business Impact Calculator. Produces a causally-connected impact
model, not just a TAM slide. Every number has a source and a sensitivity check.

Produces:
- Impact equation (causal, not correlational)
- TAM/SAM/SOM with methodology and source for each
- Bottom-up model and reconciliation with top-down
- Sensitivity analysis: top 3 load-bearing assumptions
- Time horizon (Year 1 / Year 3 / Year 5)
- Four reality checks: 1% rule, CAC sanity, So What test, competitive deflation

---

## Agent 7 — 2×2 Strategist

**Read:** `references/agent-7-2x2-strategist.md`

The 2×2 is the output of analysis, not the input. This agent derives axes
from what the prior 6 agents found — then justifies them.

Produces:
- Opportunity prioritization 2×2 (axes derived from the two most contested
  trade-offs found in Agents 1–6)
- Solution space 2×2 (mapping the four hypothesised solutions)
- Risk profile 2×2 (effort to validate vs. downside if wrong)
- Axis justification: why these axes for this specific problem
- Blank quadrant test: if a quadrant is empty, the axes are probably wrong

**Hard rule:** The agent must argue why "Impact vs Effort" is or isn't the
right choice before using it. In many strategic problems, it isn't.

---

## Agent 8 — Synthesizer

**Read:** `references/agent-8-synthesizer.md`

Takes all prior output and produces the communication artifacts. Every section
must pass the "So What" test before it's included.

Produces:
- One-sentence refined problem statement (sharpened by 7 rounds of analysis)
- One-page problem brief (stakeholder-ready)
- Three How Might We statements (one per major opportunity cluster)
- Success metric definition (baseline, target, measurement method)
- Open questions and load-bearing assumptions
- Recommended validation plan (2–3 cheapest/fastest tests to kill wrong hypotheses)

---

## Sequence Enforcement

```
Agent 1 (Problem Definition)
  │
  └─► Hard gate: must have a real problem, not a symptom or solution
          │
Agent 2 (Root Cause)
  │
Agent 3 (JTBD)       ← agents 2 and 3 can run in parallel
  │
Agent 4 (Opportunity Mapping)
  │
Agent 5 (Hypotheses)
  │
Agent 6 (Business Impact)
  │
Agent 7 (2×2)
  │
Agent 8 (Synthesis)
```

Shortcuts by use case:
- **"I just need a sharp problem statement"** → Agent 1 only
- **"I need to prep for a discovery interview"** → Agents 1 + 3
- **"I need hypotheses for a data investigation"** → Agents 1 + 2 + 5
- **"I need a one-pager for stakeholders"** → Full sequence → Agent 8
- **"I need to size an opportunity for a business case"** → Agents 1 + 6

---

## Reference Files

| File | Agent |
|---|---|
| `references/agent-1-problem-definer.md` | Agent 1 |
| `references/agent-2-root-cause-analyst.md` | Agent 2 |
| `references/agent-3-jtbd-frame.md` | Agent 3 |
| `references/agent-4-opportunity-mapper.md` | Agent 4 |
| `references/agent-5-hypothesis-generator.md` | Agent 5 |
| `references/agent-6-business-impact-tree.md` | Agent 6 |
| `references/agent-7-2x2-strategist.md` | Agent 7 |
| `references/agent-8-synthesizer.md` | Agent 8 |
| `shared-agents/business-impact-calculator.md` | Agent 6 (shared) |
| `shared-agents/industry-context-agent.md` | Agent 1, 6 (shared) |
