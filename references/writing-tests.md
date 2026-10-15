# Writing Tests

Prerequisites: read [test-criteria.md](test-criteria.md), [assessing-a-module.md](assessing-a-module.md), [mutation-testing.md](mutation-testing.md), and [debrief-template.md](debrief-template.md) before starting.

When asked to write new tests standalone, DO NOT MODIFY APPLICATION CODE OR EXISTING TESTS. (When embedded in a workflow that owns code changes, that workflow's rules govern code changes — see the Rules section of SKILL.md.)

First, **assess existing tests** by following [assessing-a-module.md](assessing-a-module.md). Create a new debrief file using [the template](debrief-template.md) and record the initial coverage and mutation scores there.

Second, **write tests following this process exactly**:

Do the following for each function/method in the module's interface, finishing one function before starting the next:

1. Determine the function's purpose by examining comments, its name, its type signature, and how it's used. If uncertain, make a note of this in the debrief, skip writing tests, and move on to the next function.
2. Make note of any potential bugs in the function's implementation.
3. Based on its purpose, identify any faulty assumptions the function makes about its parameters and implicit inputs, and make note of any input cases that are likely to lead to incorrect function behavior. For example, a function that takes a positive integer but doesn't validate its input makes a faulty assumption about its input.
4. NEVER MODIFY PRE-EXISTING TESTS. If you find any problems in existing tests, notify the user of problems found in existing tests.
5. Write new tests by doing the following:
   a. Using `fast-check`, create property-based test stubs with arbitraries that cover all possible parameters and implicit inputs to the function. Use `fc.asyncProperty` + `await fc.assert(...)` when the function under test is async. If in doubt, err on the side of making arbitraries too broad and mention this in the debrief so the user can fix them. Name tests as descriptions of desired behavior.
   b. Using `vitest`, write assertions within the stubs covering any returned values and side effects such as throwing exceptions, mutating inputs, mutating/reassigning variables from outer scopes, etc. Make sure tests assert desired behavior, catching the faulty assumptions/bugs identified earlier and failing accordingly.
6. Re-check coverage: `pnpm exec vitest run src/foo.test.ts --coverage --coverage.include=src/foo.ts`, and revise the new tests until coverage criteria in [test-criteria.md](test-criteria.md) are met for the function.
7. Update the debrief with a section on this function.

Third, **mutation test the module** per [mutation-testing.md](mutation-testing.md):

1. Run one mutation test covering the line ranges of every function you wrote tests for.
2. For each function with surviving mutants, revise its new tests (steps 5a and 5b above), then rerun only the line ranges that had survivors. Repeat until the mutation criteria in [test-criteria.md](test-criteria.md) are met.
3. Record unkillable mutants in each function's debrief section.

Finally, double-check that you added sections to the debrief for each function and finish writing the summary section.
