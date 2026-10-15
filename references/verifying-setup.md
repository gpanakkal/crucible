# Verifying Test Setup

1. Verify all the following packages are installed on the project: `vitest fast-check @stryker-mutator/core @stryker-mutator/vitest-runner @stryker-mutator/typescript-checker`
2. Verify Vitest and Stryker configurations correctly include/exclude files. Stryker should not be checking files that only contain test data
3. Verify Stryker config:
    1. Uses the `clear-text` reporter (other reporters optional).
    2. Uses the TypeScript checker and correctly points to the TS config file.
    3. Sets `coverageAnalysis: 'perTest'`, so each mutant runs only the tests that cover it.
    4. Enables `incremental: true`, so reruns only re-test mutants whose code or tests changed. The incremental file should live in a gitignored folder.
    5. Sets `concurrency` explicitly (e.g., a fixed number or `"50%"`) if several Stryker runs may happen at once. The default uses all but one CPU core per run.
4. Look for any other configuration issues that might cause problems in the test writing workflow.
5. Report findings to the user.
