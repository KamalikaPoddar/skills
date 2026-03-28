# Pass 1 — Artifact Quality Audit

The rubric engine. Scores every ticket across five dimensions before
any execution analysis begins. A team cannot fix execution problems caused
by bad tickets — they have to fix the tickets first.

Pass 1 runs on the Ticket Content Package from Agent 1A. It does NOT require
execution data (no need for completion status, actual velocity, or PR data).

---

## The Five-Dimension Rubric

Each dimension scored 1–5. Rubrics are specific enough that two people
reading the same ticket should score within 1 point of each other.

---

## A1 — Ticket Classifier

**Question: Is the ticket type label correct given its actual complexity?**

Jira type labels are often wrong. Engineers create Stories that are really
Epics, or Epics that are Tasks, or Features that are really enhancements.
Wrong labels cause wrong planning, wrong estimation, and wrong sprint loading.

**Classification rules:**

```
EPIC / INITIATIVE:
  Correct when: The work spans multiple sprints, contains multiple independent
  deliverables, and cannot be shipped as a single unit.
  Signal in ticket: AC has 8+ items covering distinct user flows, OR description
  references "phases", OR child issues expected to total > 20 points.

FEATURE / USER STORY:
  Correct when: Deliverable in a single sprint, represents a complete user-facing
  capability, has AC that covers a coherent user flow end-to-end.
  Expected size: 3–13 story points.
  Red flags: < 1 point (should be task) or > 13 points without being an Epic.

TASK / CHORE:
  Correct when: Work is internal, has no direct user-facing AC, is < 1 sprint
  day of effort, supports a Feature but is not a Feature itself.
  Examples: "Update deployment config for feature X", "Add analytics events",
  "Write unit tests for Y module."

BUG:
  Correct when: Describes behaviour that should work but doesn't, references
  expected vs actual behaviour, linked to or caused by a prior feature.
  NOT correct when: The behaviour was never specified (that's a missing feature,
  not a bug) or the "bug" is actually a usability enhancement request.

SPIKE / RESEARCH:
  Correct when: The output is knowledge or a decision, not working software.
  Time-boxed. Produces a writeup or ADR, not a shipped feature.
```

**Scoring:**
```
5 — Type matches content perfectly. No ambiguity.
4 — Type is correct but borderline (e.g., large Story that could be Epic).
    Note the borderline case.
3 — Type is one level off. Explain the correct classification.
2 — Type is significantly wrong in a way that affects planning.
    (13-pt "Task", 1-pt "Feature", "Bug" that is actually a feature request)
1 — Type is completely wrong and would cause substantial planning errors.

CORRECT CLASSIFICATION: [what it should be, if different]
REASON: [one sentence explanation]
```

---

## A2 — Description Quality Scorer

**Question: Could any engineer unfamiliar with this feature pick up this ticket
cold and implement it correctly?**

This is the cold-start test. The description must provide enough context that
no verbal explanation is needed. Requiring a meeting to explain a ticket is
a description failure, not an engineer failure.

**Scoring dimensions within A2:**

```
CONTEXT (what and why — 1–5):
  5: Who the user is, what they're trying to do, why this matters — all clear.
  3: What is clear, why is implied or absent.
  1: Title rephrased as a sentence. No context.

SPECIFICITY (how precise is the requirement — 1–5):
  5: Specific enough to write a test before reading the AC.
     Example: "The transfer confirmation screen must display the recipient
     name, masked account number (last 4), transfer amount in source currency,
     FX rate used, total fees, and expected settlement date."
  3: General direction clear, specifics need to be inferred.
     Example: "Show transfer details on the confirmation screen."
  1: Vague to the point of being unimplementable without a follow-up conversation.

SCOPE CLARITY (what's in vs out — 1–5):
  5: Explicitly states what is OUT OF SCOPE. No ambiguity.
  3: In-scope clear, out-of-scope not mentioned (engineer must guess).
  1: Scope undefined. Engineer must make significant assumptions.

COMPOSITE SCORE: avg of three dimensions, rounded.
```

**Scoring output:**
```
DESCRIPTION SCORE: [X/5]
  Context:      [X/5] — [one-line finding]
  Specificity:  [X/5] — [one-line finding]
  Scope:        [X/5] — [one-line finding]

COLD-START TEST: [PASS — engineer could implement independently /
                  CONDITIONAL — needs one clarification /
                  FAIL — requires significant verbal context]

SPECIFIC GAPS: [List what's missing that would fail the cold-start test]
```

---

## A3 — AC Coverage Auditor

**Question: Does the AC cover the full behaviour of this feature — including
edge cases, failure states, and boundaries — or only the happy path?**

The AC is the contract. Bugs that match an unspecified behaviour are not bugs
— they're specification gaps. Most AC covers the happy path and nothing else.

