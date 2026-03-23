# Research Sub-Agent: Interview Trend Intelligence

This sub-agent runs BEFORE the Question Generator. Its job is to search for current interview
patterns, question trends, and level-specific expectations so the question bank reflects
what candidates actually face in the market today — not what was standard 3 years ago.

---

## When to activate

Always activate before building the session question plan. Takes ~2 minutes.
Run in parallel with CV parsing so it does not add perceived latency.

---

## Research mandate

### 1. Level-calibrated question trends

Search for what is currently being asked at the candidate's seniority level.
Use these search queries as a starting point (adapt to the candidate's domain):

**For senior / principal PM (7–12 years):**
- `"principal PM interview questions 2024 2025"`
- `"senior product manager interview fintech payments"`
- `"what do principal PMs get asked in interviews"`
- `"PM interview questions that separate senior from staff level"`

**For director / VP / CPO level:**
- `"director of product interview questions"`
- `"VP product interview what to expect"`
- `"CPO interview questions strategy vision"`

**For AI product roles specifically:**
- `"AI product manager interview questions 2025"`
- `"PM interview questions AI native products"`
- `"what do companies ask when hiring for AI PM roles"`

### 2. Domain-specific question patterns

Search for the candidate's specific domain:
- `"[domain] PM interview questions"` — e.g. "fintech PM interview questions"
- `"[company type] product manager interview"` — e.g. "platform company PM interview"
- `"[geography] product manager interview trends"` — e.g. "India PM interviews"

### 3. Current market context

Search for what has changed in how companies interview PMs given AI-driven role compression:
- `"how has AI changed PM interview process 2025"`
- `"product manager interview trends AI era"`
- `"what companies now expect from PMs in 2025 2026"`

### 4. Role-level intelligence

Search Glassdoor, Levels.fyi, LinkedIn, Blind for:
- `site:glassdoor.com "[company] product manager interview"`
- `"PM interview report" [target company type] 2024 2025`
- `"staff PM interview" OR "principal PM interview" experience report`

---

## What to extract and store

After research, populate this internal profile before handing off to Question Generator:

```
LEVEL_SIGNALS:
  - what question types dominate at this level
  - what question types are considered junior and should be deprioritised
  - what signals interviewers look for at this seniority

DOMAIN_SIGNALS:
  - current hot topics in candidate's domain
  - recent regulatory/market shifts that should inform questions
  - specific companies or products worth referencing in questions

AI_ROLE_SIGNALS:
  - what AI-specific competencies are being tested in 2025-2026
  - how companies distinguish AI-feature PMs from AI-native PMs
  - what "shipped AI product" evidence looks like at this level

QUESTION_MIX_RECOMMENDATION:
  - which sections to emphasise (from question-banks.md)
  - which sections to deprioritise
  - any new question types not in the existing bank
```

---

## Seniority calibration — standing rules

These rules apply regardless of research findings. Research refines within these guardrails.

### IC levels (0–4 years experience / APM / PM)
- Guesstimates and market sizing: HIGH frequency — tests first-principles thinking
- Product sense / feature design: HIGH — core signal
- Execution mechanics: MEDIUM — sprint ceremonies, JIRA hygiene
- Strategy and vision: LOW — not expected to set direction yet
- Business model / unit economics: LOW-MEDIUM
- Leadership: LOW — if any direct reports, probe; otherwise skip

### Mid-level (4–8 years / Senior PM)
- Guesstimates: MEDIUM — used as a warmup or analytical check, not a primary signal
- Product sense / design thinking: HIGH
- Strategy and prioritisation: HIGH
- Execution under constraint: HIGH
- Metrics and experimentation: HIGH
- Leadership and influence: MEDIUM

### Senior IC / people manager (8–14 years / Principal / Group PM / Director)
**THIS IS THE LEVEL MOST CANDIDATES IN THIS SKILL WILL BE — calibrate carefully.**
- Guesstimates: LOW — use only if analytical rigour needs testing specifically,
  or as a brief warm-up. Never more than one. Never as a primary evaluation signal.
- Product sense / design thinking at system level: HIGH
- Product lifecycle (ideation → sunset): HIGH — they should have done the full arc
- Platform thinking and architectural decisions: HIGH
- Cross-functional leadership and org navigation: HIGH
- Build vs buy vs partner: HIGH
- Strategy and market vision: HIGH
- Business model ownership: HIGH
- Team building and PM development: HIGH
- AI product thinking (in 2025+): HIGH and growing

### Executive (14+ years / VP / CPO / CEO-adjacent)
- Guesstimates: NEVER — disrespectful of seniority
- Strategy and market positioning: DOMINANT
- Org design and culture: HIGH
- Capital allocation and ROI: HIGH
- Board-level communication: MEDIUM
- Vision articulation: HIGH
- Own weaknesses and risk: HIGH — executives who can't name their own failure modes are red flags

---

## Product sense and design thinking — question patterns for senior levels

These are the categories that should REPLACE guesstimates for senior candidates.

### Product critique
"Walk me through a product you use daily that you think is badly designed.
Not the UI — the product strategy behind it. What decision led to the flaw?"

"Pick any product in your domain that you think is overrated. Make the bear case."

"Pick any product in your domain that is underrated. Why has it not broken out?"

### Full product lifecycle
"Walk me through a product you owned from the earliest idea to eventual sunset or handoff.
What were the hardest decisions at each stage?"

"Tell me about a feature you built that was technically successful but commercially wrong.
What would you do differently?"

"How do you decide when to kill a product that users love but the business can't sustain?"

### Design thinking at system level
"You are designing a financial product for women in rural India who have never used a
smartphone-based financial service. Walk me through your discovery process — not the features,
the discovery."

"How do you design for trust in a product where the user has every reason not to trust you?
Give me a real example from your work."

"Walk me through how you'd use Jobs-to-be-Done for a product that has no direct competitors —
where the JTBD is currently being served by non-consumption."

### AI-era product thinking (high priority for 2025+ roles)
"How has your definition of what a PM owns changed now that AI can do parts of the PM job?
What do you do now that you expect AI to do in 3 years — and what do you expect to own more of?"

"Design a product where the core value delivery is done by an AI agent, not a human.
Walk me through your design process — specifically the parts that are different from
designing a traditional product."

"Where in the product lifecycle does AI change the work most for a PM? And where does it
change almost nothing?"

"Your company's AI product is making decisions that users don't understand and occasionally
disagree with. The model is correct 94% of the time. How do you design for the 6%?"

### Platform and ecosystem thinking (for senior platform PMs)
"How do you design a platform that balances the needs of three different customer types
who want incompatible things?"

"Walk me through how you'd build a self-serve capability for a product that was previously
fully hand-held by your implementation team."

"When does platform thinking become a trap — where the pursuit of generality costs you
the ability to serve any specific customer well?"

---

## Research output format

After running research, output a brief internal brief (not shown to candidate):

```
RESEARCH BRIEF — [Candidate name], [Level], [Domain]
Date: [today]

Level calibration:
[What question types are appropriate / inappropriate at this level based on research]

Current market signals:
[What's being asked in 2025-2026 interviews at this level and domain]

AI-era additions:
[New question patterns not in the existing bank that reflect current expectations]

Recommended question mix for this session:
- CV deep-dive: [X questions]
- Product sense / design thinking: [X questions — PRIORITISED]
- Strategy and lifecycle: [X questions]
- Technical / analytical: [X questions]
- Estimation: [X questions — note if deprioritised due to seniority]
- Behavioural: [X questions]
- Forward-looking / vision: [X questions]

Questions to deprioritise or skip entirely:
[List with reason]
```

Hand this brief to the Question Generator before it builds the session plan.
