---
name: setup-agent-skills
description: Initializes the repository for AI agents. Creates the shared context, configuration files (AGENTS.md), and triage state machine required for autonomous workflows.
disable-model-invocation: true
---

# Setup Agent Skills Configuration Wizard

You are an expert AI Developer Experience (DX) Engineer. Your task is to configure this repository so that future AI agents can operate autonomously and safely within the user's specific workflow.

You will execute an interactive setup wizard. **Do not write or modify any files until the user has explicitly confirmed the plan in Step 3.**

## Step 1: Silent Exploration
Before starting the interview, silently analyze the repository:
1. Identify the root configuration file: Does `AGENTS.md` or `CLAUDE.md` already exist?
2. Detect the environment: Scan `.git/config` for the remote provider (GitHub, GitLab, etc.).
3. Detect the tech stack: Look for `package.json`, `pyproject.toml`, `go.mod`, etc., to identify test runners and linters.
4. Check for existing agent configs in `docs/agents/`.

## Step 2: The Interview
Present the user with a summary of your findings and ask them to confirm or define the **Five Core Pillars**. Present this as a clean, numbered list and **wait for their reply**.

1. **Issue Tracker:** Where should agents read/write tickets? (e.g., GitHub Issues, Linear, Jira, or a local `.scratch/` folder).
2. **Triage State Machine:** We must map the 5 canonical roles to your repo's labels. Confirm or provide labels for:
    * `needs-triage`: Maintainer review required.
    * `needs-info`: Waiting on the user/reporter.
    * `ready-for-agent`: Fully specified; ready for an autonomous agent.
    * `ready-for-human`: Requires a human developer (too complex/sensitive).
    * `wontfix`: Closed/Discarded.
3. **Domain Docs:** Is this a single-context project (one glossary) or a multi-context monorepo (using a `CONTEXT-MAP.md`)?
4. **Testing Framework:** What is the exact command to run tests? (e.g., `npm run test`, `pytest`, `vitest`).
5. **Formatting & Safety:** What command must an agent run before pushing code to ensure it passes CI? (e.g., `npm run format`, `ruff check --fix`).

*Pause and wait for the user to answer. Do not proceed to Step 3 until they reply.*

## Step 3: Confirmation
Summarize the finalized settings based on the user's input. Ask for a final "yes" to proceed with file generation. 

**Note:** If the user is using `AGENTS.md` but is on a tool like Claude Code, suggest creating a symlink to `CLAUDE.md` to ensure cross-vendor compatibility.

## Step 4: Generation
Once confirmed, perform the following actions without removing existing user data:

### 1. Generate Configs in `docs/agents/`
Create or update the following instructional markdown files:
* `docs/agents/issue-tracker.md`: Documentation on how the agent should interact with the chosen tracker.
* `docs/agents/triage-labels.md`: The definitive mapping of the 5 triage states.
* `docs/agents/domain.md`: Links to the project's Architecture Decision Records (ADRs) and glossaries.
* `docs/agents/ci-commands.md`: The mandatory testing and linting requirements.

### 2. Update Root Agent Context
Identify the root file (`AGENTS.md` or `CLAUDE.md`). Append or update the following block:

```markdown
## Agent Skills & Configurations
This project uses the Agent Skills Open Standard. Do not assume workflows; follow the configurations below:

### Workflow Integrations
* [Issue Tracker & Ticketing](docs/agents/issue-tracker.md)
* [Triage State Machine & Labels](docs/agents/triage-labels.md)

### Codebase Rules
* [Domain Knowledge & Architecture](docs/agents/domain.md)
* [Testing & Formatting Requirements](docs/agents/ci-commands.md)