**Coverage dimensions:**

```
HAPPY PATH (always required — 1/5 if missing):
  Does the AC describe what happens when everything goes correctly?

EDGE CASES (common — 2/5 if absent):
  Empty states: What happens when a list is empty, a value is zero, or
                a required entity doesn't exist?
  Boundary values: Maximum characters, minimum amounts, rate limits, caps.
  Concurrent actions: What if the user does X twice? Or does X while Y is in progress?

FAILURE STATES (critical — 2/5 if absent):
  What happens when the operation fails?
  Network timeout, downstream service error, validation failure, auth failure.
  Does the AC specify the error message? The recovery path?

PERMISSIONS / ROLES (required if feature is role-dependent):
  Does AC specify who can do this? What happens when an unauthorised user tries?

MOBILE / RESPONSIVE (required if UI feature):
  Does AC mention mobile behaviour, if different from desktop?

DATA / STATE CONSISTENCY (required for data-modifying features):
  What is the expected state after the operation?
  Is rollback behaviour specified for failures?
```

**Scoring:**
```
5 — Happy path + named edge cases + all failure states + permissions.
    Could write automated tests from the AC alone without making assumptions.
4 — Happy path + most edge cases. One or two failure states missing.
3 — Happy path + some edge cases. Failure states absent or vague.
    An engineer would have to make significant decisions not specified in AC.
2 — Happy path only. No edge cases. No failure states.
    ("User can complete the transfer" — nothing else.)
1 — No AC present, or AC is so vague it provides no real constraint.

AC SCORE: [X/5]
MISSING COVERAGE:
  ☐ [Specific edge case not covered]
  ☐ [Specific failure state not covered]
  ☐ [Permissions behaviour unspecified]
  ☐ [other gap]

COVERAGE VERDICT:
  If bugs were raised on this ticket: [were they AC gaps or genuine defects?]
  [DEFECT] — behaviour was specified in AC but implemented wrong
  [SPEC GAP] — behaviour was not in AC; engineer made a reasonable choice
               that turned out to be wrong
  [MISSING FEATURE] — a new requirement added after the fact, not a bug
```

---

## A4 — Grooming Depth Assessor

**Question: Was the technical design documented before implementation began,
and does what was built match what was planned?**

This dimension has two sub-questions:
1. Was there a technical design section? (pre-implementation quality)
2. Does the implementation match it? (implementation delta — enhanced by B5)

**Technical design presence scoring:**
```
5 — Technical approach documented: chosen approach, alternatives considered,
    constraints identified, external dependencies named, data model sketched.
    Either in ticket body or in a linked Confluence/Notion page.
4 — Approach documented, alternatives not discussed.
3 — High-level approach mentioned ("we'll use X pattern") but no detail.
2 — One sentence ("engineer to decide approach") — not grooming, it's abdication.
1 — No technical notes. Pure user-facing description only.
    (Acceptable for simple CRUD; unacceptable for complex features.)
```

**Grooming discussion evidence (from changelog/comments):**
```
Was this ticket discussed in a grooming session? Signals:
  Comment from multiple team members before development started
  Story points set by consensus (not just PM-assigned)
  Technical questions asked and answered in comments before In Progress

GROOMING EVIDENCE: [YES — [evidence] / NO — [no pre-dev comments found] /
                    UNCLEAR — [single actor set points before any discussion]]
```

**Design vs implementation check (from B5 CodeRabbit — if available):**
```
If CodeRabbit summary provided for this ticket:
  Does the implementation align with the documented approach?
  [ALIGNED — implementation matches design notes]
  [MINOR DEVIATION — small adjustments, no AC impact]
  [SIGNIFICANT DEVIATION — implemented differently, review if AC still met]
  [NO DESIGN TO COMPARE — no technical notes present]
```

**Scoring output:**
```
GROOMING SCORE: [X/5]
  Technical design depth: [X/5] — [finding]
  Grooming discussion:    [evidence or ABSENT]
  Design vs impl delta:   [ALIGNED / DEVIATION / NO DESIGN (check B5)]
```

---

## A5 — Estimation Auditor

**Question: Were estimates set appropriately — before development, by engineers,
based on the AC — and how well did they predict actual effort?**

Poor estimation is almost always a grooming problem, not an engineer problem.
If the AC wasn't written before estimation, the estimate was guesswork.

**Estimation process scoring:**
```
5 — Points set during grooming, before development started (confirmed by
    changelog: points set > 1 day before first "In Progress" transition).
    Set by or confirmed by an engineer, not unilaterally by PM.
    AC existed before points were assigned.

4 — Points set in grooming, but AC written simultaneously or shortly after.
    Slight sequencing issue but fundamentally sound.

3 — Points set by PM without grooming, but estimate was directionally correct.
    (Within 2 points of actual effort for tickets with time-in-progress data.)

2 — Points set after development started (changelog shows points added/changed
    after first "In Progress" transition). Post-hoc estimation.

1 — No points set (story points = null or 0). Ticket entered sprint unpointed.
    Or: points wildly off (estimate 2, actual > 13, or vice versa).
```

