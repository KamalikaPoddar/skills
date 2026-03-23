# Skills
 
A personal library of structured AI skills — portable, version-controlled, and built to work across Claude, ChatGPT, Gemini, and any instruction-following LLM.
 
Each skill is a self-contained coaching or workflow system: a detailed instruction protocol, a set of reference files, and everything an AI model needs to do something genuinely useful rather than generically helpful.
 
This is my way of building an AI-native life — not by prompting better, but by encoding how I think into reusable systems that get smarter with use.
 
---
 
## What Is a Skill?
 
A skill is a structured prompt system packaged as a `.skill` file — a renamed zip that contains:
 
```
skill-name/
├── SKILL.md                  ← The full instruction protocol for the AI
└── references/               ← Supporting files the AI loads at runtime
    ├── template-1.md
    └── template-2.md
```
 
`SKILL.md` is the core: a detailed system prompt that defines the AI's persona, session flow, decision logic, frameworks, and output format. The `references/` folder holds templates and continuity files that get uploaded alongside the skill to give the AI context it can't hold between sessions.
 
Skills are plain markdown under the hood. They work anywhere.
 
---
 
## Skill Library
 
| Skill | What It Does | Track |
|---|---|---|
| [AI Native PM Coach](./skills/ai-native-pm-coach/) | Structured coaching for experienced PMs becoming AI-native builders | Coaching |
| [Rapid Prototyping](./skills/pm-rapid-prototype-builder/) | Turn your concept note or PRD into a working, on-brand, stakeholder-ready prototype in hours not weeks | Building |
 
