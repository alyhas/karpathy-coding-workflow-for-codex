# Review Checklist

Use before reporting completion on a substantial coding task.

## Goal and Boundaries

- Is the implemented behavior the user's actual outcome, not just their proposed mechanism?
- Did I identify material assumptions, constraints, non-goals, and changed contracts?
- Did I preserve unrelated files, comments, formatting, and behavior?

## Correctness

- Did I trace the real caller, runtime, route, data, or UI boundary?
- Does a test, reproduction, fixture, assertion, benchmark, or smoke check cover the important behavior?
- If coverage is manual, is the exact manual evidence clear enough to repeat?
- Did I check edge cases introduced by the chosen design?

## Simplicity

- Is there a smaller local change that would satisfy the same evidence?
- Did every new abstraction, option, helper, or wrapper pay for itself?
- Did I delete dead code, stale branches, obsolete comments, and unused imports created by the change?

## Final Report

- State what changed, where, and why.
- State exactly what validation ran and whether it passed.
- Call out only real residual risk or unavailable checks.
