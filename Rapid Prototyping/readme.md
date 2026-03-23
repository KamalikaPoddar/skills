# PM Rapid Prototype Builder

> **Turn your concept note or PRD into a working, on-brand, stakeholder-ready prototype
> in hours — not weeks.**

A multi-agent AI skill for product managers that orchestrates the full prototyping
workflow: from brief → brand extraction → tool selection → ready-to-paste prompts →
iteration → engineering handoff.

Built by [Kamalika Poddar](https://github.com/kamalikap) — 12 years building fintech
infrastructure across core banking, UPI, payment aggregators, account aggregators, and
cross-border payment rails.

---

## Why This Skill Exists

PMs are moving from writing docs to showing demos. But the tooling landscape is
fragmented, prompt quality is inconsistent, and most prototypes either look too generic
to be credible or break down at the engineering handoff.

This skill solves three specific gaps:

1. **Wrong fidelity / wrong tool** — PMs spend 4 hours in the wrong tool for their use case
2. **Generic-looking prototypes** — stakeholders see an AI template, not their product
3. **Dead-end demos** — prototypes that impress in the meeting but can't be handed off to engineers

---

## What It Does

The skill runs 7 sequential agents, each with a focused job:

| Agent | Job | Output |
|---|---|---|
| **1. Intent Clarifier** | Establishes what you're trying to learn and at what fidelity | Prototype Brief |
| **2. Brand Style Agent** | Extracts your company's real colors, fonts, and components | Style Pack |
| **3. Industry Context Agent** | Maps your domain to compliance and UX constraints | Constraint Pack |
| **4. Tool Selector** | Recommends the right tool with a reason | Recommendation |
| **5. Prompt Engineer** | Generates a ready-to-paste master prompt + iteration prompts | Master Prompt |
| **6. Prototype Reviewer** | Reviews your v0.1 and provides fix prompts | Review Report |
| **7. Handoff Generator** | Produces an engineering-ready artifact pack | Handoff Pack |

---

## File Structure

```
pm-rapid-prototype-builder/
├── SKILL.md                              # Main orchestrator — start here
├── README.md                             # This file
└── references/
    ├── brand-style-agent.md              # Agent 2: brand extraction (3 modes)
    ├── industry-context-agent.md         # Agent 3: compliance constraints (reusable)
    ├── tool-selector.md                  # Agent 4: tool decision logic
    └── tools/
        ├── v0.md                         # v0 (Vercel) prompting guide
        ├── lovable.md                    # Lovable prompting guide
        ├── bolt.md                       # Bolt.new prompting guide
        ├── cursor.md                     # Cursor prompting guide
        ├── claude-artifacts.md           # Claude Artifacts prompting guide
        └── claude-code.md               # Claude Code prompting guide
```

---

## Supported Tools

| Tool | Best for | Technical floor |
|---|---|---|
| **Claude Artifacts** | Instant concept demos, zero setup | None |
| **Lovable** | Full-stack apps with auth + design quality | Low |
| **Bolt.new** | Speed-first rapid iteration | Low-medium |
| **v0 (Vercel)** | High-fidelity React UI, dashboard components | Low |
| **Cursor** | Prototypes inside existing codebases | Medium |
| **Claude Code** | PM workflow automation + complex multi-file builds | Medium-high |

---

## Supported Industries

The Industry Context Agent (Agent 3) produces compliance-aware prompts for:

- 🏦 Financial Services (RBI, SEBI, NPCI, FCA, CFPB)
- 🌐 Cross-Border Payments & Remittance (FEMA, FinCEN, FATF)
- 🏥 Healthcare & MedTech (HIPAA, NHS, CDSCO)
- 🎓 EdTech (COPPA, FERPA, DPDP Act)
- 🛒 E-commerce & D2C
- 🚗 Mobility & Transport
- 🏗️ B2B SaaS & Enterprise
- 🔒 Cybersecurity & Identity
- 🌾 AgriTech & Rural
- 🌍 Generic (universal defaults for any domain)

---

## Brand Style Agent — Three Modes

The Brand Style Agent (Agent 2) adapts to whatever you have:

| Mode | You provide | Agent does |
|---|---|---|
| **Full** | Brand guide URL, Figma link, or PDF | Extracts exact colors, fonts, components |
| **Partial** | Company website URL or app screenshots | Infers the style via visual analysis |
| **Minimal** | Just the company name | Best-effort from public presence + industry defaults |

The output (Style Pack) is injected verbatim into the master prompt so your prototype
uses your actual brand colors, fonts, border radius, button styles, and nav patterns —
not shadcn defaults.

---

## How to Use

### Option A — Install as a Claude skill

1. Download `pm-rapid-prototype-builder.skill`
2. In Claude.ai → Settings → Skills → Install from file
3. Any PM session that involves prototyping will automatically invoke this skill

### Option B — Use the files directly

Copy any reference file into your Claude conversation and reference it explicitly:

```
Read this file and follow its instructions to help me build a prototype:
[paste contents of SKILL.md]
```

### Option C — Add to your GitHub skills repo

```bash
git clone https://github.com/your-username/pm-skills
cp -r pm-rapid-prototype-builder pm-skills/
cd pm-skills && git add . && git commit -m "feat: pm-rapid-prototype-builder"
git push
```

---

## Example Session

```
PM:   "I have a stakeholder meeting in 3 hours. I built a concept note for
       a cross-border remittance product for Indian migrant workers in the GCC.
       I need something to show. Help."

Skill: [Runs Intent Clarifier] → scopes to: sender initiates transfer flow
       [Runs Brand Style Agent Mode 3] → infers company style from name
       [Runs Industry Context Agent] → Cross-Border Payments constraint pack
         (FX rate disclosure, transfer limit, KYC status, purpose of transfer)
       [Tool Selector] → recommends Lovable (full-stack, auth, design quality)
       [Prompt Engineer] → generates master prompt with:
         - Brand colors + fonts
         - KYC status indicator
         - FX rate with 30-second expiry timer
         - Full cost breakdown (send / fees / recipient receives)
         - OTP gate before confirmation
         - Transfer under review state
         - Iteration prompt: "add recipient confirmation screen"

PM:   [Pastes prompt into Lovable, gets prototype in ~20 minutes]

PM:   "Here's a screenshot — what's missing?"

Skill: [Prototype Reviewer] → flags missing: empty state on transaction history,
        error state for bank decline, session timeout indicator
        → provides 3 paste-ready fix prompts

PM:   [Meeting goes well. Stakeholders approve budget.]

PM:   "Help me hand this off to engineering."

Skill: [Handoff Generator] → produces full pack with component inventory,
        data contract, user stories, compliance gaps, open engineering questions
```

---

## Reusable Subagents

Two agents in this skill are designed for reuse across the broader PM skill suite:

**`industry-context-agent.md`** — can be imported by:
- PRD Writer (compliance constraints in requirements)
- Regulatory Radar (regulatory translation)
- Stakeholder Briefing Generator (compliance context)

**`brand-style-agent.md`** — can be imported by:
- PRD Writer (on-brand screenshots and mockup references)
- Competitive Intelligence (competitor brand analysis)
- Stakeholder Briefing (on-brand documents)

---

## Roadmap

- [ ] Figma MCP integration for direct design token extraction (Agent 2)
- [ ] Confluence / Notion MCP for auto-pulling existing PRDs (Agent 1)
- [ ] Automated prototype screenshot review via vision model (Agent 6)
- [ ] Jira ticket generation from Handoff Pack (Agent 7)
- [ ] Additional industries: InsurTech, GovTech, LegalTech

---

## Contributing

This skill is part of the open PM Skills suite. To contribute:

1. Fork the repo
2. Add or improve a reference file
3. Test with a real prototyping session
4. Submit a PR with: what you changed, why, and an example output

---

## Author

**Kamalika Poddar**
Product leader with 12 years in fintech infrastructure — core banking, UPI, payment
aggregators, account aggregators, wealth tech, and cross-border payment rails.
Building AI tools to help PMs move faster and ship more confidently.

[GitHub](https://github.com/kamalikap) · [LinkedIn](https://linkedin.com/in/kamalikap)

---

## License

MIT — free to use, fork, and build on. Attribution appreciated.
