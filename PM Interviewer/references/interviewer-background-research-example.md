# Worked Example: Interviewer Background Research Sub-Agent

This example demonstrates how the sub-agent would execute for a real scenario.

---

## Scenario

**Candidate:** Kamalika Poddar, 12 years experience, Principal PM level  
**Interviewer:** Shreyas Doshi (hypothetical — using a well-known PM with substantial public content)  
**Context:** Kamalika is interviewing for a Senior PM role and mentions: *"I'm interviewing with Shreyas Doshi next week. Can you help me prepare?"*

---

## Execution: Phase-by-Phase

### Phase 1: Identity Verification (2 searches)

**Search 1:** `"Shreyas Doshi" product manager LinkedIn`

**Findings:**
- Current: Independent product advisor and coach
- Previously: Stripe (PM leadership), Twitter (Product Lead), Yahoo (PM)
- ~15 years in product management
- Based in San Francisco Bay Area
- Domain: Consumer products, B2B SaaS, payments, growth

**Search 2:** `"Shreyas Doshi" Twitter`

**Findings:**
- Active Twitter/X presence: @shreyas
- 200K+ followers
- Prolific writer on PM topics
- Strong public voice and clear philosophies

**Verification:** ✅ Identity confirmed, substantial public presence

---

### Phase 2: Professional Background (3 searches)

**Search 3:** `"Shreyas Doshi" career path Stripe Twitter Yahoo`

**Findings:**
- Started at Yahoo as PM (early-mid 2000s)
- Moved to Twitter as Product Lead during growth era
- Joined Stripe as PM leadership, helped scale product org
- Went independent in ~2020 to focus on PM coaching and advising
- Career arc: Big company → growth stage → enterprise scale → independent

**Search 4:** `"Shreyas Doshi" interview joined Stripe`

**Findings:**
- Known for building high-performing PM teams
- Helped scale Stripe's product org during rapid growth
- Left to focus on helping other PMs level up
- Has spoken about the craft of product management extensively

**Search 5:** `site:linkedin.com/in "shreyas-doshi"`

**Findings:**
- Strong engineering and computer science background
- MBA from Wharton
- Pattern: Long tenures (4-6 years per company)
- Built teams at scale (managed 30+ PMs at Stripe)

**Career Trajectory Signals:**
- Deep IC experience before moving to leadership
- Values long-term impact over job hopping
- Made contrarian move to go independent at peak of career
- Engineering→MBA→Product path (values technical depth)

---

### Phase 3: Product Philosophy & Public Voice (5 searches)

**Search 6:** `"Shreyas Doshi" blog OR article product management`

**Findings:**
- Does not have a traditional blog
- Primary content is on Twitter and occasional guest posts
- Known for Twitter threads on PM topics

**Search 7:** `"Shreyas Doshi" twitter PM frameworks OR product thinking`

**Findings (sample from his actual Twitter content):

**Key philosophies identified:**

1. **The LNO Framework (Leverage, Neutral, Overhead)**
   - Shreyas categorizes work into three types:
   - Leverage work: High impact, compounds over time
   - Neutral work: Keeps things running, no net gain
   - Overhead work: Necessary but draining
   - PMs should maximize leverage work

2. **Product Thinking vs Product Doing**
   - Strong distinction between strategic thinking and execution mechanics
   - Values deep product sense over process mastery
   - Criticizes "PM as project manager" mentality

3. **Ikigai of Product Management**
   - Intersection of: (1) What you're great at, (2) What the world needs, (3) What you can get paid for, (4) What you love
   - Encourages PMs to find this intersection intentionally

4. **Pre-Mortems over Post-Mortems**
   - Advocates for thinking through failure scenarios before launch
   - "What could go wrong?" as a core PM skill

5. **Strong Opinions on PM Career Development**
   - Values craft over titles
   - Skeptical of fast career progression without depth
   - Emphasizes learning over climbing

**Search 8:** `"Shreyas Doshi" podcast OR interview OR talks`

**Findings:**
- Guest on Lenny's Podcast (multiple times)
- Lenny Rachitsky podcast: Discussed PM career growth, impact, mental models
- First Round Review interview: On building product culture
- Various conference talks on product leadership

