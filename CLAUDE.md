# Global Preferences

Last updated: 2026-04-15

## Communication

- Follow the user's language: reply in Chinese if the user writes in Chinese, otherwise reply in English.
- Code, comments, and commit messages must be in English.
- Use [Conventional Commits](https://www.conventionalcommits.org/) for Git commits.
- Use Mermaid for complex flows, dependencies, or state transitions.
- State conclusions first, then supporting reasoning.
- Make key assumptions explicit.
- If multiple reasonable interpretations exist, do not choose silently; surface options and tradeoffs first.

## Response Style

- Be concise. No trailing summaries of what was just done.
- Show code and diffs; minimize prose around them.
- Only explain non-obvious decisions.

## Problem Solving

- Think one level higher: solve root causes, not just symptoms.
- Prefer the simplest solution that fully solves the problem.
- Do not add speculative features.
- Push back on unnecessary complexity when a simpler approach exists.
- If the task is unclear, stop and clarify before coding.

## Scope & Simplicity

Before writing code, ask:

1. What exact problem does this solve?
2. Does the codebase already have something reusable?
3. Will this likely still matter in 6 months?

Rules:

- Make surgical changes only. Change only what is necessary for the current task.
- Every changed line should be traceable to the request, the spec, a bug hypothesis, or validation needs.
- Match the existing local style and structure unless the task requires otherwise.
- Prefer deletion over addition.
- Remove commented-out code, TODO-only placeholders, and code made unused by your changes.
- Do not introduce single-use abstractions or flexibility for hypothetical future needs.
- Do not refactor or clean up unrelated code opportunistically. If you notice unrelated dead code or issues, mention them instead of silently fixing them.
- If a solution feels bloated, rewrite it smaller.

## Verification & Testing

- Define success criteria before coding.
- Convert tasks into verifiable outcomes. "Looks correct" is not verification.
- Each step in a multi-step task should have a corresponding check.

Testing rules:

- Test business behavior, not implementation details.
- Use realistic domain data when possible.
- Assert outcomes, not intermediate internals.
- Tests should remain valid across refactors.
- New features require tests.
- Bug fixes require regression tests.

Examples:

- "Fix the bug" → reproduce with a test, then make it pass.
- "Add validation" → add tests for invalid input, then make them pass.
- "Refactor" → preserve behavior and verify with tests before and after.

## Security

- Never log credentials, tokens, or secrets.
- Never commit .env, credentials, or key files.
- Never delete or modify real environment data. Tests must be isolated from production — use in-memory databases, mocks, or dedicated test fixtures.
- When editing code that contains injection risks (SQL, XSS, command), mention the risk and fix it within the scope of the current change. For risks outside your scope, mention them without fixing.

## Workflow

- Prefer small, incremental edits over large rewrites.
- In multi-file work, implement the smallest working core first, then extend outward.
- If 2 consecutive searches or file reads don't yield actionable findings, stop and state what will be changed next and why.
- After changes, verify with tests, logs, and diff review.
- If the current direction is based on a wrong assumption, stop and re-plan instead of patching around it.
- When stuck: state what was tried, why it failed, and propose 2 alternative approaches before asking for help.

## Bug Protocol

When given a bug:

1. Restate the problem briefly to confirm understanding.
2. Propose at least 2 root-cause hypotheses.
3. Validate hypotheses yourself and fix the issue without step-by-step confirmation unless the action is destructive.
4. If all hypotheses fail, ask the user for more information.

Rules:

- Fix bugs autonomously.
- Bug fixes must include a reproducible test when practical.
- Verify the bug no longer reproduces before considering the task done.

## Spec-Driven Development

- No spec, no code for non-trivial features.
- A spec should define goal, scope, interface, constraints, and validation.
- No approval, no execute for non-bug non-trivial code changes. Approval means explicit user confirmation in conversation.
- Spec is the source of truth.
- If implementation reveals the spec is wrong, update the spec first.
- If changes affect behavior, contracts, constraints, or design decisions, sync the spec.
- Mechanical-only changes do not require a spec.

## Quality Bar

- Keep diffs tight, direct, and explainable.
- Prefer correctness, simplicity, and verifiability over cleverness.
- Do not widen task scope without explicitly stating why.
- A task is not done until the result is verified.