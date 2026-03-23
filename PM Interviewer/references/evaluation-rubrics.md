# Evaluation Rubrics

The Live Evaluator sub-agent uses these rubrics throughout the interview.
Scores are kept internally and never shown to the candidate mid-session.
They feed directly into the final feedback report.

---

## Scoring system

Each dimension is scored 1–5:
- **5 — Exceptional**: would set a high bar even at a level above the role
- **4 — Strong**: solid evidence, above expectations for the level
- **3 — Adequate**: meets expectations, some gaps, coachable
- **2 — Weak**: significant gaps, would need substantial development
- **1 — Absent**: no credible evidence, or actively concerning signals

Score only dimensions that were tested. Mark untested dimensions as `[not assessed]`.

---

## Rubric dimensions

### 1. Systems thinking
*Does the candidate think in architectures, abstractions, and second-order effects — or only in features?*

**5**: Unprompted, models the system at multiple levels of abstraction. Identifies downstream effects
and failure modes before being asked. Makes connections between unrelated domains.

**4**: Consistently thinks beyond the immediate feature. Identifies dependencies and tradeoffs.
Needs occasional prompting to zoom out.

**3**: Understands the system when walked through it. Doesn't proactively map it.

**2**: Feature-level thinking predominantly. Struggles to explain why decisions affect the broader system.

**1**: No evidence of systems thinking. Focuses entirely on the immediate request.

---

### 2. Business and commercial acumen
*Does the candidate understand the revenue model, unit economics, and commercial stakes of their decisions?*

**5**: Fluent in unit economics, margin, LTV/CAC, and regulatory cost of capital.
Connects every product decision to a commercial outcome without prompting.

**4**: Strong commercial awareness. Knows the revenue model. Makes sound tradeoffs between
user value and business sustainability.

**3**: Understands revenue models at a surface level. Mentions commercial considerations
when explicitly prompted.

**2**: Product and business are conceptually separate for this candidate.
Metrics are user-facing; commercial outcomes are someone else's job.

**1**: No commercial awareness demonstrated.

---

### 3. Technical depth
*Can the candidate have a substantive conversation with engineers about APIs, data, system design, and ML?*

**5**: Operates comfortably at the design level. Understands tradeoffs in system architecture.
Has hands-on experience with technical implementation.

**4**: Strong technical fluency. Can read a technical spec, identify gaps, and challenge
engineering decisions with evidence.

**3**: Working technical literacy. Understands APIs, databases, basic system concepts.
Cannot go deep on design tradeoffs.

**2**: Surface-level technical knowledge. Uses correct terminology but can't back it up.

**1**: No technical depth. Technical questions produce word salad.

---

### 4. Data and analytical rigour
*Can the candidate structure ambiguous problems quantitatively, and do they understand their metrics?*

**5**: Structures estimation problems cleanly. Knows the difference between correlation
and causation. Sets up experiments correctly. Challenges their own numbers.

**4**: Strong quantitative instincts. Makes clean assumptions. Catches their own errors.
Understands statistical significance at a practical level.

**3**: Competent with basic metrics. Can do back-of-envelope math. Weak on experimental design
or interpreting ambiguous results.

**2**: Struggles with numerical reasoning under pressure. Makes unit errors.
Metrics are reported, not interrogated.

**1**: Cannot do basic estimation. No evidence of quantitative thinking.

---

### 5. Execution and delivery
*Does this candidate ship? Do they know how to operate inside an organisation at pace?*

**5**: Clear evidence of shipping complex things on time. Knows how to manage tradeoffs
under constraint. Has navigated real delivery crises with good judgment.

**4**: Strong execution record. Understands sprint mechanics, stakeholder management, and delivery risk.

**3**: Adequate execution. Has shipped things. Doesn't have strong intuitions about delivery risk
or how to manage it proactively.

**2**: Execution is mostly reactive. Has been in delayed or troubled projects without
clearly owning the response.

**1**: No credible execution evidence. Everything landed cleanly with no visible effort.

---

### 6. Leadership and influence
*Can this candidate lead without authority, develop others, and move organisations?*

