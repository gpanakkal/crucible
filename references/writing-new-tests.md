
### Writing Tests

When asked to write new tests for a given module/file, DO NOT MODIFY APPLICATION CODE OR EXISTING TESTS.

First, **assess existing tests** per the criteria above and make note of the coverage and mutation scores in the debrief.

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
9. Add a section to the debrief 

Finally, **debrief the user** on every function you iterated over.

### Test Debriefs

Format debriefs per the section below. If there is nothing to report in a function subsection, simply write "n/a". Output the debrief into a Markdown file in `test-writing-debriefs/`.

#### Debrief: {moduleName/fileName}

**Coverage** (branch)
Before: X% → After: Y%
Lines that could not be covered: {line ranges}

**Mutation score** (total)
Before: X% → After: Y%

##### {functionName}

**Function purpose**
{one sentence describing what the function is supposed to do}
(**confidence**: high | uncertain)
{if uncertain: what's unclear and why}

**Faulty assumptions found**

- (line {line number/range}): {assumption about input type/range/shape that the function doesn't validate}

**Bugs found in implementation**

- (line {line number/range}): {description + line number}

**Issues found in pre-existing tests**

- (line {line number/range}): {issue description + test name}

**Test cases written**

- {brief description of each property/invariant tested}

**Failing tests**

- (line {line number/range}): {test name + reason}

**Unkillable mutants**

- (line {line number/range}): {brief description}