**Estimation accuracy scoring (where actual effort derivable):**
```
Derive actual effort from: time-in-progress from changelog × team daily rate
OR from: engineer comments mentioning time spent

If estimate vs actual data available:
  [CALIBRATED]   — actual within ±50% of estimate
  [OVERESTIMATED] — actual < 50% of estimate (team sandbagging or ticket scope shrunk)
  [UNDERESTIMATED] — actual > 150% of estimate (most common)
  [SIGNIFICANTLY UNDERESTIMATED] — actual > 200% of estimate (planning problem)

Date commitment accuracy (if due date was set in Jira):
  [MET] / [MISSED by N days] / [NO DATE SET]
```

**Spillage connection:**
```
If ticket spilled (not completed in sprint):
  Was spillage predictable from the estimate? [YES — ticket was > half the sprint /
                                               NO — should have fit within sprint]
  Was the estimate revised after scope expanded? [YES/NO]
  Was a revised estimate communicated to PM before sprint end? [YES/NO/UNCLEAR]
```

**Scoring output:**
```
ESTIMATION SCORE: [X/5]
  Process quality: [X/5] — [finding]
  Accuracy: [CALIBRATED / OVER / UNDER / SIGNIFICANTLY UNDER]
  Date commitment: [MET / MISSED by N / NOT SET]
  Spillage predictability: [if spilled]
```

---

## Pass 1 — Per-Ticket Summary

After scoring all five dimensions, produce a summary per ticket:

```
╔══════════════════════════════════════════════════════════╗
  TICKET QUALITY AUDIT — [PROJ-ID] "[Title]"
╠══════════════════════════════════════════════════════════╣

SCORES:
  A1 Classification:  [X/5] — [type: correct / should be Epic/Story/Task]
  A2 Description:     [X/5] — [cold-start: Pass/Conditional/Fail]
  A3 AC Coverage:     [X/5] — [happy path only / partial / comprehensive]
  A4 Grooming Depth:  [X/5] — [design: present/partial/absent]
  A5 Estimation:      [X/5] — [calibrated/over/under; process: pre/post groom]

OVERALL TICKET SCORE: [avg X/5]
  [5.0: Gold standard] [4.0–4.9: Strong] [3.0–3.9: Adequate]
  [2.0–2.9: Needs improvement] [<2.0: Significant gaps — rework before next sprint]

TOP 2 IMPROVEMENTS:
  1. [Most impactful thing to fix on this ticket type going forward]
  2. [Second most impactful]

LIKELY CONTRIBUTION TO EXECUTION PROBLEMS:
  [Did poor artifact quality likely cause bugs, spillage, or rework?
   Connect to Pass 2 findings where relevant.]
╚══════════════════════════════════════════════════════════╝
```

---

## Pass 1 — Sprint-Level Summary

After scoring all tickets, aggregate:

```
╔══════════════════════════════════════════════════════════╗
  PASS 1 SUMMARY — ARTIFACT QUALITY | [Sprint Name]
╠══════════════════════════════════════════════════════════╣

SPRINT AVERAGE SCORES:
  A1 Classification accuracy:  [X/5]
  A2 Description quality:      [X/5]
  A3 AC coverage:              [X/5]
  A4 Grooming depth:           [X/5]
  A5 Estimation calibration:   [X/5]
  OVERALL ARTIFACT QUALITY:    [X/5]

DISTRIBUTION:
  Gold (4.5+):              [N tickets] ([X%])
  Strong (3.5–4.4):         [N tickets] ([X%])
  Adequate (2.5–3.4):       [N tickets] ([X%])
  Needs improvement (1.5–2.4): [N tickets] ([X%])
  Significant gaps (<1.5):  [N tickets] ([X%])

WEAKEST DIMENSION: [A1/A2/A3/A4/A5] — [what this means for the team]
STRONGEST DIMENSION: [A1/A2/A3/A4/A5] — [acknowledge what's working]

SYSTEMIC GAPS (appear in >50% of tickets):
  [Gap 1 — specific pattern with example]
  [Gap 2]

TICKETS NEEDING IMMEDIATE REWORK (score < 2.0):
  [List with specific top improvement action each]

TICKET QUALITY TREND (vs prior sprint if available):
  [Improving / Stable / Declining] — [evidence]

📌 CONTEXT NEEDED FROM PM:
   [Questions that require PM judgment — e.g., "Was the grooming process
   different this sprint? Was there time pressure that affected AC quality?"]
╚══════════════════════════════════════════════════════════╝
```