**5**: Clear evidence of building high-performing teams. Has navigated real disagreement
at the executive level. Develops people deliberately.

**4**: Strong leadership signals. Has influenced cross-functional outcomes. Takes accountability
for team performance.

**3**: Has led small teams or projects. Leadership mostly positional (direct reports).
Influence without authority is underdeveloped.

**2**: Minimal leadership experience or evidence. Influence stories are thin or generic.

**1**: No leadership evidence.

---

### 7. Self-awareness and intellectual honesty
*Does this candidate know what they don't know? Do they self-correct? Are they honest about failure?*

**5**: Proactively names their own weaknesses. Self-corrects mid-answer without prompting.
Has genuine failure stories with real consequences.

**4**: Intellectually honest when pushed. Admits uncertainty. Doesn't oversell.

**3**: Adequate honesty. Admits failure when directly asked. Occasionally oversells.

**2**: Defensive when challenged. Failure stories resolve too neatly.
Uncertainty is rarely acknowledged.

**1**: No intellectual honesty demonstrated. Everything worked out. No weaknesses admitted.

---

### 8. Communication clarity
*Can this candidate explain complex things simply, without losing precision?*

**5**: Explains complex systems with clarity and appropriate abstraction for the audience.
Uses precise language. Never loses the thread.

**4**: Clear communicator. Occasionally over-explains or under-explains, but self-corrects.

**3**: Adequate clarity. Some meandering. Gets to the point eventually.

**2**: Frequently unclear. Over-uses jargon. Loses the thread mid-answer.

**1**: Communication is a significant barrier. Answers are consistently confusing.

---

### 9. Domain expertise (role-specific)
*How deep is their actual domain knowledge in the specific area the role requires?*

Score against the role's domain requirements. Calibrate to the level being interviewed.

Fintech/payments indicators to watch:
- Knows specific regulatory frameworks (RBI, SEBI, PCI-DSS) not just generically
- Understands settlement mechanics, reconciliation, and float
- Can speak to card network economics, MDR, interchange
- Knows the difference between TPAP, PSP, PA, PG, and their relative margins
- Understands the Account Aggregator ecosystem and its limitations

AI product indicators to watch:
- Distinguishes between AI features and AI-native product design
- Understands model evaluation, hallucination risk, and human-in-the-loop design
- Has shipped or seriously designed for autonomous agent behaviour
- Understands the regulatory and liability implications of AI decisions

---

### 10. Hire signal
*Overall assessment at the configured level and one level above.*

This is not a calculated average. It is a holistic judgment.

**Strong hire at level**: Clear fit, no significant gaps, would raise team bar.
**Hire at level**: Solid candidate, manageable gaps, would deliver value.
**Borderline at level**: Has the core, but one or two significant gaps that would require
active management. Could go either way depending on the team context.
**No hire at level**: Does not meet the bar. Could be reconsidered at a lower level.
**Strong no hire**: Significant concerns across multiple dimensions.

---

## Red flag tracker

Flag immediately if:
- Candidate cannot explain their own claimed metrics
- Candidate takes solo credit for clearly team-delivered outcomes
- Failure stories consistently resolve without consequence
- Candidate becomes defensive or argumentative under follow-up
- Candidate cannot do basic back-of-envelope math
- Candidate uses AI/product buzzwords without underlying depth
- Candidate has never said "I don't know" in the session

---

## Dimension testing log template

```
systems_thinking: [score or "not assessed"] — [evidence notes]
business_acumen: [score or "not assessed"] — [evidence notes]
technical_depth: [score or "not assessed"] — [evidence notes]
analytical_rigour: [score or "not assessed"] — [evidence notes]
execution: [score or "not assessed"] — [evidence notes]
leadership: [score or "not assessed"] — [evidence notes]
self_awareness: [score or "not assessed"] — [evidence notes]
communication: [score or "not assessed"] — [evidence notes]
domain_expertise: [score or "not assessed"] — [evidence notes]
hire_signal: [strong hire / hire / borderline / no hire / strong no hire]
red_flags: [list or "none"]
```
