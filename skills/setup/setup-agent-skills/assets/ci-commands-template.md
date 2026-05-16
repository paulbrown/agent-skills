# CI/CD & Code Quality Enforcement Rules

This document outlines the strict quality gates that any AI agent must satisfy before declaring a task complete, opening a Pull Request, or pushing code to this repository. Do not skip these steps.

## 1. Mandatory Test Execution
Before proposing code modifications or asserting that a bug is fixed, you must execute the project's test suite to verify your changes.

* **Primary Test Runner Command:** `{{TEST_COMMAND}}`
* **Coverage/Isolation Requirements:** `{{TEST_FLAGS_OR_CONSTRAINTS}}`

### The TDD Workflow Requirement
If you are running a Test-Driven Development loop (such as the `/tdd` skill), you must adhere to the following sequence:
1. Write or locate a failing test that perfectly reproduces the target bug or specifies the new feature.
2. Run `{{TEST_COMMAND}}` to verify it fails (**Red**).
3. Write the minimal code required to fix the failure.
4. Run `{{TEST_COMMAND}}` again to verify it passes (**Green**).
5. Refactor the code for quality, ensuring the tests remain passing.

## 2. Formatting, Linting, & Safety Check
To keep the codebase uniform and avoid breaking the CI pipeline, you must run linting and code formatting tools over any file you touch. **Do not commit unformatted code.**

* **Formatting & Linting Command:** `{{FORMAT_COMMAND}}`
* **Static Analysis/Type Checking:** `{{TYPE_CHECK_COMMAND}}`

## 3. Pre-Flight Verification Checklist
Before completing an issue or handing off work back to a human developer, verify you have checked off the following items:

- [ ] Every file added or modified has been processed using `{{FORMAT_COMMAND}}`.
- [ ] Static type checking (`{{TYPE_CHECK_COMMAND}}`) passes with zero errors.
- [ ] The full suite or relevant module suite via `{{TEST_COMMAND}}` passes with zero failures.
- [ ] No temporary debugging statements, left-over console blocks, or unreachable testing artifacts remain in the code.

> **Failure to Comply:** If any of the above commands fail, you must treat the failure as a regression bug. Re-enter the triage loop (`/diagnose`), resolve the formatting or testing errors, and run this verification sequence again.