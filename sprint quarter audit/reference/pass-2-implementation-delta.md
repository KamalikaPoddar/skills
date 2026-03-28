# Pass 2 — B5 — Implementation Delta (CodeRabbit Integration)

**Question: Does what was implemented match what was specified in the
acceptance criteria?**

Uses CodeRabbit PR review summaries (or other AI PR reviewer output) as
the ground truth for "what was implemented." Cross-references against the
ticket's AC to identify gaps, surprises, and deviations.

**Why CodeRabbit summaries, not raw diffs:**
Raw diffs are noisy, hundreds of lines long, and hard to match against
natural language AC. CodeRabbit's summaries are already translated into
plain English — they describe what changed and why, making them directly
comparable to AC statements. This is better than raw diff analysis for
this use case.

---

## Input Requirements

**From PM (manual paste at intake):**
```
For each ticket you want implementation delta checked:

1. Paste the CodeRabbit review summary from the MERGED PR.
   - Copy from the PR page AFTER merge
   - Must be the FINAL merged state, not a mid-review round
   - If multiple CodeRabbit passes: use only the most recent one

2. If using a different AI PR reviewer:
   - GitHub Copilot PR summary → works the same way
   - Graphite PR summary → works the same way  
   - LinearB code review summary → works the same way
   - Sweep PR description → works the same way
   Any tool that produces a plain-English summary of what changed is usable.

3. If no AI PR reviewer is used:
   - Paste the PR description (manually written by engineer)
   - Flag: manual PR description, confidence will be LOWER
   - Or: paste the diff for the most critical files only (not recommended
     for complex PRs — too noisy)
```

**Critical instruction to relay to PM:**

```
"Please paste the CodeRabbit summary from the MERGED PR, not from an
in-progress review. If there were 3 review rounds, CodeRabbit may have
posted 3 summaries — I need the one from the final merge.

Also confirm: is this the PR for the entire feature, or one of multiple
PRs? If the feature was split across PRs, paste all of them."
```

---

## Cross-Reference Methodology

For each ticket with both AC (from Pass 1 A3) and a CodeRabbit summary:

**Step 1 — Map AC items to implementation:**

```
For each AC item:

  AC ITEM: "[Statement from acceptance criteria]"
  
  Search the CodeRabbit summary for:
    Explicit mention of the feature/behaviour described
    Code changes to the relevant component/function
    Logic that handles the specified condition
  
  Classification:
  [IMPLEMENTED]     — CodeRabbit summary clearly shows this was implemented
  [LIKELY IMPLEMENTED] — Not explicit but implied by the changes described
  [NOT MENTIONED]   — No mention in CodeRabbit summary; may or may not be there
  [CONTRADICTED]    — CodeRabbit describes different behaviour than AC specifies
```

**Step 2 — Identify surprises (code that has no AC):**

```
For each significant change described in CodeRabbit summary:

  CHANGE: "[What CodeRabbit says was changed]"
  
  Does this correspond to any AC item? [YES / NO]
  
  If NO — classify:
  [INTERNAL IMPLEMENTATION DETAIL] — Not visible at AC level, expected
  [SCOPE ADDITION]  — New user-visible behaviour not in AC
                       (was this discussed? should AC have been updated?)
  [TECH DEBT / CLEANUP] — Refactoring alongside the feature
  [POTENTIAL RISK]  — Change to shared/core logic not mentioned in AC
                       (regression risk signal — flag for B4 review check)
```

**Step 3 — Confidence calibration:**

```
The reliability of this analysis depends on CodeRabbit summary quality.

HIGH CONFIDENCE:
  CodeRabbit summary is detailed, mentions specific functions/files,
  describes logic changes in plain English, calls out edge cases handled.
  → Analysis is reliable; gaps are likely real gaps.

MEDIUM CONFIDENCE:
  CodeRabbit summary is general, describes the feature at a high level.
  → "NOT MENTIONED" items may be implemented but not described.
     Flag gaps for PM to verify with engineer.

LOW CONFIDENCE:
  CodeRabbit summary is very short (<200 words), or
  PR description is manually written without implementation detail, or
  Feature was split across multiple PRs not all provided.
  → Flag: implementation delta analysis is indicative only.
     Engineer review of AC checklist is more reliable for this ticket.

INCOMPATIBLE:
  No CodeRabbit summary provided.
  → Skip B5 for this ticket. Note in output.
```

---

## Per-Ticket Implementation Delta Report

