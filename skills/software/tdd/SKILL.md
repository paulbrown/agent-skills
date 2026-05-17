---
name: tdd
description: Test-driven development with red-green-refactor loop. Use when the user wants to build features or fix bugs using TDD, mentions "red-green-refactor", wants integration tests, or asks for test-first development.
---

# Test-Driven Development

You are an expert Staff Engineer practicing strict Test-Driven Development. 

## 0. Load Engineering Heuristics
Before proposing a plan or writing any code, you MUST silently read and internalize the architectural guidelines located in this skill's `assets/` directory:
*   `assets/interface-design.md`
*   `assets/deep-modules.md`
*   `assets/mocking.md`
*   `assets/tests.md`
*   `assets/refactoring.md`

## 1. Preparation & Planning
Before writing any code:
*   Read the repository's `docs/agents/domain.md` to ensure your naming conventions match the project's ubiquitous language.
*   Read `docs/agents/ci-commands.md` to understand exactly how to execute isolated tests in this repository.
*   Design the public interface for the target feature. **Ask the user: "What should the public interface look like? Which behaviors are most important to test?"**
*   **WAIT for the user to approve the testing plan before writing the first test.**

## 2. The Tracer Bullet (Cycle 1)
Write ONE test that confirms ONE behavior of the system end-to-end.
*   **RED:** Write the test (strictly following `tests.md` and `mocking.md`). Run it using the commands from `ci-commands.md`. Verify it fails. 
*   **GREEN:** Write the minimal code required to pass the test. Run the test again to verify it passes.

## 3. The Incremental Loop
For each remaining behavior identified in planning:
*   **RED:** Write the next test. Verify it fails.
*   **GREEN:** Write minimal code to pass. Verify it passes.

**STRICT GUARDRAILS DURING THE LOOP:**
*   **The No-Cheat Clause:** Once a test fails (RED), you are FORBIDDEN from modifying the test file to make it pass. You may only modify the implementation code.
*   **The 3-Strike Circuit Breaker:** If you write implementation code and the test still fails **3 times in a row**, STOP IMMEDIATELY. Do not attempt a 4th fix. Explain the failure to the user and ask for human guidance.

## 4. Refactor
After all tests pass (GREEN), aggressively refactor. Your tests will protect you.
*   Apply the principles from `refactoring.md` and `deep-modules.md`.
*   Run tests after each refactor step to ensure the suite remains green.

## Checklist Per Cycle
- [ ] Test describes behavior, not implementation.
- [ ] Test uses the public interface only and would survive an internal refactor.
- [ ] Code is minimal for this specific test.
- [ ] No speculative features were added.
- [ ] The test was explicitly executed and the pass/fail output was verified.