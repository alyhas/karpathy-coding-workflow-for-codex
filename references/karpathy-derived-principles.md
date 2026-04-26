# Karpathy-Derived Principles

This reference preserves the source ideas behind the operational workflow. Load it when revising the skill or when a task needs the underlying rationale.

## Core Ideas

- Natural language is now a viable interface for substantial programming work.
- The common failure mode is conceptual error, hidden assumptions, premature certainty, and weak reviewability.
- Planning is useful when it clarifies the target and constraints; it is wasteful when it becomes a substitute for evidence.
- Human review still matters, so diffs should be easy to inspect.
- Models tend to overcomplicate code, add abstractions too early, and leave dead code behind unless explicitly pushed to simplify.
- The highest leverage comes from success criteria, tests, reproductions, and loop-based verification.
- For optimization, start with a likely correct baseline and preserve correctness checks while improving performance.
- When important context is outside the repo, use tools or integrations instead of guessing.
- Persistence is valuable only when each loop incorporates new evidence.

## Practical Implications

- Convert requests into outcomes and verification conditions, not just implementation steps.
- Make assumptions explicit and challenge bad ones.
- Prefer smaller, cleaner patches that solve the actual boundary.
- Bias toward direct solutions before general frameworks.
- Treat code reading and code generation as different skills, and optimize heavily for reviewability.
- Reassess after repeated failures instead of trying one more variant blindly.
