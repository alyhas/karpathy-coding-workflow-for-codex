---
name: karpathy-coding-workflow
description: Use when Codex is doing non-trivial implementation, debugging, refactoring, optimization, or code review work in a real repo and needs explicit outcomes, repo reading before edits, tests or other verification, simple design, assumption checks, cleanup, and a reviewable diff.
---

# Karpathy Coding Workflow

Use a natural-language-first coding loop: turn the request into a small English spec, check it against the repo, implement the simplest correct change, simplify, verify, and report the evidence.

System, user, `AGENTS.md`, and repo-specific instructions override this skill. If a narrower domain skill applies, use that skill with this workflow rather than replacing it.

## First Move

- Rewrite the request as `Goal`, `Context`, `Constraints`, `Done when`, and `Non-goals`.
- Identify assumptions that would change the implementation, public contract, data model, performance target, or verification plan.
- Ask only when the missing answer is material and cannot be discovered locally. Otherwise state the assumption and keep moving.
- If the requested approach conflicts with repo evidence, push back with the concrete reason and propose the smaller correct path.

## Execution Loop

1. **Read before writing**
   - Search the repo, inspect callers, tests, configs, migrations, generated types, and comments near the change.
   - Trace the real runtime or data boundary before choosing a fix.
   - Preserve unrelated behavior, formatting, comments, and user edits.

2. **Build a correctness harness**
   - Prefer a failing test, reproduction, fixture, assertion, smoke script, or benchmark before changing behavior.
   - For bug fixes, reproduce the bug when feasible and keep the reproduction as regression coverage.
   - For performance work, establish a correctness baseline first; speedups do not count if behavior drifts.
   - If automated coverage is not practical, define the manual or executable check before implementation.

3. **Choose the simplest correct design**
   - Start with the direct solution that satisfies the harness.
   - Prefer a boring local change over a new abstraction, framework, wrapper, or broad rewrite.
   - Add an abstraction only when it removes real duplication or makes the contract easier to verify.
   - Keep public APIs small, unsurprising, and consistent with existing patterns.

4. **Implement tightly**
   - Edit the narrowest responsible files.
   - Keep names concrete and data flow obvious.
   - Delete dead code made obsolete by the change.
   - Do not mix cosmetic churn, opportunistic refactors, or unrelated cleanup into the patch.

5. **Simplify after green**
   - Re-read the changed path and collapse unnecessary layers.
   - Remove speculative options, stale branches, unused helpers, and defensive code that does not defend a real boundary.
   - If the final shape is still awkward, revisit the brief before adding more code.

6. **Verify and review**
   - Run the narrowest relevant check first, then broader checks proportional to risk.
   - Inspect the diff for assumption drift, brittle logic, hidden behavior changes, untested branches, dead code, and reviewer friction.
   - Treat passing tests as evidence, not proof; still reason through the actual code path.

## Decision Rules

- If repeated attempts fail, stop trying variants and reframe the problem from the evidence.
- If external facts, vendor APIs, production settings, or current docs matter, use available tools instead of guessing.
- If the user asks for a workaround but the permanent fix is local and safe, implement the permanent fix.
- If a change cannot be fully verified, make the unverified boundary explicit and explain what evidence is still missing.

## Bundled Resources

- Use `assets/task-brief-template.md` when the prompt is fuzzy, cross-cutting, or risky.
- Use `assets/review-checklist.md` before reporting completion on substantial code changes.
- Read `references/karpathy-derived-principles.md` only when you need the underlying principles or are revising this skill.

## Completion Report

Keep the final report short and evidence-backed:

- What changed and why.
- The files or surfaces touched.
- The verification run and the result.
- Any material risk, skipped check, or remaining unknown.

## Common Mistakes

- Accepting a flawed user-proposed design without checking the repo.
- Planning forever instead of using the plan to drive edits and checks.
- Adding abstractions because the task feels important rather than because the code demands them.
- Letting generated code grow while forgetting to delete obsolete branches.
- Claiming completion from a green test run without reviewing the real changed path.
