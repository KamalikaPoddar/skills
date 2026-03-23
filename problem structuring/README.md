# PM Problem Structuring

> **Turn a fuzzy signal into a sharp, evidence-grounded problem brief —
> before you commit a single engineer to building anything.**

A multi-agent skill for AI-native PMs that applies McKinsey-grade hypothesis
discipline, Teresa Torres' opportunity mapping, Clayton Christensen's JTBD
framework, and causal business impact modelling — in the right sequence,
with stress tests baked in at every stage.

Built by [Kamalika Poddar](https://github.com/kamalikap)

---

## Why This Skill Exists

The most expensive thing a product team can do is build the right solution to
the wrong problem. Yet most PM problem structuring is:

- Stopping at symptoms instead of root causes
- Generating one hypothesis and running with it
- Jumping to solutions before mapping the opportunity space
- Sizing markets without a causal connection to business value
- Using generic 2×2 frameworks regardless of what the problem actually requires

This skill enforces the correct sequence and builds in stress tests that most
PMs skip — not because they don't know better, but because there was no
structured process to enforce the discipline.

---

## The Five Failure Modes This Skill Prevents

| Failure mode | What it looks like | What this skill does |
|---|---|---|
| Symptom as problem | "Conversion dropped 12%" called a problem | Agent 1 blocks until a real causal statement exists |
| Solution in disguise | "We need a dashboard" called a problem | Symptom/solution test in Agent 1 |
| Single hypothesis | One root cause assumption, no alternatives | Agent 5 forces 4 MECE competing hypotheses |
| Correlation confused for causation | "Users who use Feature X retain better" | Agent 2 explicit causation tests |
| Generic 2×2 | Impact/Effort used on every decision | Agent 7 requires axis justification before any matrix |

---

## The 8-Agent Sequence

```
1. Problem Definer      — SCQA breakdown, symptom/solution tests, canonical statement
2. Root Cause Analyst   — Five Whys (depth) + Fishbone (breadth) + causation tests
3. JTBD Frame           — 3-layer jobs, 4 forces, non-obvious competition, firing question
4. Opportunity Mapper   — OST with strict opportunity-vs-solution discipline
5. Hypothesis Generator — 4 MECE hypotheses, kill criteria, steel man obligation
6. Business Impact Tree — Causal impact equation + TAM/SAM/SOM + sensitivity
7. 2×2 Strategist       — Axes derived from analysis, blank quadrant test, justification
8. Synthesizer          — One-pager + HMW statements + success metrics + validation plan
```

Each agent builds on the last. The sequence is enforced — you cannot run
Agent 5 before Agents 2 and 3 have done their job.

---

## File Structure

```
pm-problem-structuring/
├── SKILL.md                                        # Main orchestrator
├── README.md                                       # This file
└── references/
    ├── agent-1-problem-definer.md
    ├── agent-2-root-cause-analyst.md
    ├── agent-3-jtbd-frame.md
    ├── agent-4-opportunity-mapper.md
    ├── agent-5-hypothesis-generator.md
    ├── agents-6-and-7.md                           # Business Impact + 2×2
    └── agent-8-synthesizer.md

shared-agents/                                      # Repo-level, importable by any skill
├── README.md
├── business-impact-calculator.md                   # Used by Agent 6
├── industry-context-agent.md                       # Used by Agents 1, 6
└── brand-style-agent.md
```

---

## What Makes This Top 1%ile

**The sequence is enforced.** Not optional. Problem definition before root cause.
Root cause before hypotheses. JTBD before opportunity mapping. Every agent's
output feeds the next.

**Every agent has a mandatory stress test:**
- Agent 1: Counterfactual check + incentive test
- Agent 2: Pre-mortem on the root cause
- Agent 3: The firing question
- Agent 4: Breadth test + adjacent opportunity space
- Agent 5: Steel man obligation on the least-favoured hypothesis
- Agent 6: Four reality checks (1% rule, CAC sanity, So What, competitive deflation)
- Agent 7: Blank quadrant test + axis justification
- Agent 8: "So What" test on every section

**The business impact is causally connected.** Not "our market is $5B." But:
"If we solve [specific root cause] for [specific segment], [specific metric]
moves by [amount] because [mechanism] — and here are the three assumptions
that make that wrong."

**The JTBD goes three layers deep.** Functional job (what task). Emotional job
(how they want to feel). Social job (how they want to be perceived). The
non-obvious competition map. The firing question. Most PM JTBD work stops
at Layer 1. The insights that change product direction are almost always in
Layers 2 and 3.

---

## Usage Patterns

**Full sequence (stakeholder brief):**
All 8 agents → complete one-page brief + HMW statements + validation plan

**Discovery prep (before user interviews):**
Agents 1 + 3 → Sharp problem statement + JTBD questions to guide interviews

**Data investigation (metric drop):**
Agents 1 + 2 + 5 → Root causes + 4 MECE hypotheses + kill criteria matrix

**Investment case (opportunity sizing):**
Agents 1 + 6 → Sharpened problem + causal impact model

**Roadmap discussion (prioritisation):**
Agents 4 + 7 → Ranked opportunity space + prioritisation 2×2

---

## Shared Agents Used

This skill imports two shared agents from `shared-agents/`:

**`business-impact-calculator.md`** (Agent 6)
Full 6-step impact model: causal equation + TAM/SAM/SOM + sensitivity analysis
+ reality checks. Also used by: PRD Writer, PM Rapid Prototype Builder.

**`industry-context-agent.md`** (Agents 1, 6)
Maps domain to compliance/regulatory context. Relevant when the problem or
opportunity has regulatory dimensions (fintech, healthcare, etc.)
Also used by: PM Rapid Prototype Builder, PM Technical Writer.

---

## Example Walk-Through

**Input:** "Our 30-day retention dropped from 42% to 31% over 8 weeks."

**Agent 1 (Problem Definer):**
→ Symptom check FAILS — this is a metric, not a problem
→ Reframed: "Users who sign up via paid social channels are not completing
  the account setup flow within their first session, causing them to miss
  the core value moment and churn before Day 30 — affecting 40% of new
  signups and threatening our Q4 growth OKR."

**Agent 2 (Root Cause):**
→ Fishbone: highest density in User Behaviour + Product/UX categories
→ Five Whys: Users abandon at the "Link your bank account" step (73% of
  drop-offs) → because they don't understand why it's required → because
  the benefit isn't explained before the ask → because the PM assumed
  users would already trust the product by that point

**Agent 3 (JTBD):**
→ Functional: "Complete account setup so I can send my first transfer"
→ Emotional: "Feel confident I'm setting this up correctly, not just
  clicking through something I don't understand"
→ Social: "Look like someone who uses modern, sophisticated tools —
  not someone who accidentally signed up for something sketchy"
→ Non-obvious competition: "Asking a colleague who's used it before"
  is getting hired instead of completing onboarding

**Agents 4–8:** [Full opportunity map, 4 MECE hypotheses, impact model
showing ₹2.4Cr annual revenue opportunity from solving this cohort,
2×2 prioritising the "explain value before asking for bank link"
opportunity, one-page brief, and a 3-test validation plan taking 4 days]

---

## Author

**Kamalika Poddar**
12 years in fintech infrastructure — core banking, UPI, payment aggregators,
account aggregators, wealth tech, and cross-border payment rails.
[GitHub](https://github.com/kamalikap) · [LinkedIn](https://linkedin.com/in/kamalikap)

---

## License
MIT — free to use, fork, and build on. Attribution appreciated.
