# Agent 1A — Sprint Ingestion
 
Primary source for sprint execution data. Extracts significantly more than
a standard Jira report — this is the forensic layer, not the summary layer.
 
---
 
## Source Handling
 
### Jira (Primary — MCP)
 
If Jira MCP is connected, auto-fetch. Don't ask.
 
**JQL queries to run:**
 
```
# Current sprint tickets
project = [PROJECT] AND sprint in openSprints()
 
# Completed sprint (by name or most recent closed)
project = [PROJECT] AND sprint = "[SPRINT_NAME]" ORDER BY status ASC
 
# Last 6 sprints for pattern analysis
project = [PROJECT] AND sprint in lastSprints(6) ORDER BY sprint DESC, status ASC
 
# Carryover detection: tickets in current sprint that were also in prior sprint
project = [PROJECT] AND sprint = "[CURRENT]" AND sprint was "[PRIOR]"
 
# Mid-sprint additions: tickets added after sprint start date
project = [PROJECT] AND sprint = "[SPRINT]" AND created > "[SPRINT_START_DATE]"
```
 
**Per-ticket extraction targets:**
 
```
Core fields:
  Issue key, summary, issue type, status, assignee, reporter
  Story points (original estimate), story points (final)
  Sprint(s) the ticket appeared in — flags carryover
  Created date, updated date, resolved date
  Epic link, parent initiative
  Labels, components, fix version
 
Audit-specific fields:
  Time in each status (from status change history)
  How many times status changed (churned tickets = complexity signal)
  Was ticket added after sprint start? (mid-sprint addition flag)
  Was ticket in any prior sprint? (carryover flag — note how many sprints)
  Acceptance criteria present? (yes/no from description length + AC section)
  Blocked flag — was it ever "Blocked" status, and for how long?
  Reassigned? (changed assignee mid-sprint)
  Bug type if bug: new bug vs regression of existing feature
 
OKR/objective fields (if present):
  Custom field: OKR link, Epic theme, Strategic initiative label
  Any label matching OKR naming convention (ask PM what their convention is)
```
 
### Linear (MCP or Export)
 
