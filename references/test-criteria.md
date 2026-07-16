# Test Criteria

These criteria define what "done" means for unit tests. Apply them whenever writing, fixing, or evaluating tests — including when test-writing happens as a step inside another workflow.

Unit tests should:

- Have the maximum possible branch coverage per Vitest.
- Kill all killable mutants, achieving the maximum possible mutation score out of all code in scope of the prompt (not just what's covered by tests). Unkillable mutants will prevent a score of 100.
- Be property-based whenever possible, except if only a handful of input cases exist. E.g., a function with a single boolean parameter and no implicit inputs has only two possible input cases, so don't bother with making it property-based.
- (if property-based) have arbitraries that cover all possible parameters and implicit inputs. It is vital that no cases that could occur in production are excluded. If necessary or unclear, err towards making arbitraries too broad.
- Fail if they test erroneous code or in certain cases when arbitraries are purposely made overly broad. Think of tests as requirements: the name should describe desired behavior, and if a test catches a bug, it should fail now but pass without requiring revisions to the test's logic once the bugs in the function (or in the definitions of arbitraries) are fixed. Only define tests as expected to fail (e.g., `test.fails`) or be skipped (e.g., `test.skip`) if instructed to.

## Checking the criteria

Check branch coverage and run tests: `pnpm exec vitest run src/foo.test.ts --coverage`
Check for surviving mutants on the code being tested: `pnpm exec stryker run --mutate "src/foo.ts"`
