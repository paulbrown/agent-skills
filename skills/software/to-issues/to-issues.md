---
name: to-issues
description: Break a plan, spec, or PRD into independently-grabbable issues on the project issue tracker using tracer-bullet vertical slices.
---

# To Issues

Break a plan into independently-grabbable issues using vertical slices (tracer bullets). The issue tracker and triage label vocabulary should have been provided to you. If you don't know them, read `docs/agents/issue-tracker.md` and `docs/agents/triage-labels.md`.

## Process

1. **Gather context.** Work from whatever is already in the conversation context. If the user passes an issue reference (issue number, URL, or path) as an argument, fetch it from the issue tracker and read its full body and comments.
2. **Explore the codebase.** If you have not already explored the codebase, do so to understand the current state of the code. Issue titles and descriptions must use the project's domain glossary vocabulary (`docs/agents/domain.md`).
3. **Draft vertical slices.** Break the plan into tracer bullet issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer. Slices may be 'HITL' (Human in the Loop) or 'AFK' (Away from Keyboard).
    * Prefer AFK over HITL where possible.
    * Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests).
    * A completed slice is demoable or verifiable on its own.
    * Prefer many thin slices over few thick ones.
4. **Quiz the user.** Present the proposed breakdown as a numbered list. For each slice, show:
    * **Title:** short descriptive name.
    * **Type:** HITL / AFK.
    * **Blocked by:** which other slices (if any) must complete first.
    * **Ask the user:** Does the granularity feel right? Are the correct slices marked as HITL and AFK? Iterate until the user approves the breakdown.
5. **Publish the issues.** For each approved slice, publish a new issue to the issue tracker. Use the `<issue-template>` below. Publish issues in dependency order (blockers first) so you can reference real issue identifiers in the "Blocked by" field. Apply the `ready-for-agent` triage label (or your repo's equivalent) to AFK issues.

<issue-template>
## Parent & Shared Context
- **Parent Epic:** A reference to the parent PRD/Epic (if any).
- **Domain Rules:** Before starting work, review `docs/agents/domain.md` to ensure you use the correct terminology.

## What to build
A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation. Avoid specific file paths or code snippets unless they are explicitly finalized schemas/state machines from a prototype.

## Strict Boundaries (What NOT to build)
Explicitly list adjacent features or modules that are explicitly out of scope for this specific ticket. Do not implement features meant for subsequent tickets.

## Acceptance criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Validation: Code must pass tests and formatting as defined in `docs/agents/ci-commands.md`.

## Blocked by
A reference to the blocking ticket (if any) or "None - can start immediately."
</issue-template>

**Crucial Guardrail:** Do NOT close or modify any parent issue or PRD during this process.