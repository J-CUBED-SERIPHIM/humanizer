# Corva Lending — Cora Agent System

The complete agent system specification for **Cora**, the AI sales and service agent for **Corva Lending** (corvalending.com, formerly Ameritrust Mortgage).

Built by **J Cubed Marketing & Automation**. Modeled on the ULC **Reese** agent system — same 6-capability architecture and "top 20% salesperson" behavioral core, re-engineered for non-QM mortgage lending and its compliance surface.

## What's Here

| File | Purpose |
|---|---|
| `Corva-Agent-System.md` | The full agent spec — 10 sections + appendices, 6-capability architecture, mortgage-advertising guardrails, all loan programs, example conversations |
| `Corva-Agent-Context-Pack.md` | Fast-load rules reference (guardrails-first) for a quick presale/pilot deployment before the full spec is wired up |

## Architecture at a Glance

Cora is a **single consumer-facing agent** backed by **6 capability areas** (the same pattern as Reese — implemented as prompt sections, tool calls, or a retrieval layer, not six separate bots the borrower ever sees):

1. **Cora (Orchestrator)** — The primary conversational agent. Handles every borrower interaction, runs discovery, enforces the silence-after-close protocol, and drives to one outcome: a booked call with a licensed loan officer (or a started secure application).
2. **Compliance Monitor** — The mortgage-advertising gate. Runs on every outbound message. Blocks rate/APR/payment quotes, "you're approved" language, guarantees, Fair-Lending violations, and missing NMLS/Equal-Housing disclosures. This is the safety net that lets Cora talk about programs freely.
3. **Borrower Profiler** — Infers the borrower persona (Self-Employed Owner, Real Estate Investor, Global Buyer, Prime Mover, Equity Optimizer) from natural language and tailors the conversation. Never interrogates.
4. **Knowledge Agent** — Retrieves loan-program details (non-QM + agency/QM), general eligibility signals, and positioning, formatted for the detected persona.
5. **Objection Coach** — Handles objections with the 4-step method (Listen → Empathize → Isolate → Solution) and the lending objection library.
6. **Pipeline Agent** — Manages lead status, the mortgage funnel, follow-up cadence, and CRM integration.
7. **Booking Agent** — Handles loan-officer appointment scheduling, availability, secure-application handoff, and reminders.

## What Cora Is NOT

Cora markets, educates on program types in general terms, qualifies interest, and books a licensed loan officer. Cora is **not** a loan officer. She never quotes a rate, APR, payment, points, or fees; never issues a pre-approval or says "you qualify"; never commits to lend; never collects SSN/DOB/account numbers over chat. Anything requiring real numbers or a decision routes to a licensed LO (NMLS). See §2.

## Deployment

The spec is a **platform-agnostic prompt architecture**. It runs on any LLM platform that supports structured system prompts, tool/function calling for the capability areas, and variable interpolation for branch/loan-officer data (marked with `[VARIABLES]` throughout).

### Variables
All branch-, officer-, and license-specific data (NMLS IDs, licensed states, LO name, booking link, secure application URL, disclosures) is parameterized. Search for `[` in the spec to find every variable to set before going live.

## Compliance Note

This agent operates in a federally and state-regulated space. Before live deployment, a licensed compliance reviewer must sign off on §2 (Guardrails + Compliance Monitor), Appendix A (disclosures/variables), and every example message. Regulations referenced: TILA/Reg Z (and trigger terms), MAP Rule/Reg N, ECOA/Reg B + Fair Housing, RESPA, UDAAP, TCPA, GLBA/data security, and CA/TX state licensing.

## Note
PDF renders are excluded from version control (see `.gitignore`).
