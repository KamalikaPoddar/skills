# From Practitioner to System: 12 Years in Indian Fintech, 1.5 Years of Building AI into How I Do Product
 
**Kamalika Poddar** · Product Owner, Global Payments Platform, M2P Fintech
 
*M2P Fintech · PayU · CAMS · LXME · Axis Bank · Temenos*  
*Payments · Lending · WealthTech · Account Aggregation · Regulated Indian Fintech*
 
---
 
> I've spent 12 years building regulated fintech products in India — across payments, lending, personal finance and open finance. For the last 1.5 years, I've been systematically rebuilding how I do PM work using AI. Not as a productivity shortcut. As an operating system. This document is that infrastructure. What it is, how it works in practice, and where I am trying to pivot my product craft to next.
 
---
 
## The Problem I Was Actually Trying to Solve
 
India's regulated fintech stack is operationally expensive for a PM. Especially new to fintech PM. Every product decision sits at the intersection of RBI master circulars, NPCI frameworks, GST council rules, and now DPDP obligations — simultaneously. And often a lot of time is lost in just going back and forth, either with fellow PMs during brainstorming sessions, on what to build and how to build. Only to have compliance later squash the entire effort we put in to build it. 
 
Regulatory conflicts surface at prototype review or legal sign-off, not at ideation or produc thypothesis stage. By then, a feature has been estimated and committed to a sprint, and significant dev bandwidth wasted. Legal and compliance back-and-forth consumes days for questions that, with the right source material,  takes hours.  Post-build ticket/PRD audits rarely happen with enough rigour to catch drift before the next sprint.
 
I built AI into each of these gaps — not as a collection of tools, but as a layered system where each piece solves one of these problems specifically.
 
---
 
## The Stack
 
**Layer 1 — The Regulatory RAG**
 
A NotebookLM RAG instance, continuously fed with live RBI master circulars relevant to the products I build: Prepaid Payment Instruments, Payment Aggregators, Debit Cards, Forex Cards. SEBI circulars for wealth management work. GST council computation guidelines. Updated each time a circular is revised or a new one is issued.
 
Before any PRD is written, a product hypothesis is interrogated against this RAG. The output is either a clear flag with the relevant circular provision cited, or a clean pass. What used to require a discovery meeting with legal now begins as a targeted, evidence-backed question. The RAG doesn't replace legal review — it compresses the back-and-forth from weeks to a focused, specific conversation. It helps me to propose 3-4 user flows, have the system play devil's advocate before arrivign at a user journey that makes sense while being compliant. Sharing these insights with the Legal/compliance teams also often helps fast-track approvals. 
 
**Layer 2 — The Agent Skills System**
 
A set of domain-specific agent protocols — each one encoding a type of PM judgment — designed to work across Claude, ChatGPT, and Gemini. Not generic frameworks. These carry my 12 years of regulated fintech context: the regulatory history, the platform architecture decisions, the product bets already in flight, experience in building trust in the users' mind by ensuring user interactions take those triggers into scope. Every session starts from that context rather than from zero. And this has beena  game changer for new APMs to hit the ground running faster. 
 
**Layer 3 — The BMAD Technical PRD Pipeline**
 
BMAD (a multi-agent development framework) takes my functional PRD first draft and generates a structured technical PRD — data models, computation sequences, edge cases, test cases — hosted on GitHub. The solution architect uses this as the design input. Engineers build from the architect's output. Two documents, two audiences, zero loss of product intent in translation. This sits above the functional PRD on Confluence; the technical PRD on GitHub is the bridge between product thinking and engineering execution.
 
---
 
## The Forex Card GST Case: All Three Layers Working Together
 
*This case study is also how I became the organisational reference point for GST computation at M2P.*
 
### The gap
 
Our compliance auditor agent flagged forex card conversion GST as a high-risk compliance issue. The platform had been expecting the upstream system to compute and provide the GST values — which was an incorrect or rather incomplete implementation. GST on forex card loading is not optional or configurable: it is a mandatory deduction under Indian tax law, with specific rules governing how the total liability is split between CGST, SGST, and IGST depending on the location of the issuer and the nature of the transaction.
 
