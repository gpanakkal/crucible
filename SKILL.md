---
name: crucible
compatibility: Designed for TypeScript projects using Vitest, fast-check and Stryker Mutator
description: Write solid unit tests using property-based testing, mutation testing, and fuzzing.
---

# Crucible

## When to use this

- When asked to write, fix, or audit unit tests on TypeScript projects

## When NOT to use this

- UI tests
- Simulation tests

## Rules (read before running)

- Do not modify application code unless specifically prompted to do so.
- When asked to add tests, do not modify existing tests.
- When asked to fix tests, do not add new tests.
- When asked to audit tests, fix existing tests and then add tests as needed to meet test criteria.

### Test Criteria

Unit tests should:

- Have the maximum possible branch coverage per Vitest.
- Achieve the maximum possible mutation score out of all code in scope of the prompt (not just what's covered by tests). Unkillable mutants will prevent a score of 100.
- Be property-based whenever possible, except if only a handful of input cases exist. E.g., a function with a single boolean parameter and no implicit inputs has only two possible input cases, so don't bother with making it property-based.
- (if property-based) have arbitraries that cover all possible parameters and implicit inputs. It is vital that no cases that could occur in production are excluded. If necessary or unclear, err towards making arbitraries too broad.
- Fail if they test erroneous code or if arbitraries are purposely made too broad. Think of tests as requirements: they should be named accordingly, and should automatically pass as soon as the user fixes the bug in the future after the user fixes the function and/or arbitraries. Don't use `test.fails`/`.skip`; this makes it less obvious to the user that attention is required, so tests passing when they shouldn't is the highest-priority error to avoid.

Check branch coverage and run tests: `pnpm exec vitest run src/foo.test.ts --coverage`
Check for surviving mutants on the code being tested: `pnpm exec stryker run --mutate "src/foo.ts"`

## Task Instructions

- [Verifying testing setup](references/verifying-testing-setup.md)
- [Writing new tests](references/writing-new-tests.md)
- [Auditing Tests](references/auditing-tests.md)