**Key quotes extracted:**
- "Most PMs over-index on features and under-index on product thinking"
- "Your job is not to build things. Your job is to create impact."
- "The best PMs think in bets, not certainties"
- On AI: "AI will automate product execution, but not product vision"

**Search 9:** `"Shreyas Doshi" what makes great PM OR hiring PMs`

**Findings:**
- Has written extensively about PM competencies
- Values: (1) Product sense, (2) Strategic thinking, (3) Execution excellence, (4) Influence
- Critical of: Surface-level metrics knowledge, process over substance, lack of user empathy
- Emphasizes: First principles thinking, ability to articulate trade-offs clearly

**Search 10:** `"Shreyas Doshi" criticism OR skeptical about product management`

**Findings:**
- Vocal critic of "product theater" — meetings and rituals that create illusion of progress
- Skeptical of over-reliance on frameworks without understanding principles
- Criticizes PMs who optimize for looking good vs being good
- Frustrated with "feature factory" culture

---

### Phase 4: Known Interview Style (3 searches)

**Search 11:** `"interviewed by Shreyas Doshi" OR "Shreyas Doshi interview questions"`

**Findings:**
- Limited direct Glassdoor data (he's not currently at a company conducting official interviews)
- Inferred from his coaching content: Likely Socratic style
- His Twitter threads suggest he values clarity of thinking over polish

**Search 12:** `"Shreyas Doshi" looks for in product managers OR hiring philosophy`

**Findings:**
- Public tweet: "I look for PMs who can articulate the 'why' before the 'what'"
- Values: Depth of product thinking, ability to handle ambiguity, strategic clarity
- Red flags (inferred from his criticism): Over-reliance on playbooks, shallow metrics knowledge, lack of user empathy

**Search 13:** `site:glassdoor.com "Shreyas Doshi" OR site:blind.com "Shreyas"`

**Findings:**
- No direct interview reports (expected, since he's independent)
- Stripe PM interviews generally emphasize: product sense, technical fluency, growth mindset
- Twitter community shares that his coaching style is direct and substance-focused

---

### Phase 5: Domain & Product Expertise (2 searches)

**Search 14:** `"Shreyas Doshi" Stripe products OR launched OR built`

**Findings:**
- At Stripe: Worked on payments infrastructure, developer experience, platform growth
- At Twitter: Growth products, user engagement, ad products
- Domains: B2B SaaS, payments, developer tools, consumer social, growth
- Technical fluency: Deep understanding of APIs, webhooks, platform architecture

**Search 15:** `"Shreyas Doshi" AI OR machine learning OR product strategy`

**Findings:**
- Has commented on AI's impact on PM role
- Views: AI will automate execution but amplify need for vision and judgment
- Expects PMs to understand AI capabilities, not necessarily build models
- Pragmatic, not hype-driven

---

## Structured Profile Output

```markdown
INTERVIEWER PROFILE — Shreyas Doshi, Independent Product Advisor
Research date: March 24, 2026
Research confidence: HIGH

═══════════════════════════════════════════════════════

PROFESSIONAL IDENTITY
- Current: Independent product advisor and coach (since ~2020)
- Previous: Stripe (PM Leadership, ~6 years) → Twitter (Product Lead, ~5 years) → Yahoo (PM, ~4 years)
- Career arc: Built depth at scale companies, then moved to independent practice
- Total experience: ~15 years in product management, ~20 years including engineering
- Seniority level: Former VP/Director level, now advisor to senior PMs and leaders
- Domain depth: B2B SaaS, payments, developer tools, consumer growth, platform products

CAREER TRAJECTORY SIGNALS
- Key pivots: Engineering → PM, big company → startup → scale → independent
- Tenure pattern: Long tenures (4-6 years), values depth over breadth
- Risk appetite: Contrarian move to go independent at career peak
- Track: IC → People leadership → Coaching/Advisory
- Education: Engineering degree + Wharton MBA (values both technical and business thinking)

═══════════════════════════════════════════════════════

PRODUCT PHILOSOPHY & VALUES

Primary beliefs about PM work:
- "Your job is not to build things. Your job is to create impact." — Emphasizes outcomes over outputs
- PMs should maximize "Leverage work" (LNO framework) — work that compounds over time
- Product thinking > Product doing — Strategy and vision matter more than process mastery
- Think in bets, not certainties — Embrace probabilistic thinking and pre-mortems
- Clarity of the "why" before the "what" — Purpose and strategy precede features

What he values in PMs:
- Deep product sense (user empathy, market understanding, intuition informed by data)
- Strategic thinking (ability to see 2-3 moves ahead, connect dots, articulate trade-offs)
- First principles thinking (not just applying frameworks, but understanding underlying logic)
- Intellectual honesty (owning uncertainty, admitting what you don't know)
- Craft mastery (caring deeply about the work, not just the title)

What he criticizes:
- "Product theater" — rituals that create illusion of progress without substance
- Feature factory culture — shipping without strategy
- Surface-level metrics knowledge — citing numbers without understanding drivers
- Over-reliance on frameworks without understanding principles
- Optimizing for looking good vs being good
- Fast career climbing without building depth

Framework and methodology preferences:
- LNO Framework (Leverage/Neutral/Overhead work categorization)
- Pre-mortems as a planning tool
- Product Ikigai (intersection of skill, need, payment, passion)
- Jobs-to-be-Done thinking (user needs over features)

Relationship with data and intuition:
- Balanced: Values data-informed decisions, not data-driven
- Believes great PMs blend quantitative rigor with qualitative insight
- Skeptical of metrics theater (dashboard worship without understanding)

AI and technology stance:
- Pragmatic about AI: It will automate execution, amplify need for vision
- Expects PMs to understand AI capabilities and constraints
- Not hype-driven, values substance over buzzwords

═══════════════════════════════════════════════════════

PUBLIC VOICE & CONTENT

First-party content found:
- Twitter/X: @shreyas — 200K+ followers, prolific threads on PM craft
- Podcast appearances: Lenny's Podcast (multiple), First Round Review
- Guest articles: Occasional pieces on PM career and craft
- No personal blog, but extensive Twitter content

Key themes in his public content:
1. PM career development and craft mastery
2. Product thinking frameworks and mental models
3. Critique of shallow PM practices and "product theater"
4. Strategic clarity and leverage thinking
5. Building high-performing product teams

Notable quotes:
- "Most PMs over-index on features and under-index on product thinking"
- "The best PMs think in bets, not certainties"
- "I look for PMs who can articulate the 'why' before the 'what'"
- On AI: "AI will automate product execution, but not product vision"

═══════════════════════════════════════════════════════

INTERVIEW STYLE (inferred)

Public statements about hiring:
- Values clarity of thinking over polish
- Looks for depth in answers, not rehearsed responses
- Wants to see how PMs handle ambiguity and trade-offs
- Emphasizes the "why" behind decisions

Inferred style based on background:
- Likely Socratic — asks follow-ups that probe reasoning
- Probably direct and substance-focused (not adversarial, but not softening)
- Will push on vague answers or framework name-dropping
- Values intellectual honesty — "I don't know" is better than BS
- Expects technical fluency given his engineering+payments background
- Will test for strategic thinking and product sense depth

═══════════════════════════════════════════════════════

DOMAIN & PRODUCT EXPERTISE

Products shipped:
- Stripe: Payments infrastructure, developer experience, platform growth
- Twitter: Growth products, engagement features, ad products
- Deep experience across 0→1, growth, and scale phases

Domain expertise:
- Payments and fintech (deep)
- Developer tools and platforms (deep)
- B2B SaaS (deep)
- Consumer social and growth (strong)
- Platform and ecosystem products (strong)

Technical depth:
- Engineering background (CS degree)
- Deep understanding of APIs, webhooks, platform architecture
- Can discuss technical trade-offs fluently
- Expects PMs to be technically credible with engineers

Scale operated at:
- Startup growth (Twitter early-ish)
- Hyper-growth (Stripe)
- Managed 30+ PMs at Stripe
- Built products used by millions (Twitter) and millions of businesses (Stripe)

Geographic markets:
- Primarily US market, but Stripe is global
- Understands platform businesses across markets

═══════════════════════════════════════════════════════

PERSONA ADAPTATION RECOMMENDATIONS

Based on this research, the mock interview should adapt:

1. **Question emphasis:**
   - High: Product sense, strategic thinking, "why before what"
   - Medium-High: Technical fluency (APIs, architecture), platform thinking
   - Medium: Metrics and experimentation, but probe for depth not surface knowledge
   - Low: Process questions, estimation (he values thinking, not arithmetic)

2. **Difficulty calibration:**
   - Set to "Hard" baseline — he expects deep thinking from senior PMs
   - Probe relentlessly on strategy and first principles
   - Don't accept polished answers; push for real thinking

3. **Style adaptation:**
   - Use Socratic questioning: "Why did you choose X over Y?"
   - Push on vague answers: "That sounds like the polished version. Give me the real version."
   - Probe for leverage thinking: "How did that work compound over time?"
   - Test for intellectual honesty: Reward "I don't know" over BS
   - Expect technical fluency: Use precise language about systems and APIs

4. **Follow-up themes:**
   - "What was the bet you were making?"
   - "How did you think about the trade-offs?"
   - "What would you do differently knowing what you know now?"
   - "Why that problem, not another problem?"
   - "How did you separate leverage work from overhead work?"

5. **Red flags for him:**
   - Shallow metrics knowledge (citing numbers without understanding drivers)
   - Framework name-dropping without first principles understanding
   - Feature-centric thinking without strategy
   - Lack of user empathy or customer understanding
   - Process over substance (talking about rituals not outcomes)
   - Optimizing for resume over impact

Specific questions he'd likely ask:

1. **Product Sense:**
   "Walk me through a product you use daily. Not the features — tell me what bet the PM made on user behavior, and whether it paid off."

2. **Strategic Clarity:**
   "Tell me about a time you had to choose between three good options with limited data. How did you think about the decision? What was the bet?"

3. **Leverage Thinking:**
   "Looking at your CV, you claim you 'increased user engagement by 40%'. Walk me through the work you did. How much of it was leverage work vs neutral vs overhead?"

4. **First Principles:**
   "You used [framework X] in that story. Explain why that framework exists — what problem was it solving? Could you have solved the problem without it?"

5. **Technical Fluency:**
   "You mentioned integrating with [system]. Walk me through the technical architecture. Where were the constraints? What trade-offs did you make?"

Topics Kamalika should prepare:

1. **Strategic clarity on AgentPay:**
   - Be ready to explain the "why" behind AgentPay's core architecture decisions
   - Articulate the bets being made on AI agent behavior and trust models
   - Show first principles thinking, not just regulatory compliance

2. **Leverage work examples:**
   - Identify 2-3 high-leverage projects from past roles
   - Be clear on how they compounded over time
   - Distinguish between leverage, neutral, and overhead in own work

3. **Technical depth:**
   - Be fluent on payment systems architecture (given his Stripe background)
   - Discuss API design choices, state machines, event-driven architecture
   - Show engineering credibility

4. **Product sense depth:**
   - Prepare examples of user empathy and discovery
   - Show ability to critique own products and decisions
   - Demonstrate strategic product thinking, not just execution

5. **Intellectual honesty:**
   - Be ready to own failures and mistakes
   - Practice saying "I don't know" when appropriate
   - Show learning agility and self-awareness

═══════════════════════════════════════════════════════

RESEARCH CONFIDENCE & GAPS

Confidence level: HIGH
- Substantial first-party content (Twitter, podcasts)
- Clear and consistent product philosophy
- Well-documented career background
- Strong signals on values and red flags

What we know well:
- His core product philosophies and frameworks
- What he values and criticizes in PMs
- His career arc and domain expertise
- His public voice and communication style

What we're inferring:
- Exact interview style (not conducting company interviews currently)
- Specific question patterns (based on philosophy, not direct observation)
- How he adapts for different seniority levels

What we don't know:
- Recent evolution in his thinking (content is last 2-3 years)
- How he adapts interview for specific roles vs general PM assessment
- His personal communication style 1-on-1 vs public persona

Sources consulted:
- Twitter/X: @shreyas (primary source)
- Lenny's Podcast episodes
- LinkedIn profile
- First Round Review interview
- Various PM community discussions
```

---

## Candidate Briefing (What Kamalika Would Receive)

**Conversational summary:**

"I've researched Shreyas Doshi. Here's what will help you prepare:

Shreyas is a highly respected product leader who spent 15+ years at Yahoo, Twitter, and Stripe before going independent as a product advisor. He's known for helping PMs at companies like Stripe scale their product thinking. He has a strong engineering background (CS + Wharton MBA) and deep expertise in payments, platforms, and developer tools.

His product philosophy centers on three things:

First, he emphasizes **strategic product thinking over execution mechanics**. He's famous for saying 'Your job is not to build things, your job is to create impact.' He created the LNO framework (Leverage/Neutral/Overhead work) and pushes PMs to focus on leverage work that compounds over time. He values clarity on the 'why' before the 'what.'

Second, he's a **strong critic of 'product theater'** — meetings, frameworks, and processes that create the illusion of progress without substance. He's skeptical of PMs who over-index on looking good versus being good. He values intellectual honesty and first-principles thinking over framework name-dropping.

Third, he has **high technical expectations** given his engineering background and Stripe experience. He understands payments infrastructure, APIs, platform architecture deeply — and he expects PMs working in technical domains to be credible with engineers.

From his public content, I can infer his interview style would be:
- Socratic and probing — he'll ask 'why?' repeatedly to test depth of thinking
- Direct but not aggressive — he values substance and will push on vague answers
- Focused on bets and trade-offs — he thinks probabilistically, not in certainties
- Testing for leverage thinking — he'll want to know how your work compounded

**Key areas to prepare:**

1. **Strategic clarity:** Be ready to articulate the 'why' behind your decisions, especially for AgentPay. Show first-principles thinking, not just regulatory checkbox-ticking.

2. **Leverage work examples:** Identify 2-3 projects from your past that had compounding impact. Be able to explain what made them high-leverage vs neutral or overhead work.

3. **Technical depth:** Given his Stripe background, brush up on payment systems architecture, APIs, state machines. Show engineering credibility.

4. **Product sense depth:** Prepare examples of user empathy, discovery work, and strategic product thinking. He'll probe beyond the polished CV narrative.

5. **Intellectual honesty:** Practice owning failures and saying 'I don't know' when appropriate. He values self-awareness over false confidence.

**What to avoid:**
- Surface-level metrics without understanding drivers
- Framework name-dropping without first principles
- Polished, rehearsed answers without real thinking
- Process-heavy talk without outcomes
- Anything that sounds like 'product theater'

I'll adapt my interview style to reflect his approach — expect Socratic questioning, strategic probing, and a focus on leverage thinking. Ready to start?"

**Source transparency:**
"My research is based on his extensive Twitter content (@shreyas), podcast appearances (Lenny's Podcast, First Round Review), and LinkedIn profile. He has a very clear and consistent public voice, so I'm confident in the persona adaptation."

**Ethical disclosure:**
"Note: This research uses only publicly available information. I'm synthesizing his professional background and public statements to help you prepare authentically — not to game the interview. The best preparation is understanding his perspective so you can have a genuine conversation about product work."

---

## Mock Interview Adaptation in Practice

**Sample opening question (adapted for Shreyas):**

"Let's start with AgentPay. Your CV says you're 'building India's first AI Agent Financial Identity platform.' Walk me through the bet you're making here — not the features, the underlying bet on agent behavior and trust. Why this problem, not another payments problem?"

**Sample follow-up (testing for leverage thinking):**

"You mentioned building the Mandate Engine. That sounds like infrastructure work. Help me understand — is that leverage work that compounds, or overhead work that enables other teams to do leverage work?"

**Sample technical probe (given his Stripe background):**

"You're designing PPI accounts for AI agents. Walk me through the technical architecture. How does an agent authenticate? How do you handle state? What's the transaction flow?"

**Sample strategic challenge (testing first principles):**

"You mentioned using graduated autonomy based on trust scores. Explain why graduated autonomy exists as a pattern — what problem is it solving? Could you solve the trust problem without it?"

---

## Success Indicators

This research and adaptation would be successful if:

✅ Kamalika understands Shreyas's emphasis on strategic thinking over execution  
✅ She's prepared for technical depth questions given his payments background  
✅ She's ready to articulate first principles, not just cite frameworks  
✅ She knows to expect Socratic questioning and probing on the "why"  
✅ The mock interview feels more realistic because it reflects his actual style  
✅ She feels more confident because she understands his perspective  

---

## What This Demonstrates

This example shows:
1. Systematic research protocol execution
2. Information extraction and synthesis
3. Persona adaptation logic
4. Candidate briefing that's actionable
5. Integration with main interview skill
6. Ethical boundaries maintained throughout

The sub-agent transforms generic interview prep into targeted preparation for a specific person's style and priorities.
