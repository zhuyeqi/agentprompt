# Agent Instructions

Last updated: 2026-05-19

## Priority

1. Current user request
2. Nearest directory instructions
3. Repository instructions
4. Global preferences

If instructions conflict, state the conflict and follow the higher-priority instruction.

## Communication

- Reply in the user's language.
- Code, comments, and commit messages must be in English.
- Use Conventional Commits for Git commits.
- State conclusions first, then supporting reasoning.
- Make key assumptions explicit.
- If multiple reasonable interpretations exist, surface options and tradeoffs before choosing.
- Be concise.
- Show code and diffs when useful; minimize prose around them.
- Only explain non-obvious decisions.

## Engineering

- Inspect existing patterns before editing.
- Solve root causes, not symptoms.
- Prefer the simplest complete solution.
- Make surgical changes only.
- Every changed line should trace to the request, spec, bug hypothesis, or validation need.
- Match existing style and structure.
- Do not add speculative features.
- Do not introduce single-use abstractions or flexibility for hypothetical future needs.
- Do not refactor or clean up unrelated code opportunistically.
- Prefer deletion over addition.
- Remove commented-out code, TODO-only placeholders, and code made unused by your changes.
- Push back on unnecessary complexity.

## Scope

- If the task is unclear, ask before coding.
- Non-trivial changes need a spec and explicit approval before implementation.
- Non-trivial means changes that alter public behavior, data contracts, persistence, auth/security, user workflows, or more than one subsystem.
- Mechanical-only, documentation-only, and bug-fix changes do not require a new spec.
- If implementation reveals the spec is wrong, update the spec first.

## Testing

- Define success criteria before coding.
- Convert tasks into verifiable outcomes.
- Test business behavior, not implementation details.
- Use realistic domain data when possible.
- Assert outcomes, not intermediate internals.
- New behavior requires tests unless the change is documentation-only, mechanical-only, or explicitly exploratory.
- Bug fixes should include a regression test when practical.
- If tests are impractical, explain why and use another verification method.
- Verify the requested behavior before considering the task done.

## Bug Protocol

When given a bug:

1. Restate the problem briefly.
2. Propose at least two root-cause hypotheses.
3. Validate hypotheses before fixing.
4. Fix autonomously unless the action is destructive.
5. Verify the bug no longer reproduces.

If all hypotheses fail, state what was tried and ask for more information.

## Git Safety

- Check `git status` before editing when making code changes.
- Never discard, overwrite, or revert user changes unless explicitly requested.
- Ask before destructive actions such as `git reset --hard`, `git checkout --`, or deleting files with user data.
- Review `git diff` before final response.
- Stage only files changed for the current task.
- Use Conventional Commits.

## Security

- Never log credentials, tokens, or secrets.
- Never commit `.env`, credentials, or key files.
- Never delete or modify real environment data.
- Keep tests isolated from production systems.
- When editing code that contains injection risks, fix in-scope risks and mention out-of-scope risks.

## Completion

A task is complete only when:

- The requested change is implemented, or the blocker is clearly stated.
- Relevant verification has run.
- The final response lists changed files, verification, and remaining risk.
