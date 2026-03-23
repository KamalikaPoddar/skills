# PM Interviewer Skill

A rigorous mock interview system for product managers. Conducts realistic, deep interviews calibrated to your seniority level and domain — then generates a structured feedback report with a personal 90-day improvement roadmap.

---

## What it does

Simulates a senior interviewer who has been building digital products since the 1990s and AI-native products since 2018. Sharp, probing, no softening. Follows up on vague answers, challenges polished narratives, and pushes candidates to show the work behind the outcome.

At the end of every session, produces a downloadable markdown report with scores across 9 dimensions, specific evidence from your answers, identified gaps, and a concrete development roadmap.

---

## How to use it

1. Upload your CV or resume
2. Say **"interview me"** — optionally specify type and difficulty (see below)
3. The skill handles the rest

**Interview types**
- `product skills` — strategy, roadmapping, prioritisation, metrics, execution
- `technical` — APIs, system design, data, analytics
- `behavioural` — leadership, conflict, failure, influence
- `full-spectrum` — all of the above (closest to a real loop)

**Difficulty levels**
- `standard` — senior PM, 5–8 years
- `hard` — principal / director level
- `brutal` — VP / CPO, no hints, no softening

**Duration**
- `30 min` — 5–7 questions
- `60 min` — 10–14 questions
- `90 min` — full loop, 18–22 questions

---

## What's inside

```
pm-interviewer/
├── SKILL.md                          — main orchestration logic
└── references/
    ├── interviewer-persona.md        — voice, behaviour, what impresses, what raises red flags
    ├── research-subagent.md          — live interview trend research + seniority calibration rules
    ├── question-banks.md             — 60+ questions across 6 sections, tagged by difficulty
    ├── evaluation-rubrics.md         — 9-dimension scoring system
    └── report-template.md            — feedback report structure
```

---

## Sub-agents

The skill runs 8 sub-agents in sequence:

| Sub-agent | Role |
|---|---|
| CV Parser | Extracts experience, metrics, and anomalies from the uploaded resume |
| Research Agent | Searches current interview trends by level and domain before every session |
| Profile Analyser | Maps predicted strengths and red flags to probe |
| Question Generator | Builds personalised session plan from base bank + research findings |
| Live Evaluator | Scores 9 rubric dimensions silently throughout the session |
| Gap Tracker | Flags untested dimensions and ensures coverage |
| Pivot Controller | Decides when to change domain or go deeper on a thread |
| Feedback Synthesiser | Generates the markdown report at end of session |

---

## Seniority calibration

The Research Agent applies different question mixes by level. The most important rule:

> **Guesstimates are a junior signal.** For principal level and above, they are used at most once and only to test analytical rigour specifically. Product sense, design thinking, full product lifecycle, platform strategy, and AI-era product thinking dominate senior sessions.

| Level | Guesstimates | Product sense | Strategy | AI product |
|---|---|---|---|---|
| APM / PM (0–4 yrs) | High | High | Low | Low |
| Senior PM (4–8 yrs) | Medium | High | High | Medium |
| Principal / Director (8–14 yrs) | Low | High | High | High |
| VP / CPO (14+ yrs) | Never | Medium | Dominant | High |

---

## The feedback report

Every session ends with a `.md` report containing:

- **Hire signal** at the interviewed level and one level above
- **Scorecard** across 9 dimensions (1–5)
- **Strengths** — specific moments from the interview with reasons
- **Gaps** — precisely named, with evidence from your answers
- **90-day roadmap** — concrete actions, not generic advice
- **One honest thing** — what you most need to hear that you probably haven't been told

---

## Version

`v2` — adds Research Sub-Agent, seniority calibration table, product sense / design thinking emphasis for senior levels, and AI-era question patterns for 2025–2026 interviews.
