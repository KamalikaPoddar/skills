# Agent 1C — OKR & Metric Intake

Establishes the baseline: what were the team's objectives, what were the
metric values at period start, and what are they now? Without this, the
OKR impact assessment (Agent 4) can describe outputs but not outcomes.

---

## OKR Mode (Set at Intake)

The PM chose their mode at the start of the audit. Reference it throughout:

**MODE A — Semantic Inference:**
Accept any ticket as potentially OKR-linked if its description or title
contains language that maps to the stated OKR/KR. Flag inferences explicitly.
Higher coverage, some noise. Good for teams without explicit OKR tagging.

**MODE B — Explicit Links Only:**
Only count tickets with a documented OKR field in Jira, an initiative label
matching an OKR, or an epic that is explicitly tied to a KR.
All other tickets are "orphaned work." Good for teams with mature OKR hygiene.

---

## OKR Ingestion Sources

### OKR-Specific Tools (Lattice / Ally / Gtmhub)
If MCP connected: pull objectives, key results, current progress %.
If not: ask PM to paste the OKR dashboard or export.

### Notion / Confluence OKR Pages
Read and parse the structure. Most teams follow:
```
Objective: [statement]
  KR1: [statement] — Target: [X] — Current: [Y] — Owner: [person]
  KR2: [statement] — Target: [X] — Current: [Y] — Owner: [person]
```

### Jira Epics as OKR Proxies
If OKR tool not connected: use Jira epic names as strategic themes.
Ask PM to confirm which epics map to which OKRs.

### Manual Input
PM states OKRs directly in the conversation. Extract:
- Objective statement
- Each KR with: metric name, start value, target value, current value
- KR owner (team or person)

---

## Metric Baseline Table

**This is what makes OKR analysis possible.** Without baselines, we can only
say work happened — we cannot say whether it worked.

```
METRIC BASELINE TABLE
═════════════════════
Sprint/Quarter: [period]
Collected:      [from tool / from PM input / unavailable]

| KR | Metric | Period Start | Period End | Target | Δ | % to Target |
|----|--------|--------------|------------|--------|---|-------------|
| KR1 | [metric] | [value] | [value] | [value] | [+/-X] | [X%] |
| KR2 | [metric] | [value] | [value] | [value] | [+/-X] | [X%] |

For each KR:
  Direction of movement: [toward target / away from target / flat]
  Expected contribution this sprint: [what shipped claimed to address this]
  Attribution confidence: [HIGH — metric moved and matches shipped work /
                           MEDIUM — metric moved but causation unclear /
                           LOW — no metric data available]
```

**When metric baselines are unavailable:**
Flag clearly. OKR Impact assessment will be:
- Traceability analysis (which tickets link to which OKRs) — still possible
- Actual impact assessment (did the metric move?) — NOT possible
- Flag as: "Output linkage verified; outcome impact unverifiable — PM to provide
  metric movement data to complete this section."

---

## OKR Structure Output

```
OKR PACKAGE
═══════════
Period: [Q / Sprint]
OKR Mode: [Semantic Inference / Explicit Links Only]

OBJECTIVE 1: [Statement]
  KR1: [statement]
    Metric: [name] | Start: [X] | Now: [Y] | Target: [Z] | Gap: [X%]
    Owner: [person/team]
    OKR-linked tickets in this sprint: [count] ([X story points])
    
  KR2: [statement]
    [same format]

OBJECTIVE 2: [Statement]
  [same format]

TOTAL:
  Story points with any OKR link: [N] ([X%] of delivered)
  Story points with no OKR link:  [N] ([X%] of delivered) — "orphaned work"
```

---

# Agent 1D — Quality Signal Pull

Optional layer. When available, transforms the audit from "what we shipped"
to "what we shipped and what it cost the product's quality."

---

## Signal Sources

### Bug Backlog Delta (Jira)

```
JQL: project = [P] AND issuetype = Bug AND created >= "[sprint_start]"
     AND created <= "[sprint_end]"

Metrics to extract:
  Bugs reported in period: [N]
  Of those: new bugs [N] | regressions of existing features [N]
  Bugs closed in period: [N]
  Net bug backlog change: [+N grew / -N shrank]
  
  Bug introduction rate: bugs per story point of feature work delivered
  This period: [X bugs/pt] vs prior period: [X bugs/pt]
  Trend: [improving / stable / worsening]
```

### GitHub / GitLab Signals (if connected)

```
PR cycle time: average time from PR open to merge this sprint
  This sprint: [X hours/days] vs prior 3 sprints avg: [X]
  Trend: [faster / stable / slower]

Deploy frequency: number of production deploys this sprint
  vs team's baseline: [higher / same / lower]

Rollbacks: any production rollbacks this sprint? [Y/N + description]

Review participation: average reviewers per PR (proxy for code quality culture)
```

### Support / CS Ticket Volume (if accessible)

```
Post-launch ticket volume for features shipped this sprint:
  Within 7 days of shipping [feature]: [N] support tickets
  Common themes in those tickets: [extract from ticket titles if available]
  
  Interpretation: high post-launch support volume = either poor UX,
  poor documentation, or poor QA — all are product failures
```

### Quality Signal Summary

```
QUALITY SIGNALS SUMMARY
════════════════════════
Data available: [list what was accessible]
Data unavailable: [list what wasn't — and what it limits]

Bug introduction this sprint:     [N new bugs / X bugs/pt]
Net backlog health:               [improved / stable / worsened by N]
Deploy health:                    [normal / concern — explain]
Post-launch support signals:      [none / [N] tickets on [feature]]

QUALITY VERDICT:
[GREEN] — no quality signals of concern
[AMBER] — [specific concern] worth monitoring
[RED]   — [specific concern] requiring immediate attention
```

**If quality data unavailable:**
Flag clearly and skip — do not block audit on missing quality signals.
The audit produces findings across 4 lenses; quality is the 5th that
enhances but is not required.