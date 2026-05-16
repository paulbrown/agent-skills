---
name: to-prd
description: Turn the current conversation context into a PRD and publish it to the configured project issue tracker. Use when you want to synthesize an agreed-upon plan into a formal specification.
---

# To PRD

This skill takes the current conversation context and codebase understanding and produces a Product Requirements Document (PRD). 

**Do NOT interview the user** — just synthesize what you already know.

## Process
1. **Read Context:** Explore the repo to understand the current state of the codebase. Use the project's domain glossary (`docs/agents/domain.md`) vocabulary throughout the PRD. Respect any ADRs in the area you are touching.
2. **Module Sketching:** Sketch out the major modules you will need to build or modify. Actively look for opportunities to extract deep modules (encapsulating functionality in a simple, testable interface). 
3. **Verify:** Check with the user that these modules match their expectations and ask which modules they want tests written for. Wait for confirmation.
4. **Generate:** Write the PRD using the `<prd-template>` below.
5. **Publish:** Read `docs/agents/issue-tracker.md` to determine WHERE to publish this PRD (e.g., GitHub, Linear, or a local `.scratch/` folder).
6. **Labeling Guardrail:** You MUST label this generated document strictly as a `prd`. Do NOT apply any action-oriented triage labels (such as `ready-for-agent`). The PRD is an Epic/Planning document. Tagging it with `prd` serves as a fence that tells autonomous background coding agents to ignore it, preventing them from trying to implement the entire feature set in a single massive, error-prone loop.

<prd-template>
- **Problem Statement:** The problem from the user's perspective.
- **Solution:** The solution from the user's perspective.
- **User Stories:** A LONG, numbered list of user stories (As an <actor>, I want a <feature>, so that <benefit>).
- **Implementation Decisions:** The modules built/modified, interfaces, schema changes, and API contracts. *Do NOT include specific file paths or code snippets* (except for state machines or schemas from prototypes).
- **Strict Boundaries (Anti-Overlap):** Explicitly define the boundaries of each module. State clearly what each slice or module SHOULD NOT handle. This prevents downstream agents from hallucinating overlapping scope when implementing isolated issues.
- **Testing Decisions:** What makes a good test, which modules will be tested, and prior art for the tests.
- **Out of Scope:** Things explicitly not covered in this PRD.
- **Further Notes:** Any additional technical considerations.
</prd-template>