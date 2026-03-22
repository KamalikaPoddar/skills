# Life Skills
A repo of all the different skills i have created to aide me in my day to day work, personal projects, hobbies and more. Basically my way to become an AI native human.

## AI Native PM coach
**A structured coaching system for experienced Product Managers who want to become genuinely AI-native — not AI-adjacent.**

This is not a chatbot persona. It is a complete coaching protocol: a diagnostic intake that cuts through self-flattery, two coaching tracks mapped to your actual situation, five frameworks applied invisibly, a hard accountability system, and a longitudinal memory architecture that makes every session smarter than the last.
 
Built for Claude. Portable to ChatGPT, Gemini, and any instruction-following LLM.

### Who This Is For
 
**Working PMs with existing product experience** — across any domain, any industry, any seniority level — who want to close the gap between where they are and what it actually means to be AI-native.
 
This coaching system operates on two tracks:
 
- **Track A — Personal Project Builder:** You are building (or seriously intending to build) your own AI product. The coaching centres on what you're building, who for, whether the AI component is real or decorative, and whether you have a business or a mood board.
 
- **Track B — In-Role AI-Native Builder:** You are not independently building, but you want to become meaningfully more effective in your current role — shipping better AI products, championing the right bets internally, building the kind of portfolio of judgment that makes you genuinely AI-native rather than AI-adjacent.
 
**This is explicitly NOT for people trying to break into Product Management.** If that's you, this coaching system will redirect you clearly.
 
---
 
### What Makes This Different
 
Most AI coaching prompts give you an enthusiastic generalist who validates your ideas, lists frameworks, and ends with "what do you think?" This is not that.
 
This system is built on three principles that most coaching prompts skip:
 
**1. Diagnostic before advisory.** The intake does not ask you to describe yourself. It asks questions that reveal how you actually think under pressure — the consequential decision you had to make with incomplete information, the product that failed and what you got wrong specifically, the gap between how your skip-level sees you and how your closest peer sees you. Declarative questions get you the flattering version. Diagnostic questions get the truth.
 
**2. Longitudinal memory without a database.** Most AI sessions start from zero. This system maintains continuity across sessions through a two-file architecture: a user-facing session log you bring back each time, and a private Coach's Vault — a running record of working hypotheses, active blind spots, and longitudinal observations that never gets shown to you directly but makes every subsequent session substantially smarter.
 
**3. Accountability that does not move on.** At the end of every session, specific takeaways are assigned with unambiguous completion criteria. At the start of the next session, those takeaways are checked before anything else happens. If you didn't complete them, that is the session — not a brief acknowledgment before moving to more interesting content.

## How to Use:
### Claude (claude.ai)
 
1. Download `ai-native-pm-coach.skill`
2. In Claude, go to **Settings → Skills → Add Skill**
3. Upload the `.skill` file
4. The skill activates automatically when Claude detects a PM coaching context
 
**For subsequent sessions:** Upload both your `session-log.md` and `coach-vault.md` files at the start of the conversation before saying anything else. Claude will read both silently and begin from where you left off.
 
---
 
### ChatGPT
 
1. Open the `ai-native-pm-coach/SKILL.md` file
2. Copy the full contents (everything below the YAML frontmatter `---`)
3. Start a new GPT-4 conversation and paste as the first message, prefixed with:
 
   > *"For this conversation, you are operating under the following coaching protocol. Read it fully before responding to anything."*
 
4. Then paste the skill contents
5. Begin your session
 
**For memory:** ChatGPT has no native file upload for custom instructions in standard chat. Paste the contents of your `session-log.md` and `coach-vault.md` directly into your first message, clearly labelled, before beginning.
 
**For persistent use:** Create a Custom GPT and paste the SKILL.md contents into the System Prompt field.
 
---
 
### Gemini
 
1. Open the `ai-native-pm-coach/SKILL.md` file
2. Copy the full contents below the YAML frontmatter
3. In Gemini Advanced, use a Gem (custom AI) and paste the skill contents as the system instructions
4. Save the Gem and use it for all coaching sessions
 
**For memory:** At the start of each session, upload your `session-log.md` and `coach-vault.md` files directly in the conversation. Gemini Advanced supports file uploads. Label them clearly in your opening message.
 
---
 
### Any Other Instruction-Following LLM
 
The SKILL.md is plain markdown. The coaching protocol works with any model that can follow detailed system-level instructions. The minimum capability requirement is:
 
- Ability to accept a long system prompt or initial instruction block
- Ability to read uploaded or pasted markdown files
- Reasoning quality sufficient to follow multi-step conditional logic
 
Paste the contents of SKILL.md as your system prompt or first message. Bring the session files each time.
 
---
 
## Starting Your First Session
 
Once the skill is loaded, begin with:
 
> *"I'm a Product Manager and I want to start a coaching session."*
 
The coach will run the diagnostic intake — six questions, asked one at a time, designed to reveal how you actually think rather than how you describe yourself. It will take 20–30 minutes for a thorough first session. That intake is the foundation everything else builds on. Don't rush it.
 
At the end of the session, you'll receive two files to save:
- Your Session Log
- The Coach's Vault
 
Keep them together. Bring them both next time.
 
---
 
## What To Expect
 
**Session 1:** Diagnostic intake, track routing (A or B), first hard observation, initial takeaways assigned.
 
**Sessions 2–4:** Deep work on the highest-leverage problem. Accountability check at the start of every session. The coaching gets more specific and more confrontational as the coach builds a clearer picture of your patterns.
 
**Sessions 5+:** The longitudinal observations start to matter. The coach is tracking how you respond to challenge, what you avoid, how your thinking is evolving. The coaching at this point is substantially different from what a fresh-context session could produce.
 
---
 
## A Note on Tone
 
This coaching system is built around a specific philosophy: the coach who says the hard thing, not the comfortable thing.
 
That means assumptions get challenged. Vague explanations get pushed back on. Missed takeaways get named directly before the session moves on. The intake is designed to cut through the polished version of your career and find the honest one.
 
If you are looking for a supportive thought partner who reflects your ideas back with enthusiasm, this will feel uncomfortable. That discomfort is the point. The coaching recalibrates when you're already down — it's not blunt for its own sake. But it does not validate poor decisions to be encouraging, and it does not skip accountability because the topic you want to talk about is more interesting.
 
---
 
## Contributing
 
Issues, improvements, and framework additions welcome. If you have adapted this for a specific domain (fintech, healthtech, B2B SaaS, etc.) and want to contribute a specialised variant, open a PR.
 
When contributing changes to `SKILL.md`, please maintain:
- The two-file session architecture (session log + coach vault)
- The Track A / Track B routing structure  
- The accountability protocol sequence
- The principle that diagnostic questions replace declarative ones
 
---
 
## License
 
MIT. Use it, modify it, build on it. If you deploy a variant, a link back here is appreciated but not required.
 
---
 
*Built with the conviction that most AI coaching prompts are too agreeable to be useful.*

