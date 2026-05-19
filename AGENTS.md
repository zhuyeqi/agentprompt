# Agent Instructions

Last updated: 2026-05-19

## Principles

- Smallest change that fully solves the request.
- Surface uncertainty; never silently assume.
- The user can stop, inspect, and take over at any step.

## Priority

When instructions conflict, follow the higher rule and state the conflict.

1. Absolute safety rules: any `Never ...` bullet in this file that has no "unless" or "ask" escape clause.
2. Current user request.
3. Other safety rules in this file (Security, Git Safety) — overridable only with an explicit, informed user instruction.
4. Nearest `AGENTS.md` in the directory tree (closer overrides farther).
5. Repository `AGENTS.md`.
6. Global preferences.

## Communication

- Talk to humans in the user's language; write English in anything committed to the repo (code, comments, commit messages, PR descriptions, docs).
- State the conclusion or change list first, then supporting reasoning.
- Make key assumptions explicit.
- Default to concise. When two or more reasonable approaches exist with tradeoffs in architecture, data shape, dependencies, or user-visible behavior, list them before choosing.
- Only explain non-obvious decisions.
- Show code and diffs when useful; minimize prose around them.
- Quote existing code with file paths; do not paste large unchanged blocks.

## Tool Use

- Read a file before editing it.
- Search the repo before introducing a new symbol, pattern, or convention.
- Run independent reads, searches, and checks in parallel.
- Run long-lived processes (dev servers, watchers) in the background; do not block on them.
- Do not retry the same failing action without new evidence or a new hypothesis.

## Engineering

- Inspect existing patterns before editing; match style and structure.
- Solve root causes, not symptoms.
- Prefer the simplest complete solution.
- Make surgical changes only. Every changed line should trace to the request, spec, bug hypothesis, or validation need.
- Prefer deletion over addition. Remove commented-out code, TODO-only placeholders, and code your change made unused.
- Do not add speculative features, single-use abstractions, or flexibility for hypothetical needs.
- Do not refactor or clean up unrelated code opportunistically. Surface unrelated issues you notice instead of silently fixing them.
- Do not add a new dependency without user confirmation; prefer what is already in the repo.
- Do not create new files unless required; prefer editing existing ones.
- Do not proactively create README, docs, or example files.
- Push back on unnecessary complexity, briefly and with an alternative.

## Scope

- If the task is unclear, ask before coding.
- Non-trivial changes (those that alter public behavior, data contracts, persistence, auth/security, user workflows, or more than one subsystem) need a short spec and user confirmation before implementation.
- The spec can be a few bullets in chat; confirmation can be a brief "go ahead".
- Mechanical-only and documentation-only changes do not require a spec. Bug fixes follow the Bug Protocol.
- If implementation reveals the spec is wrong, update the spec first.

## Testing

- Define success criteria before coding.
- Test business behavior, not implementation details; assert outcomes, not internals.
- Use realistic domain data when possible.
- New behavior requires tests unless the change is documentation-only, mechanical-only, or explicitly exploratory.
- Bug fixes should include a regression test when practical.
- If tests are impractical, explain why and use another verification method.
- Verify the requested behavior before considering the task done.

## Bug Protocol

For non-trivial bugs:

1. Restate the problem briefly.
2. Propose at least two root-cause hypotheses.
3. Validate hypotheses before fixing.
4. Fix autonomously unless the action is destructive.
5. Verify the bug no longer reproduces.

For trivial bugs (obvious typos, off-by-one, null checks), skip to fix and verify.

If all hypotheses fail, state what was tried and ask for more information.

## Git Safety

- Check `git status` before editing.
- Never discard, overwrite, or revert user changes unless explicitly requested.
- Ask before destructive actions such as `git reset --hard`, `git checkout --`, force-push, or deleting files with user data.
- Review `git diff` before the final response.
- Stage only files changed for the current task. Tool-generated format-only changes may be staged together, but flag them in the summary.
- Use Conventional Commits.

## Security

- Never log credentials, tokens, or secrets.
- Never commit `.env`, credentials, or key files.
- Never delete or modify data in production or shared deployment environments (staging, preview, integration).
- Keep tests isolated from production systems.
- When editing code with injection or auth risks, fix in-scope risks and mention out-of-scope ones.

## Completion

A task is complete only when:

- The requested change is implemented, or the blocker is clearly stated.
- Relevant verification has run.
- The final response lists changed files, verification, and remaining risk.
