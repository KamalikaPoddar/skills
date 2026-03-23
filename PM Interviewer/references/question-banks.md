# Question Banks

Questions are organised by section. Always personalise using the candidate's CV before asking.
Each question has a [difficulty] tag: [S] = Standard, [H] = Hard, [B] = Brutal.

---

## Section 1 — CV deep-dive (always start here)

These are not generic. Generate these from the candidate's actual CV.

**Pattern for any claimed achievement:**
- "Walk me through exactly what you did — not the outcome, the work."
- "What did you personally build that someone else couldn't have?"
- "Who owned the technical decision vs the product decision here?"
- "What was the closest this came to failing?"
- "What would you do differently today?"

**Pattern for any claimed metric:**
- "How did you measure that?"
- "What was the baseline?"
- "Was this a controlled test or directional?"
- "What happened 6 months after you left?"

**Pattern for any people leadership claim:**
- "Walk me through your last performance review conversation with a struggling team member."
- "Tell me about a time your team disagreed with your product direction. What happened?"
- "Who on your team grew the most under you, and what did you specifically do?"

---

## Section 2 — Product skills questions

### Strategy and vision
[S] "You've just been made PM for a payments product that has plateaued at $5M ARR for two years.
First 30 days — what do you do, and what do you not do?"

[S] "How do you decide whether to build a feature that one large enterprise client is paying for
vs investing in platform capability that benefits all clients but has no direct revenue attached?"

[H] "You're a B2B SaaS PM. Your top 3 customers represent 60% of your ARR. All three want different
things this quarter. How do you build a roadmap that doesn't lose any of them?"

[H] "Walk me through how you'd evaluate whether your company should build, buy, or partner to add
AI-based fraud detection to your payments platform."

[B] "Your CEO comes to you and says: our biggest competitor just shipped feature X. We need it in
6 weeks. It would take your team 4 months. What do you do?"

[B] "Platform product vs features product — how do you know when your organisation has crossed
the threshold where platform thinking is mandatory rather than optional?"

### Prioritisation and roadmap
[S] "Walk me through how you'd prioritise a backlog of 50 items with 3 competing stakeholder groups
and a team of 8 engineers."

[S] "You have 3 high-value features, all with good data. You can only ship one this quarter.
How do you decide?"

[H] "How do you handle a situation where the data says ship Feature A, but your intuition says
Feature B is the right move? Walk me through a real example."

[H] "How do you build a roadmap when you're operating in a regulated environment where compliance
work is mandatory but produces no user-visible value?"

[B] "Your roadmap is entirely reactive — driven by client escalations and competitive pressure.
How do you transition to a proactive, strategy-led roadmap without losing the clients you have?"

### Metrics and measurement
[S] "You've just launched a new feature. What are the first three metrics you'd look at on day 1,
week 1, and month 1 — and why are they different?"

[S] "How do you set up an A/B test for a checkout flow change? Walk me through the full setup."

[H] "Your DAU/MAU ratio has been dropping for 3 months. You have full analytics access.
Walk me through your diagnosis process."

[H] "How do you measure the success of a platform product that has no direct user interaction —
only downstream effects on partner products?"

[B] "Your NPS has gone from 42 to 61 in 6 months. Your CEO is thrilled. Should they be?
What else would you need to know before concluding anything?"

### Execution and delivery
[S] "Walk me through how you run a sprint planning session for a team of 8 engineers across
two product workstreams."

[S] "Your sprint is 50% complete and a P1 bug has just dropped. What do you do?"

[H] "A senior engineer on your team keeps pushing back on your technical decisions in public
sprint meetings. How do you handle it?"

[H] "You are 3 weeks from a major client go-live and your QA team has found a critical issue
that will take 2 weeks to fix. How do you handle this?"

[B] "Two of your best engineers are leaving within the same month. You have a committed roadmap
and a client demo in 6 weeks. Walk me through your decision-making."

---

## Section 3 — Technical and analytical questions

### APIs and systems
[S] "Explain the difference between REST and event-driven architecture. When would you choose
one over the other for a payments platform?"

[S] "What does idempotency mean in a payments context? Why does it matter?"

[H] "You're designing an API for a multi-tenant card issuing platform. Walk me through the key
design decisions you'd make around authentication, versioning, and rate limiting."

[H] "How would you design a real-time fraud detection system that needs to make a decision in
under 200ms? What are the tradeoffs you'd make?"

[B] "Your platform processes 10M transactions per day. A client's transaction volumes suddenly
spike 10x. Walk me through how your system should behave and what breaks first."

### Data and analytics
[S] "You have a conversion funnel with 5 steps. Step 3 has a 60% drop-off. How do you diagnose it?"