No one in the organisation had a clear, definitive answer on the computation logic.
 
### What happened instead of three weeks of legal back-and-forth
 
**Step 1 — RAG expansion.**  
I downloaded the relevant master circulars covering forex prepaid card issuance and the GST council's guidelines for foreign exchange transaction computation. Vectorised both and added to the existing RAG instance alongside the PPI and PA circulars already loaded.
 
**Step 2 — Regulatory interrogation.**  
Queried the expanded RAG for the exact computation logic — the sequence for arriving at the conversion GST value, the conditions that trigger each split (CGST/SGST vs IGST), the applicable rates, the rounding rules, and any issuer-specific carve-outs. The RAG surfaced the relevant provisions with citations, replacing what would have been a multi-week legal engagement with a same-day scoping session.
 
**Step 3 — Functional PRD first draft.**  
Used the RAG output as the primary source to write the functional specification: what the platform needed to compute, in what order, under what conditions, with what output structure. This also helped me with writing the detailed test cases which in this case where extremely computationally heavy and involved a plethora of test cases to cover. 
 
**Step 4 — Technical PRD via BMAD.**  
Handed the functional first draft to BMAD agents. The agents produced a structured technical PRD covering the data model for GST fields, the computation sequence, edge case handling, and test conditions for each split scenario. This was committed to GitHub and handed to the solution architect as the design input. Engineering built from the architect's output.
 
### The outcome
 
The compliance gap was closed before it became a regulatory filing issue. The computation logic is now embedded in the platform, no longer dependent on an upstream expectation that was never going to be met. The organisation now has documented, auditable logic for forex GST computation — logic that can be tested, version-controlled, and referenced when the next circular revision comes.
 
> What would have taken three to four weeks of legal and compliance consultation — discovery meetings, clarification rounds, back-and-forth on interpretation — took days. The RAG gave me faster, deeper access to the primary source material than any human consultation process would have, and the BMAD pipeline converted that into engineering-ready specifications without losing product intent.
 
The GST expertise I built through this process now means I am the internal reference point for these questions. That is not a credential I had before. It is a capability the AI workflow produced.
 
---
 
## The Skills That Run Alongside the RAG
 
The RAG handles regulatory context. The skills handle everything else in the PM workflow.
 
| Skill | What it encodes | Where it runs |
|---|---|---|
| **Problem Structuring** | Issue tree decomposition, JTBD mapping, hypothesis validation — before any solution is entertained | Every sprint, at ideation |
| **Sprint / Quarter Audit** | Forensic review of ticket quality, AC coverage, estimate accuracy, spillover patterns — a data investigation, not a feelings retrospective | End of every sprint |
| **Competitor Intelligence** | Five-subagent system: industry context → user psychology → signal collection → pattern detection → action recommendation | Weekly brief |
| **Rapid Prototyping** | Turns a concept note or PRD into a stakeholder-ready working prototype — replacing "let's mock it before the steering" with a working demo | Pre-stakeholder sessions |
| **Tech Writer** | Converts sprint board output into release notes, user guides, and API docs — closing the documentation gap every PM team has but nobody owns | Post-sprint |
| **AI Native PM Coach** | Structured coaching protocol with session continuity, carrying forward open questions and assigned actions across conversations | Ongoing |
 
**What makes these different from the generic PM skills repos on GitHub:**
 
Those repos encode methodology — Mom Test, Shape Up, Teresa Torres. They are reusable because they are generic. Anyone can clone the same repo and get the same output.
 
These skills encode *my* context. The regulatory history. The platform architecture decisions. The product bets already in flight at M2P, PayU, CAMS. Nobody else's instance of these skills produces the same output, because the reference files behind them carry 12 years of RBI and SEBI-governed, India-specific fintech judgment. The skill is the protocol. The reference files are the knowledge graph. Together, they are not a productivity tool — they are a domain-aware operating system.
 
The full library — SKILL.md files, reference architecture, cross-platform installation instructions for Claude, ChatGPT, and Gemini — is publicly available and open:
 