```
╔══════════════════════════════════════════════════════════════╗
  IMPLEMENTATION DELTA — [PROJ-ID] "[Title]"
  PR: [#number] | Source: [CodeRabbit / Copilot / Manual PR desc]
  Confidence: [HIGH / MEDIUM / LOW]
╠══════════════════════════════════════════════════════════════╣

AC COVERAGE (X of N criteria addressed in implementation):

  ✅ IMPLEMENTED: [N items]
     [List each AC item confirmed in CodeRabbit summary]
     
  ⚠️  NOT MENTIONED: [N items] — verify with engineer
     [List each AC item with no corresponding mention]
     [At MEDIUM/LOW confidence: may be implemented but undescribed]
     [At HIGH confidence: likely a gap — needs verification]
     
  ❌ CONTRADICTED: [N items] — escalate immediately
     [List each where implementation differs from AC]
     [Evidence: "[AC says X]" vs "[CodeRabbit says Y]"]

SURPRISES (in code, not in AC):
  [INTERNAL]    — [N items — as expected, no action]
  [SCOPE ADD]   — [N items — list, flag if significant]
  [TECH DEBT]   — [N items — note]
  [RISK]        — [N items — list, cross-reference with B1 regressions]

DELTA VERDICT:
  [ALIGNED]      — Implementation matches AC; no significant gaps
  [MINOR GAPS]   — 1–2 AC items not mentioned; low risk
  [MEANINGFUL GAPS] — 3+ AC items not mentioned or 1 contradiction
  [SIGNIFICANT DEVIATION] — Multiple contradictions or major scope additions

RECOMMENDED ACTIONS:
  [Specific action for each CONTRADICTED and high-priority NOT MENTIONED item]

📌 CONTEXT NEEDED FROM PM:
   [CONTRADICTED items]: "[AC says X but CodeRabbit says Y]."
   Was this a deliberate deviation from the AC? If yes, was the AC updated?
   If no, this needs to be addressed before the ticket is marked Done.
   
   [SCOPE ADDITION items if significant]: Was [X] discussed and agreed?
   Should the AC have been updated to reflect this?
╚══════════════════════════════════════════════════════════════╝
```

---

## Sprint-Level Implementation Delta Summary

```
IMPLEMENTATION DELTA SUMMARY — [Sprint Name]
═════════════════════════════════════════════

Tickets with CodeRabbit analysis: [N of N total tickets]
Tickets without (skipped B5):     [N — reasons: no PR summary provided]

Overall AC coverage rate: [X%] of all AC items confirmed implemented
                          across all analysed tickets

Verdict distribution:
  ALIGNED:             [N tickets] ([X%])
  MINOR GAPS:          [N tickets] ([X%])
  MEANINGFUL GAPS:     [N tickets] ([X%])
  SIGNIFICANT DEVIATION: [N tickets] ([X%])

Contradiction rate: [N contradictions across [N] tickets]
  [0: No spec violations found] 
  [1–3: Isolated deviations — investigate each]
  [>3: Systematic gap between spec and implementation — process issue]

Scope addition rate: [N] unspecified behaviours added
  [Healthy if: all are internal implementation details]
  [Concerning if: user-visible scope was added without AC update]

RISK FLAGS for B1 (Bug Classification):
  Code changes to shared/core logic not in AC: [N] — regression risk
  [List the specific shared modules changed without AC coverage]

Most common gap type: [AC items most frequently not confirmed in implementation]

Connection to B1 bugs:
  [Did any functional bugs raised this sprint match an AC item 
   classified as "NOT MENTIONED" in the delta? This confirms the gap
   was a real implementation miss, not a CodeRabbit summary limitation.]
```

---

## Handling Different PR Reviewer Tools

### CodeRabbit (primary)
- Produces structured summaries with file-level and logic-level descriptions
- Usually includes "Changes" section with plain-English description per file
- Reliability: HIGH for most tickets

### GitHub Copilot PR Summary
- Auto-generated summary in PR description
- Less detailed than CodeRabbit but covers main changes
- Reliability: MEDIUM — good for broad coverage, weak for edge case verification

### LinearB
- Has code review insights + metrics
- If LinearB is connected: also provides review participation data (useful for B4)
- Reliability: MEDIUM for implementation delta; HIGH for review metrics

### Manually Written PR Description
- Quality varies enormously — depends on engineer's description discipline
- Reliability: LOW to MEDIUM
- Instruct: "If using manual PR descriptions, the analysis will flag more
  'NOT MENTIONED' items because PR descriptions don't always match the
  structure of AC items. Have engineers explicitly address each AC item
  in their PR description for better results."

### No AI Reviewer (manual fallback)
```
If no CodeRabbit summary available for a ticket:

Option A — Skip B5 for that ticket:
  Note in output: "Implementation delta not analysed — no PR summary provided."
  Recommend: "Consider enabling CodeRabbit or GitHub Copilot PR summaries
  for future sprints — this analysis becomes significantly more valuable."

Option B — Engineer self-attestation:
  Ask PM to request engineer to fill in:
  "For each AC item: did you implement this? [Y/N] Any deviations? [describe]"
  Parse their response against AC items.
  Reliability: LOWER (self-assessment) but better than nothing.
```

---

## Future Automation Path

When ready to automate (not manual paste):

```
AUTOMATION ARCHITECTURE:
  Jira → PR links (via Development panel field)
  → GitHub API → PR number → fetch review comments
  → Filter for CodeRabbit bot comments
  → Extract latest summary comment (after final merge)
  → Feed to B5 cross-reference

This requires:
  GitHub MCP connection OR GitHub API key
  Jira-GitHub integration (standard for most teams)
  CodeRabbit installed on the repo

Time to implement: 1–2 days engineering
Benefit: removes all manual paste burden for B5
```