[S] "Walk me through how you'd set up a cohort analysis for a fintech app to understand
30/60/90-day retention."

[H] "You have two features running in an A/B test. The results are statistically significant
but the effect size is tiny. Do you ship? Walk me through the decision."

[H] "How do you build an early warning system for a B2B SaaS product that predicts churn
90 days in advance?"

[B] "You have 3 months of data showing a correlation between feature X usage and 30-day
retention. Your CEO wants to invest heavily in feature X. What questions do you ask
before agreeing?"

### ML and AI product
[S] "Walk me through the product considerations for shipping an ML model to production.
What's different about shipping ML vs shipping a deterministic feature?"

[H] "How do you evaluate whether to build your own ML model vs use a third-party API
for a risk scoring use case?"

[H] "You're building an AI agent that can autonomously execute financial transactions.
How do you decide which actions it can take without human approval?"

[B] "Your AI feature is working well in testing but your users don't trust it in production.
They keep overriding its recommendations. How do you diagnose and address this?"

---

## Section 4 — Estimation and whiteboard exercises

### Estimation prompts (adapt for candidate's domain)

**Markets and sizing:**
[S] "How many UPI transactions happen in India in a single day?"
[S] "Size the market for business travel insurance in India."
[H] "How much revenue does India's ATM network generate annually?"
[H] "How many active fintech apps are on an average Indian smartphone?"
[B] "What's the total value of unclaimed financial assets in India — and how is it distributed
across asset classes?"

**Unit economics:**
[S] "You're building a co-branded credit card with an e-commerce partner. Walk me through
the unit economics from card issue to first transaction."
[H] "A neo-bank in India acquires a customer for ₹800. What does their LTV model need to
look like for this to be a good business?"
[B] "Your company charges 0.5% MDR on ₹50 lakh/month average merchant volume.
You have 500 merchants. What's your gross margin if infra costs you ₹8L/month
and you have 12 people in ops?"

**Whiteboard / product design:**
[S] "Design the notification system for a digital wallet. What events trigger notifications,
through which channels, and how do you prevent notification fatigue?"
[H] "You need to redesign the KYC onboarding flow for a fintech app targeting rural women
in India. Walk me through your approach."
[H] "Design a config-rules framework for a multi-tenant card issuing platform.
What entities do you model? What's the hierarchy?"
[B] "Design an AI agent that manages working capital for Indian MSMEs.
What are the first 3 actions you'd make autonomous, and what's your kill switch design?"

---

## Section 5 — Behavioural questions

### Leadership
[S] "Tell me about a time you had to influence without authority — no direct reporting line,
no budget lever. How did you get the outcome you needed?"

[S] "Walk me through how you gave difficult feedback to someone on your team.
What happened, and what would you do differently?"

[H] "Tell me about a product decision you made that turned out to be wrong.
How did you find out, and what did you do?"

[H] "You disagree strongly with your CEO's product direction. You've made your case
and been overruled. What do you do?"

[B] "You're 6 months into a new role. You've identified that the previous PM made
3 significant architectural decisions that are now creating real problems.
The CEO thinks those decisions were correct. What do you do?"

### Failure and resilience
[S] "Tell me about the hardest professional failure you've had. What happened?"

[H] "Walk me through a time you shipped something that you knew wasn't ready.
Why did you do it, and what happened?"

[B] "Tell me about a time your product caused real harm to users — financial loss,
a bad experience, a broken promise. What did you do?"

### Self-awareness
[S] "What's the type of PM work you consistently avoid or deprioritise? Why?"

[H] "What's a belief about product management you held 3 years ago that you no longer hold?"

[B] "If I asked your last engineering lead what it was like to work with you,
what's the most honest and least flattering thing they'd say?"

---

## Section 6 — Forward-looking / vision (always last)

"What's the one product you wish you'd built but didn't?"
"What's the most interesting unsolved problem in [candidate's domain] right now?"
"Where do you think AI agents will create the most disruption in financial services in the next 3 years?"
"If you joined this team, what's the first thing you'd want to learn that you don't know yet?"

---

## Question selection guidance

**For 30-min sessions:** 1 CV deep-dive + 2 domain questions + 1 estimation + 1 forward-looking

**For 60-min sessions:** 1 CV deep-dive + 4 domain questions + 1 estimation/whiteboard + 1 behavioural + 1 forward-looking

**For 90-min sessions:** 2 CV deep-dives + 5–6 domain questions + 2 estimations/whiteboards + 2 behavioural + 1 forward-looking

**Difficulty escalation rule:** Start one level below the configured difficulty on the first question of each domain.
Escalate by one level if the first answer is strong. Stay level if weak. This gives every candidate a chance to
show range — both the floor and the ceiling.