🔗 **[github.com/KamalikaPoddar/skills](https://github.com/KamalikaPoddar/skills)**
 
---
 
## What I've Built for the PM Community
 
Two skills in this library were built not for my own workflow, but as infrastructure for the broader PM community — specifically for the next generation of product managers developing their craft.
 
**The PM Interviewer**
 
A mock interview agent with the persona of a practitioner who has been building digital products since the 1990s and AI products since 2018. The agent runs deep diagnostic mock interviews — not surface-level behavioural prompts, but challenges that probe how a candidate thinks under pressure, how they handle incomplete information, and how they distinguish between a genuine product insight and a well-packaged assumption. Built for PMs preparing for roles at growth-stage and large tech companies, and tested across multiple real interview preparation sessions before being published.
 
**The Career Strategist**
 
A personalised career advisor built on a verified database of real PM experience — not generic advice, but JD-matched gap analysis, CV rewrites, and cover letters grounded in actual, traceable proof points. Every claim the agent makes traces to a verified STAR node; it cannot hallucinate your experience because the knowledge base is built from what actually happened. Built to solve the specific problem that most career coaching tools give you the generic version when the situation requires the specific one.
 
Both are open, documented, and available in the skills repo. Both follow the same principle as the work skills: structure and domain knowledge do more than a better prompt.
 
---
 
## What I'm Building Next: AgentPay
 
*A side project. And a question I think India's financial infrastructure hasn't answered yet.*
 
### The problem
 
India's regulated financial stack was designed for human principals — account holders, cardholders, borrowers. The RBI frameworks, the NPCI rails, the DPDP obligations: all of them assume a human is the accountable party at the end of every transaction.
 
AI agents are starting to transact. Not as a future scenario — as a current reality in global markets. An AI agent that books travel, pays a vendor, or settles a recurring invoice needs to move real money through real infrastructure. When that happens in India, the question that must be answered before the transaction — not after — is: who is the accountable party? What is the mandate? What are the limits? What happens when it goes wrong?
 
AgentPay is the bet that the answer to this question must be built before the agents arrive in volume.
 
### The product philosophy
 
Three decisions that define the whole architecture:
 
**Graduated Autonomy**  
An agent earns the right to transact at higher autonomy levels based on its behavioural track record — not because the developer declared it safe. Trust is not asserted. It is demonstrated through compliance with mandate constraints over time. An agent operating for the first time is constrained; an agent with a clean history across thousands of transactions can operate with greater latitude. The mechanism mirrors how human trust is actually built.
 
**Three-Way Match**  
Human mandate + agent intent model + merchant's signed quote must all align before a payment executes. This is not a fraud check. It is the mechanism that makes every transaction auditable and legally attributable — the evidence that the agent acted within declared scope, that the merchant knew what they were receiving, and that the human's original intent was honoured end-to-end.
 
**The Simulation Gate**  
No agent operates on live payment rails without first passing a controlled simulation environment that tests its behaviour against edge cases, failure scenarios, and adversarial inputs. Failure modes are found before they touch real money. This is the product equivalent of a clinical trial: the gate is not bureaucracy, it is the evidence base that makes deployment defensible.
 
### Why this matters to everyone in this room
 
Every payments company in India is going to face a version of this question. When AI agents start transacting through payment infrastructure — through UPI, through prepaid instruments, through payment gateways — the infrastructure will need to know how to verify an agent, honour a mandate, and attribute liability. The question is not whether this problem arrives. It is whether the trust layer is built before or after the first regulatory incident.
 
AgentPay is the bet that before is the right answer.
 
🔗 **[github.com/KamalikaPoddar/skills](https://github.com/KamalikaPoddar/skills)**
 
---
 
*Kamalika Poddar · April 2026*  
*Product Owner, Global Payments Platform, M2P Fintech*  
*4× LinkedIn Top Voice · 75,000+ newsletter subscribers · Global Top 12 Fintech Influencer (DataRail) · Bharat Fintech Summit Upcoming Leader 2024*
