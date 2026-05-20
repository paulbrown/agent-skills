---
name: grill-with-docs
description: Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, ADRs) inline as decisions crystallise. Use when you want to stress-test a plan against the project's language and documented decisions.
---

# Grill With Docs

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.

For each question, provide your recommended answer.

## Codebase Exploration
Before we begin, silently explore the repository to understand the existing documentation:
- **File structure:** Most repos have a single context (`CONTEXT.md` and `docs/adr/` at the root).
- If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. Find the relevant `CONTEXT.md` for this feature.
- **Lazy Creation:** Create files lazily. If no `CONTEXT.md` exists, create one when the first term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed.

## The Interview Protocol (The Loop)
1. **Thematic Pacing:** Group your interrogation. Focus first on the Data Model/State, then Failure Modes & Edge Cases, then UI/UX. Ask highly targeted questions. Wait for my response before moving on.
2. **Confidence Scoring:** Maintain an internal 'Architecture Confidence Score' from 0% to 100%. After every user response, silently recalculate your score. You are aiming for **95%+ confidence** that your mental model matches the codebase and the plan is airtight. 
3. **Exit Condition:** Once you hit 95% confidence, announce it, summarize the final plan, and end the grilling.

## During the Session You Must:
* **Challenge against the glossary:** When I use a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. ("Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?")
* **Sharpen fuzzy language:** When I use vague or overloaded terms, propose a precise canonical term. ("You said 'account' — do you mean Customer or User?")
* **Discuss concrete scenarios:** Invent scenarios that probe edge cases and force me to be precise about boundaries.
* **Cross-reference with code:** Check whether the code agrees with how I say something works. Surface any contradictions immediately.

## Managing Documentation (Anti-Context Rot)
Use the format defined in `assets/CONTEXT-FORMAT.md` when updating `CONTEXT.md`. Use the format defined in `assets/ADR-FORMAT.md` when creating an ADR.
* **Update CONTEXT.md inline:** When a term is resolved, update `CONTEXT.md` right there. Capture them as they happen. `CONTEXT.md` should be totally devoid of implementation details; it is a glossary and nothing else.
* **Offer ADRs sparingly:** **ONLY** write an Architecture Decision Record (ADR) to `docs/adr/` if the decision meets ALL THREE criteria:
    1. *Hard to reverse* (the cost of changing your mind later is meaningful).
    2. *Surprising without context* (a future reader will wonder "why did they do it this way?").
    3. *The result of a real trade-off* (there were genuine alternatives and you picked one for specific reasons). 
    
    *Do not document trivial decisions or minor state changes.*