*More skills added as I build and test them. See [Contributing](#contributing) if you want to add your own.*
 
---
 
## How to Use a Skill
 
### Step 1 — Get the skill files
 
Each skill lives in its own folder under `skills/`. You need two things:
- The `SKILL.md` file (the instruction protocol)
- Any files from the `references/` folder that apply to your session
 
You can download them individually from GitHub, or clone the whole repo:
 
```bash
git clone https://github.com/YOUR-USERNAME/skills.git
```
 
---
 
### Step 2 — Load into your AI of choice
 
#### Claude (claude.ai) — Native Support
 
Claude supports `.skill` files natively.
 
1. Download the `.skill` file from the skill's folder
2. Go to **Settings → Skills → Add Skill**
3. Upload the `.skill` file
4. The skill activates automatically when Claude detects the right context
 
**For sessions with memory:** Upload your session continuity files (e.g. `session-log.md`, `coach-vault.md`) at the very start of the conversation — before your first message. Claude reads them silently and picks up from where you left off.
 
---
 
#### ChatGPT
 
ChatGPT does not have a native skill format, but the markdown protocol works directly.
 
**Option A — Single session:**
1. Open the skill's `SKILL.md` file
2. Copy everything below the YAML frontmatter (below the second `---`)
3. Start a new conversation and send it as your first message, prefixed with:
   > *"For this conversation, operate under the following protocol. Read it fully before responding to anything."*
4. Paste the skill contents, then begin
 
**Option B — Persistent (recommended):**
1. Create a Custom GPT at [chat.openai.com/gpts](https://chat.openai.com/gpts)
2. Paste the `SKILL.md` contents into the **System Prompt** field
3. Save and use the Custom GPT for all sessions with this skill
 
**For sessions with memory:** Paste the contents of your continuity files (e.g. `session-log.md`, `coach-vault.md`) directly into your opening message, clearly labelled, before beginning.
 
---
 
#### Gemini
 
1. Open the skill's `SKILL.md` file
2. Copy everything below the YAML frontmatter
3. In Gemini Advanced, create a **Gem** and paste the skill contents as the system instructions
4. Save the Gem and use it for all sessions
 
**For sessions with memory:** Gemini Advanced supports file uploads. Upload your continuity files at the start of each session and label them clearly in your opening message.
 
---
 
#### Any Other LLM
 
The `SKILL.md` protocol is plain markdown. It works with any model that can:
- Accept a long system prompt or initial instruction block
- Read uploaded or pasted markdown files
- Follow multi-step conditional logic
 
Paste the contents of `SKILL.md` as your system prompt or opening message. Include continuity files in the same message if your session has prior context.
 
---
 
### Step 3 — Start the session
 
Each skill's own README has a specific starting prompt. In general, be direct about what you want:
 
> *"I want to start a [skill name] session."*
 
The skill takes it from there.
 
---
 
## Skill Continuity (Memory Across Sessions)
 
AI models have no memory between conversations. Skills that involve ongoing work — coaching, long projects, iterative processes — solve this with a **continuity file system**: structured markdown files you save locally and re-upload at the start of each new session.
 
At the end of any session that generates continuity files, the AI outputs fully-populated versions for you to save. Bring them next time. The skill reads them silently at session start and picks up with full context.
 
Each skill documents its own continuity files in its README.
 
---
 
## Skills In Progress
 
Skills I'm building or planning to add:
 
- `kamalika-career-strategist` — Personal career strategy for job search, CV alignment, and role targeting
- `agentpay-strategist` — Product strategy coach for the AgentPay platform
- `writing-editor` — Structured editorial feedback with voice preservation
 
If you want to suggest a skill or contribute one, see below.
 
---
 
## Contributing
 
### Adding a new skill
 
Skills in this library follow a consistent structure. To contribute:
 
**1. Fork the repo and create a branch**
```bash
git checkout -b skill/your-skill-name
```
 
**2. Create the skill folder**
```
skills/
└── your-skill-name/
    ├── SKILL.md
    ├── README.md
    └── references/
        └── (any template or continuity files)
```
 
**3. Write `SKILL.md` — the core instruction protocol**
 
A good `SKILL.md` must define:
- **Persona** — who the AI is, what expertise it has, what it is explicitly NOT
- **Session flow** — a clear step-by-step structure the AI follows every session, without exception
- **Frameworks** — the diagnostic or analytical tools the AI applies (invisibly, not recited)
- **Output format** — exactly what the AI produces at session close, including any continuity files
- **Boundaries** — what this skill does not do
 
YAML frontmatter is required at the top:
```yaml
---
name: your-skill-name
description: >-
  One paragraph. What this skill does, who it's for, when to invoke it,
  and what phrases or contexts should trigger it. Be specific.
---
```
 
**4. Write a `README.md` for the skill**
 
Each skill needs its own README covering: what it does, who it's for, how to start, what to expect, and how session continuity works (if applicable).
 
**5. Package as a `.skill` file (optional, for Claude)**
```bash
cd skills/
zip -r your-skill-name.skill your-skill-name/
```
 
**6. Add the skill to the table in this README**
 
Update the Skill Library table with your skill's name, description, and track.
 
**7. Open a PR**
 
Describe what the skill does and include a brief note on how you tested it across at least one LLM.
 
---
 
### Improving an existing skill
 
If you've found a flaw, a missing case, or a better framework — open an issue first to describe what's broken and what you'd change. For significant structural changes, discuss before building.
 
When modifying any skill, preserve:
- The session flow sequence (don't reorder steps without a strong reason)
- The continuity file architecture if one exists
- The principle that the skill should do something specific, not something generic
 
---
 
### Contribution standards
 
- Skills must be tested — don't submit a protocol you haven't run at least five real sessions with
- Skills must have clear scope boundaries (what they do NOT do is as important as what they do)
- No skills that are just "be a better [role]" — the value is in the structure, not the persona
- Respect the `.skill` packaging format for Claude compatibility
 
---
 
## Repo Structure
 
```
skills/
├── README.md                              ← You are here
└── skills/
    └── ai-native-pm-coach/
        ├── SKILL.md                       ← Full instruction protocol
        ├── README.md                      ← Skill-level documentation
        ├── ai-native-pm-coach.skill       ← Packaged for Claude upload
        └── references/
            ├── session-log-template.md    ← User-facing continuity file
            └── coach-vault-template.md    ← Private coach continuity file
```
 
---
 
## License
 
MIT. Use these skills, adapt them, build on them. If you publish a fork or variant publicly, a link back is appreciated but not required.
 
---
 
*This repo is how I encode judgment into systems. The goal isn't better prompts — it's protocols that do real work.*
