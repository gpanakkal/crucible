---
name: crucible
description: Write solid unit tests using property-based testing and mutation testing.
compatibility: Designed for TypeScript projects.
---

# Crucible

## When to use this

When asked to write, fix, or audit unit tests on TypeScript projects.

## When NOT to use this

When writing end-to-end, integration, UI, or simulation tests.

## Rules

- Example commands use `pnpm`, but always use the project's package manager.
- Do not modify application code unless specifically prompted to do so.
- When asked to add tests, do not modify existing tests.
- When asked to fix tests, do not add new tests.
- When asked to audit tests, fix existing tests and then add tests as needed to meet test criteria.

## Test Criteria

Unit tests should:

- Have the maximum possible branch coverage per Vitest.
- Achieve the maximum possible mutation score out of all code in scope of the prompt (not just what's covered by tests). Unkillable mutants will prevent a score of 100.
- Be property-based whenever possible, except if only a handful of input cases exist. E.g., a function with a single boolean parameter and no implicit inputs has only two possible input cases, so don't bother with making it property-based.
- (if property-based) have arbitraries that cover all possible parameters and implicit inputs. It is vital that no cases that could occur in production are excluded. If necessary or unclear, err towards making arbitraries too broad.
- Fail if they test erroneous code or if arbitraries are purposely made too broad. Think of tests as requirements: they should be named accordingly, and should automatically pass as soon as the user fixes the bug in the future after the user fixes the function and/or arbitraries. Don't use `test.fails`/`.skip`; this makes it less obvious to the user that attention is required, so tests passing when they shouldn't is the highest-priority error to avoid.

Check branch coverage and run tests: `pnpm exec vitest run src/foo.test.ts --coverage`
Check for surviving mutants on the code being tested: `pnpm exec stryker run --mutate "src/foo.ts"`

## Verifying test setup

1. Verify all the following packages are installed on the project: `vitest fast-check @stryker-mutator/core @stryker-mutator/vitest-runner @stryker-mutator/typescript-checker`
2. Verify Vitest and Stryker configurations correctly include/exclude files. Stryker should not be checking files that only contain test data
3. Verify Stryker config:
    1.  Uses the `clear-text` reporter (other reporters optional).
    2. Uses the TypeScript checker and correctly points to the TS config file.
4. Look for any other configuration issues that might cause problems in the test writing workflow.
5. Report findings to the user.

## Writing Tests

When asked to write new tests, DO NOT MODIFY APPLICATION CODE OR EXISTING TESTS.

First, **assess existing tests** per the criteria above and make note of the coverage and mutation scores in a new debrief file. Use [the template](references/debrief-template.md).

Second, **write tests following this process exactly**:

Do the following for each function/method in the module's interface, finishing one function before starting the next:

1. Determine the function's purpose by examining comments, its name, its type signature, and how it's used. If uncertain, make note of this for the debrief and move on to the next function.
2. Make note of any potential bugs in the function's implementation.
3. Based on its purpose, identify any faulty assumptions the function makes about its parameters and implicit inputs, and make note of any input cases that are likely to lead to incorrect function behavior. For example, a function that takes a positive integer but doesn't validate its input makes a faulty assumption about its input.
4. NEVER MODIFY PRE-EXISTING TESTS. If you find any problems in existing tests, notify the user of problems found in existing tests.
5. Write new tests by doing the following:
   a. Using `fast-check`, create property-based test stubs with arbitraries that cover all possible parameters and implicit inputs to the function. Use `fc.asyncProperty` + `await fc.assert(...)` when the function under test is async. If in doubt, err on the side of making arbitraries too broad and mention this in the debrief so the user can fix them. Name tests as descriptions of desired behavior.
   b. Using `vitest`, write assertions within the stubs covering any returned values and side effects such as throwing exceptions, mutating inputs, mutating/reassigning variables from outer scopes, etc. Make sure tests assert desired behavior, catching the faulty assumptions/bugs identified earlier and failing accordingly.
6. Re-check coverage: `pnpm exec vitest run src/foo.test.ts --coverage`
7. Mutation test only the current function: `pnpm exec stryker run --mutate "src/foo.ts:<startLine>-<endLine>"`
8. Revise the newly written tests and repeat steps 5a and 5b until test criteria (listed above) are met for the function.
9. Update the debrief with a section on this function.

## Auditing Tests

Look for modules or functions that don't have tests and report these to the user in the post-audit debrief.

For each module with tests, assess them per the criteria above:
1. Check code coverage using Vitest: `npx vitest run my-file-name.test.ts --coverage`.
2. Check for surviving mutants on the module using Stryker Mutator: `npx stryker run --mutate <file path relative to project root>`

For functions with tests:
- For property-based tests: 
  - look for inputs that the function would accept without throwing or returning an error value, but cannot be generated by the arbitraries. Widen arbitraries as needed to include any such inputs.
  - look for inputs that aren't covered by arbitraries, especially implicit inputs such as class fields, global variables, date/time, and randomly generated numbers. Add arbitraries for these.
- Fix any errors in mock implementations.
- Look for performance bottlenecks.
