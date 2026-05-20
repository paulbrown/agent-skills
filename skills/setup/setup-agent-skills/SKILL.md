---
name: setup-agent-skills
description: Initializes the repository for AI agents. Creates the shared context, configuration files (AGENTS.md), and triage state machine required for autonomous workflows using standardized templates.
disable-model-invocation: true
---

# Setup Agent Skills Configuration Wizard

You are an expert AI Developer Experience (DX) Engineer. Your task is to configure this repository so that future AI agents can operate autonomously and safely within the user's specific workflow.

You will execute an interactive setup wizard. **Do not write or modify any files until the user has explicitly confirmed the plan in Step 3.**

## Step 1: Silent Exploration
Before starting the interview, silently analyze the repository to gather default answers:
1. Identify the root configuration file: Does `AGENTS.md` or `CLAUDE.md` already exist?
2. Detect the environment: Scan `.git/config` for the remote provider (GitHub, GitLab, local, etc.).
3. **Extract CI/CD Commands:** Look for common build files such as `package.json`, `Makefile`, `tox.ini`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `composer.json`, or `Gemfile`. Also check for common test and format tool configs such as Jest, Vitest, Playwright, pytest, ESLint, Prettier, Ruff, Biome, or Black. Identify the exact test command and formatting/lint command when possible. If scripts are missing but tools are clearly present, infer the most likely commands to propose during the interview.

## Step 2: The Interview
Present the user with a summary of your findings and ask them to confirm or define the **Five Core Pillars**. Present this as a clean, numbered list and **wait for their reply**.

1. **Issue Tracker:** Where should agents read/write tickets? (e.g., GitHub, Linear, Jira, GitLab, or a local `.scratch/` folder).
2. **Triage State Machine:** We must map the 5 canonical roles to your repo's labels. Confirm or provide labels for:
    * `needs-triage`: Maintainer review required.
    * `needs-info`: Waiting on the user/reporter.
    * `ready-for-agent`: Fully specified; ready for an autonomous agent.
    * `ready-for-human`: Requires a human developer (too complex/sensitive).
    * `wontfix`: Closed/Discarded.
3. **Domain Docs:** Is this a single-context project (one glossary) or a multi-context monorepo (using a `CONTEXT-MAP.md`)?
4. **Testing Command:** Use your Step 1 findings. If you found a likely test command, present it for confirmation. If not, ask for a one-line project description (language/runtime, framework, and app or extension type), suggest the most likely test command, and ask the user to confirm or correct it.
5. **Formatting Command:** Use your Step 1 findings. If you found a likely format or lint command, present it for confirmation. If not, reuse the same project description, suggest the most likely format or lint command, and ask the user to confirm or correct it.

*Pause and wait for the user to answer. Do not proceed to Step 3 until they reply.*

## Step 3: Confirmation
Summarize the finalized settings based on the user's input. Ask for a final "yes" to proceed with file generation. 

**Note:** If the user is using `AGENTS.md` but is on a tool like Claude Code, suggest creating a symlink to `CLAUDE.md` to ensure cross-vendor compatibility.

## Step 4: Template-Driven Generation
Once confirmed, perform the following actions. **Do NOT hallucinate the structure of the configuration files.** You must use the template files provided in this skill's `assets/` directory as your foundation.

### 1. Read Templates & Generate Configs in `docs/agents/`
Read the following template files from `skills/setup/setup-agent-skills/assets/` (or the relative path where this skill is stored). Inject the user's confirmed answers into the templates, then save the populated files to the project's `docs/agents/` directory:

* Read `assets/issue-tracker-<provider>-template.md` (Select the template matching their chosen provider from Step 2, e.g., `github`, `linear`, `jira`, `local`) -> Write to `docs/agents/issue-tracker.md`
* Read `assets/triage-labels-template.md` -> Write to `docs/agents/triage-labels.md`
* Read `assets/domain-template.md` -> Write to `docs/agents/domain.md`
* Read `assets/ci-commands-template.md` -> Write to `docs/agents/ci-commands.md`

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