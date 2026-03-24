# Integration Guide: Interviewer Background Research Sub-Agent

This document explains how to integrate the new Interviewer Background Research sub-agent into the existing pm-interviewer skill.

---

## Overview

**What's being added:**
A new sub-agent that researches the specific person conducting the interview when the candidate knows who they'll be meeting with.

**What already exists:**
An Interview Trend Research sub-agent that researches market trends and level-calibrated question patterns.

**How they work together:**
- Trend Research: Tells you WHAT to ask (question mix, seniority calibration, market context)
- Interviewer Research: Tells you HOW to ask it (style, emphasis, specific person's priorities)

---

## Step-by-Step Integration

### 1. Add new reference file

Create a new file in the references directory:
```
/mnt/skills/user/pm-interviewer/references/interviewer-background-research.md
```

Copy the content from the main sub-agent specification document created earlier.

### 2. Update the main SKILL.md file

**Current structure (Step 0):**
```markdown
## Step 0 — read reference files first

Before starting any interview session, read:
- `references/interviewer-persona.md` — who you are, how you behave
- `references/research-subagent.md` — how to research current interview trends and calibrate by seniority
- `references/question-banks.md` — base question inventory; always augmented by research findings
- `references/evaluation-rubrics.md` — how to score and track answers
- `references/report-template.md` — structure of the end-of-interview feedback report
```

**Updated structure:**
```markdown
## Step 0 — read reference files first

Before starting any interview session, read:
- `references/interviewer-persona.md` — who you are, how you behave
- `references/research-subagent.md` — how to research current interview trends and calibrate by seniority
- `references/interviewer-background-research.md` — how to research the specific interviewer (if known)
- `references/question-banks.md` — base question inventory; always augmented by research findings
- `references/evaluation-rubrics.md` — how to score and track answers
- `references/report-template.md` — structure of the end-of-interview feedback report
```

### 3. Update Step 1b in SKILL.md

**Current text (Step 1b):**
```markdown
### 1b. Run the Research Sub-Agent
Read `references/research-subagent.md` and execute the research protocol.
This runs in parallel with CV parsing.

The research agent must produce a RESEARCH BRIEF before the Question Generator runs.
The brief determines:
- Which question categories to emphasise and deprioritise **based on seniority level**
- What current market signals and AI-era patterns to fold into questions
- The final recommended question mix for the session
```

**Updated text (Step 1b):**
```markdown
### 1b. Run the Research Sub-Agents

**Two research sub-agents run here:**

**A) Interview Trend Research (always runs):**
Read `references/research-subagent.md` and execute the research protocol.
This runs in parallel with CV parsing.

Produces: TREND RESEARCH BRIEF with level-calibrated question mix and market signals.

**B) Interviewer Background Research (conditional):**
Activate if the candidate mentions knowing their interviewer:
- *"I'm interviewing with [Name]"*
- *"Can you research my interviewer?"*
- *"My interviewer is [Name/Title/Company]"*

If activated:
1. Read `references/interviewer-background-research.md`
2. Execute the interviewer research protocol (8-15 web searches)
3. Produce: INTERVIEWER PROFILE with persona adaptation recommendations
4. Share research summary with candidate before configuring interview

If NOT activated (candidate doesn't know interviewer):
- Skip this sub-agent
- Proceed with generic persona from `interviewer-persona.md`

**Both research briefs feed into the Question Generator:**
- Trend Research → determines WHAT to ask (question mix, level calibration)
- Interviewer Research → determines HOW to ask it (style, emphasis, priorities)
```

### 4. Update Step 1d (Sub-agents activation)

**Current text:**
```markdown
### 1d. Activate sub-agents internally

Once CV, research brief, and config are set, mentally activate:

**CV Parser** → structured candidate profile  
**Research Agent** → level-calibrated question trends + AI-era signals  
**Profile Analyser** → predicted strengths, likely gaps, red flags to probe  
**Question Generator** → session plan built from base bank + research findings  
**Live Evaluator** → running scorecard (never shown mid-interview)  
**Gap Tracker** → which rubric dimensions have been tested vs untested  
**Pivot Controller** → signals when to change domain or deepen a thread  
**Feedback Synthesiser** → activated at end of session only  
```

**Updated text:**
```markdown
### 1d. Activate sub-agents internally

Once CV, research briefs, and config are set, mentally activate:

**CV Parser** → structured candidate profile  
**Trend Research Agent** → level-calibrated question trends + AI-era signals  
**Interviewer Research Agent** → persona adaptation (if interviewer known)  
**Profile Analyser** → predicted strengths, likely gaps, red flags to probe  
**Question Generator** → session plan built from base bank + both research findings  
**Persona Adapter** → adjusts interview style based on interviewer profile  
**Live Evaluator** → running scorecard (never shown mid-interview)  
**Gap Tracker** → which rubric dimensions have been tested vs untested  
**Pivot Controller** → signals when to change domain or deepen a thread  
**Feedback Synthesiser** → activated at end of session only  
```

### 5. Add trigger detection logic

Add this section after Step 1a and before Step 1b:

```markdown
### 1a.5. Detect if Interviewer is Known

After parsing the CV, check if the candidate has mentioned their interviewer:

**Trigger phrases:**
- "I'm interviewing with [Name]"
- "My interviewer is [Name/Title]"
- "Can you research [Name]?"
- "[Name] will be interviewing me"
- Provides LinkedIn URL or Twitter handle
- "I'm meeting with the [Title] at [Company]"

If detected:
→ Set flag: `interviewer_research_needed = true`
→ Extract: `interviewer_name`, `company`, `role` (if provided)

If NOT detected:
→ Set flag: `interviewer_research_needed = false`
→ Use generic interviewer persona

**Clarification protocol:**
If the candidate says something ambiguous like "I'm interviewing at Google next week":
- Do NOT auto-trigger interviewer research
- Optionally ask: *"Do you know who'll be interviewing you? If you do, I can research their background to help you prepare."*
```

### 6. Update the report template

**Add new section to report-template.md:**

Add this section after the introduction:

```markdown
## Interview Context

**Interview adapted for:** [Generic / Specific interviewer name]

[If specific interviewer:]
This mock interview was adapted based on research into [Interviewer Name]'s 
professional background, product philosophy, and public statements. The question 
selection, follow-up style, and evaluation emphasis were calibrated to reflect 
their likely interview approach.

Research sources: [List key sources]
Research confidence: [HIGH / MEDIUM / LOW]
```

---

## Execution Flow Diagram

```
START: Candidate uploads CV and requests interview
    ↓
Step 1a: Parse CV → Extract seniority, domain, experience
    ↓
Step 1a.5: Check for interviewer mention
    ↓
    ├─ Interviewer mentioned? → YES
    │   ↓
    │   Step 1b-A: Run Trend Research (8 min)
    │   Step 1b-B: Run Interviewer Research (10 min) ← NEW
    │   ↓
    │   Synthesize BOTH research briefs
    │   ↓
    │   Share Interviewer Profile summary with candidate
    │   ↓
    │
    └─ Interviewer mentioned? → NO
        ↓
        Step 1b: Run Trend Research only (8 min)
        ↓
        Use generic interviewer persona
        ↓
Step 1c: Configure interview (type, difficulty, duration)
    ↓
Step 1d: Activate all sub-agents with persona adaptation
    ↓
Step 2: Conduct interview (adapted style if interviewer known)
    ↓
Step 3: Generate feedback report (note if adapted for specific interviewer)
    ↓
END: Deliver report to candidate
```

---

## Key Decision Points

### When to run Interviewer Research?

**Always run if:**
- Candidate explicitly names a person
- Candidate provides a LinkedIn/Twitter/profile link
- Candidate asks "can you research my interviewer?"

**Never run if:**
- Candidate only mentions company, not person
- Generic prep request with no interviewer context
- Candidate explicitly says they don't know who's interviewing

**Ask for clarification if:**
- Candidate mentions title/role but not name ("I'm meeting with the VP of Product")
- Ambiguous mention that could go either way

### How to combine both research briefs?

**Priority rules:**
1. **Question mix:** Start with Trend Research recommendations
2. **Style adaptation:** Apply Interviewer Research modifications on top
3. **Conflict resolution:** If they conflict (e.g., Trend says "low estimation" but Interviewer loves estimation), defer to Interviewer Research
4. **Confidence weighting:** If Interviewer Research is LOW confidence, lean more heavily on Trend Research

**Example synthesis:**

```
TREND RESEARCH says:
- Principal level → emphasize product sense, minimize estimation
- AI-era role → include AI product thinking questions

INTERVIEWER RESEARCH says:
- This person values technical depth highly
- This person is known for estimation questions despite seniority

SYNTHESIS:
- Use principal-level product sense questions (Trend)
- Add technical depth probing (Interviewer)
- Include ONE estimation as analytical warmup (Interviewer override)
- Include AI-era questions (Trend + Interviewer alignment)
```

---

## Testing Protocol

### Verification checklist before deploying:

**Trigger detection:**
- [ ] Correctly identifies when interviewer is mentioned
- [ ] Correctly skips when interviewer is not mentioned
- [ ] Asks for clarification in ambiguous cases
- [ ] Handles edge cases (title without name, company without person)

**Research execution:**
- [ ] Completes research in 8-12 minutes
- [ ] Produces structured Interviewer Profile
- [ ] Synthesizes findings into actionable summary
- [ ] Cites sources properly
- [ ] Handles limited information gracefully
- [ ] Stops and clarifies for ambiguous identity

**Persona adaptation:**
- [ ] Modifies question emphasis based on research
- [ ] Adjusts interview style appropriately
- [ ] Incorporates specific questions from research
- [ ] Balances adaptation without overfitting
- [ ] Falls back gracefully if research yields little

**Candidate briefing:**
- [ ] Shares research summary naturally
- [ ] Provides actionable preparation recommendations
- [ ] Discloses sources transparently
- [ ] Includes ethical disclaimer
- [ ] Sets appropriate confidence level

**Report generation:**
- [ ] Notes if interview was adapted
- [ ] Includes interviewer context section
- [ ] Evaluates against adapted expectations
- [ ] Maintains calibration integrity

### Test scenarios:

**Scenario 1: Well-known PM with substantial content**
- Example: Shreyas Doshi, Lenny Rachitsky, Marty Cagan
- Expected: HIGH confidence, detailed profile, specific adaptations

**Scenario 2: Senior PM with limited public presence**
- Example: Director at mid-size company, modest LinkedIn
- Expected: MEDIUM confidence, inferred style, general adaptations

**Scenario 3: No interviewer information**
- Example: "I'm interviewing at Meta next month"
- Expected: Optionally ask if they know interviewer, otherwise skip

**Scenario 4: Ambiguous mention**
- Example: "I'm meeting with the Head of Product"
- Expected: Ask for name or LinkedIn to research

**Scenario 5: Multiple people with same name**
- Example: "I'm interviewing with John Smith"
- Expected: Ask for disambiguation (company, LinkedIn, title)

---

## Common Integration Mistakes to Avoid

**❌ Mistake 1: Running interviewer research on every session**
- This is expensive (15+ web searches) and often unnecessary
- Only run when triggered by explicit interviewer mention

**❌ Mistake 2: Overfitting to the specific interviewer**
- The goal is authentic preparation, not mimicry
- Balance persona adaptation with good fundamental PM evaluation

**❌ Mistake 3: Not handling limited information gracefully**
- Many people won't have substantial public presence
- Don't force a detailed profile when information is sparse
- Fall back to role/company inference

**❌ Mistake 4: Not disclosing the adaptation to the candidate**
- Always tell the candidate you've researched their interviewer
- Share the summary and sources
- This builds trust and helps them prepare

**❌ Mistake 5: Ignoring ethical boundaries**
- Stick to publicly available professional information only
- Don't search for personal details
- Don't present speculation as fact

**❌ Mistake 6: Not synthesizing both research briefs**
- Trend Research and Interviewer Research must work together
- Don't let one override the other blindly
- Synthesize into a coherent session plan

---

## Performance Optimization

### Minimize latency:

**Parallel execution:**
- Run Trend Research and Interviewer Research simultaneously
- Both should complete in ~10 minutes combined

**Early termination:**
- If first 3 searches yield nothing, surface this to candidate
- Ask if they have additional context (LinkedIn, blog URL)
- Don't waste 15 searches on a dead end

**Cache consideration:**
- For very well-known PMs, consider caching profiles
- Update cache quarterly to keep current
- Note: This is future optimization, not v1 requirement

### Search efficiency:

**Prioritize high-signal sources:**
1. LinkedIn profile (professional background)
2. Company blog / Medium (first-party content)
3. Twitter/X (public voice)
4. Podcast appearances (philosophy)
5. Glassdoor (interview style, if available)

**Stop early if:**
- First 5 searches yield comprehensive profile
- Person has very limited online presence after 8 searches
- Identity can't be verified after 3 searches

---

## Success Metrics

Track these to measure sub-agent effectiveness:

**Quantitative:**
- Trigger accuracy: % of correct trigger vs false positive/negative
- Research completion time: avg. time to complete research
- Search efficiency: avg. searches needed per profile
- Confidence distribution: HIGH / MEDIUM / LOW confidence rates

**Qualitative:**
- Candidate feedback: Did research help them prepare?
- Interview realism: Did adapted style feel authentic?
- Preparation value: Did briefing provide actionable insights?
- Ethical compliance: Any boundary violations?

**Target benchmarks (suggested):**
- Trigger accuracy: >95%
- Research time: <12 minutes
- Search efficiency: <15 searches/profile
- HIGH confidence: >40% of researched profiles
- Candidate satisfaction: >4.5/5 when research activated

---

## Maintenance and Updates

### Quarterly review:

**Check for:**
- Changes in major PM thought leaders (new voices emerging)
- Platform changes (Twitter → X changes, LinkedIn updates)
- Search pattern evolution (what queries work best)
- New public content sources (new podcasts, blogs)

**Update:**
- Search query templates if patterns change
- Source prioritization if new platforms emerge
- Example interviewer profiles for testing

### Incident response:

**If research fails:**
- Log the failure case
- Identify root cause (identity ambiguity, limited data, search failure)
- Update protocol to handle similar cases
- Communicate limitation to candidate

**If adaptation misses:**
- Review actual interview feedback
- Compare predicted vs actual style
- Refine inference logic
- Update persona adaptation rules

---

## Rollout Plan

### Phase 1: Soft launch (Week 1-2)
- Deploy to skill, monitor trigger detection
- Manually review first 10 interviewer profiles generated
- Collect candidate feedback on research value
- Fix any critical bugs in trigger or research flow

### Phase 2: Validation (Week 3-4)
- Validate persona adaptation quality
- Test with known interviewers (Shreyas, Lenny, etc.)
- Measure research time and search efficiency
- Refine based on early feedback

### Phase 3: Full deployment (Week 5+)
- Roll out broadly
- Monitor success metrics
- Iterate based on usage patterns
- Document learned best practices

---

## Documentation for Users

### What to add to skill description:

**Update the skill description to mention:**

```markdown
ALWAYS use this skill when a CV or resume is uploaded alongside any request 
to be interviewed or tested.

NEW: If you know who will be interviewing you, mention their name or provide 
their LinkedIn profile. The skill will research their background, product 
philosophy, and interview style to help you prepare more effectively and 
adapt the mock interview to reflect their approach.
```

### User-facing messaging:

When the sub-agent activates, the candidate should see:

```
I see you're interviewing with [Name]. Let me research their background 
and interview style to help you prepare.

[8-12 minutes later]

I've completed my research on [Name]. Here's what will help you prepare:
[Summary provided]

Based on this research, I'll adapt my interview style to reflect their 
approach. Ready to configure the interview?
```

---

## Summary: Integration Checklist

Use this checklist when implementing:

**Files to create/modify:**
- [ ] Create `references/interviewer-background-research.md`
- [ ] Update `SKILL.md` Step 0 (add reference file)
- [ ] Update `SKILL.md` Step 1a.5 (add trigger detection)
- [ ] Update `SKILL.md` Step 1b (split into A and B sub-agents)
- [ ] Update `SKILL.md` Step 1d (add Interviewer Research Agent)
- [ ] Update `references/report-template.md` (add interview context section)

**Logic to implement:**
- [ ] Trigger detection for interviewer mentions
- [ ] Interviewer research protocol (15-step search pattern)
- [ ] Profile synthesis and structuring
- [ ] Persona adaptation logic
- [ ] Research brief combination (Trend + Interviewer)
- [ ] Candidate briefing generation
- [ ] Ethical boundary enforcement

**Testing to complete:**
- [ ] Test all 5 scenarios (well-known, limited, none, ambiguous, duplicate)
- [ ] Validate trigger accuracy
- [ ] Verify research time <12 min
- [ ] Confirm persona adaptation quality
- [ ] Check ethical compliance

**Monitoring to set up:**
- [ ] Track trigger accuracy
- [ ] Monitor research completion time
- [ ] Log confidence distribution
- [ ] Collect candidate feedback

---

This integration turns generic interview prep into personalized preparation when the candidate knows their interviewer — a significant value add for the skill.