If Linear MCP connected: fetch cycle (Linear's sprint equivalent) issues.
If not: ask PM to export CSV from Linear's cycle view.
 
Map Linear fields to the same normalised format:
```
Linear field          → Normalized field
──────────────────    → ──────────────────
Cycle                 → Sprint
Estimate (points)     → Story points
State                 → Status
Priority              → Priority
Project               → Epic/initiative
Completed date        → Resolved date
Canceled              → Flag as: removed from sprint
```
 
### GitHub Projects (Export or paste)
 
GitHub Projects lacks the audit-depth of Jira. Extract what's available:
```
- Issue title, status (Todo / In Progress / Done)
- Assignee, milestone (= sprint proxy)
- Labels (use for type classification)
- Closed date
```
Flag: GitHub Projects data will limit Agent 2 (no time-in-status, no estimate history).
 
### Paste / CSV Upload
 
Accept any of:
- Jira export CSV (standard columns)
- Linear export CSV
- Copy-paste from sprint board
- PM's manual sprint summary (prose)
 
From paste/prose: extract ticket titles, statuses, story point estimates,
and any mentioned blockers or slip reasons. Flag confidence as LOWER.
 
---
 
## Normalised Sprint Data Format
 
Regardless of source, produce this structure before passing to audit agents:
 
```
SPRINT DATA PACKAGE
════════════════════
Sprint:     [Name]
Period:     [Start date] → [End date]   (or: [N days])
Team size:  [N engineers] (if derivable from assignees)
Source:     [Jira / Linear / GitHub / Paste]
Data confidence: [HIGH — full API / MEDIUM — export / LOW — manual paste]
 
TICKET INVENTORY:
[For each ticket:]
 
  [PROJ-ID] | [Title] | [Type] | [Status] | [Pts: planned → final]
  ─────────────────────────────────────────────────────────────────
  Assignee:       [name]
  Epic/Initiative:[name or "unlinked"]
  OKR link:       [explicit link / inferred: "[OKR text]" / none]
  Sprint history: [current only / CARRYOVER from [N] prior sprints]
  Added mid-sprint: [yes — Day N of sprint / no]
  Blocked:        [yes — [N] days / no]
  Time in status: [Todo: Nd | In Progress: Nd | Review: Nd]
  AC present:     [yes / no]
  Notes:          [any slip reason mentioned in comments]
 
SPRINT SUMMARY METRICS:
  Total tickets planned (Day 1):    [N]
  Total tickets completed:          [N]
  Total story points planned:       [N]
  Total story points delivered:     [N]
  Sprint completion rate:           [X%]
  
  Carryover tickets (from prior):   [N] ([X% of total])
  Mid-sprint additions:             [N] ([X% of total])
  Removed from sprint:              [N]
  Blocked at any point:             [N] tickets, [N] total days
 
  Ticket types (raw Jira labels):
    Story/Feature:  [N]
    Bug:            [N]
    Task/Chore:     [N]
    Sub-task:       [N]
    Other:          [N]
```
 
---
 
## What to Do With Missing Data
 
| Missing field | Action |
|---|---|
| No story points | Flag — note velocity analysis will be ticket-count based |
| No OKR links | Note — Agent 4 will use semantic inference if PM selected that mode |
| No time-in-status | Flag — slip root cause analysis will be limited |
| No sprint history (carryover unknown) | Flag — carryover pattern unavailable |
| No acceptance criteria field | Infer from description length: < 100 words = likely no AC |
 
Never guess. Always flag what's missing and what analysis it limits.
 
---
 
## 6-Sprint Historical Pull (for Agent 6)
 
If quarter audit mode and prior sprint data is available:
 
Pull same fields for each of the last 6 sprints.
Produce a **Historical Sprint Matrix**:
 
```
HISTORICAL SPRINT MATRIX (6 sprints)
═══════════════════════════════════════════════════════════════════
                  Sprint 1   Sprint 2   Sprint 3   Sprint 4   Sprint 5   Sprint 6
                  [oldest]                                              [current]
──────────────────────────────────────────────────────────────────────────────────
Planned pts:       [X]        [X]        [X]        [X]        [X]        [X]
Delivered pts:     [X]        [X]        [X]        [X]        [X]        [X]
Completion rate:   [X%]       [X%]       [X%]       [X%]       [X%]       [X%]
Carryover tickets: [N]        [N]        [N]        [N]        [N]        [N]
Mid-sprint adds:   [N]        [N]        [N]        [N]        [N]        [N]
Bug ticket %:      [X%]       [X%]       [X%]       [X%]       [X%]       [X%]
Unplanned work %:  [X%]       [X%]       [X%]       [X%]       [X%]       [X%]
OKR-linked work %: [X%]       [X%]       [X%]       [X%]       [X%]       [X%]
```
 
If fewer than 6 sprints available: use what exists, note the limitation.
 
---
 
## EXTENDED EXTRACTION — Ticket Content (for Pass 1)
 
Pass 1 (artifact quality) requires reading the actual ticket body, not just
metadata. This section defines what to extract per ticket for Pass 1 scoring.
 
### Jira MCP — Content Fields
 
In addition to the standard metadata fields, fetch:
 
```
Description body (full text):
  → Pass to A2 (Description Scorer)
  → Extract: does it contain an AC section? A technical notes section?
  → Flag if description is < 100 words (almost certainly insufficient)
 
Acceptance criteria (extracted from description):
  Patterns to detect:
    "Acceptance Criteria:" or "AC:" header followed by bullet points
    "Given / When / Then" format (BDD)
    Numbered list after "Definition of Done:"
  → Pass to A3 (AC Coverage Auditor)
  → If no AC section found: flag as MISSING — score 1/5 on A3
 
Technical design section (extracted from description or linked Confluence):
  Patterns to detect:
    "Technical Notes:", "Implementation Notes:", "Tech Design:", "Approach:"
    Linked Confluence page in description (fetch if MCP connected)
  → Pass to A4 (Grooming Depth Assessor)
 
Jira changelog (status transition history):
  Fields needed per transition:
    From status → To status
    Timestamp of transition
    Actor (who changed it)
  → Used by: A5 (was estimate set before/after dev started?)
             B2 (board flow analysis — time in each stage)
             B3 (spillage root cause — where did it stall?)
 
Comments (full thread):
  → Extract: any slip reasons mentioned by engineer or PM
  → Extract: any "blocked" comments with blocker description
  → Extract: review comments (for B4 review quality)
  → Flag: tickets with zero comments (possible isolation signal)
 
Linked issues:
  "Blocks" / "is blocked by": → B3 spillage analysis
  "is duplicated by" / bug links: → B1 bug classification
  PR links: → B5 implementation delta (extract PR numbers)
```
 
### Extraction Priority
 
Not all tickets need full content extraction. Prioritise:
 
```
FULL CONTENT EXTRACT (always):
  All tickets that slipped (not completed in sprint)
  All tickets with bugs raised against them
  All tickets with 3+ status transitions
  All tickets with story points > 5
 
METADATA ONLY (acceptable):
  Tasks and sub-tasks under 3 points
  Tech debt tickets with no user-facing AC
  Tickets that completed with no issues
 
SKIP (document):
  Purely operational tickets (meeting notes as tasks, etc.)
```
 
### Paste / Upload Mode
 
If Jira MCP not connected, ask PM:
 
```
"For each ticket you want Pass 1 quality audited, paste:
 1. The ticket ID and title
 2. The full description (including AC section)
 3. Story points as originally estimated
 4. Story points revised (if revised)
 5. Final status and completion date
 
 For Pass 2 (board flow), also paste the status history:
 e.g., 'To Do → In Progress (Day 2) → In Review (Day 6) →
        Back to In Progress (Day 7) → Done (Day 9)'
 
 At minimum: the tickets that caused you concern this sprint."
```
 
### Normalised Ticket Content Package
 
Output per ticket before passing to Pass 1:
 
```
TICKET CONTENT PACKAGE — [PROJ-ID]
════════════════════════════════════
Title:         [title]
Type (Jira):   [Story/Feature/Task/Bug/Epic]
Points (orig): [N] | Points (final): [N]
Status:        [final status]
 
DESCRIPTION BODY: [full text]
  Word count:    [N words]
  AC present:    [YES — extracted below / NO]
  Tech notes:    [YES — extracted below / NO]
  Linked pages:  [list if any]
 
ACCEPTANCE CRITERIA (extracted):
  [Bullet 1]
  [Bullet 2]
  [...]
  Format: [BDD / Bulleted / Numbered / Prose / MISSING]
  Count:  [N criteria items]
 
TECHNICAL NOTES (extracted):
  [Content or: NONE PRESENT]
 
CHANGELOG (status transitions):
  [Status 1] → [Status 2]: [date/day] ([actor])
  [Status 2] → [Status 3]: [date/day] ([actor])
  [...]
  Regressions (backwards transitions): [N]
 
COMMENTS SUMMARY:
  Total comments: [N]
  Slip reasons mentioned: [extract or NONE]
  Blockers mentioned: [extract or NONE]
  Review feedback: [extract or NONE]
 
LINKED ITEMS:
  Bugs raised: [list IDs or NONE]
  PRs linked: [list PR numbers or NONE]
  Blocked by: [list or NONE]
```