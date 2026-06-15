### Verifying test setup
When asked to verify the unit test setup, follow this process exactly:
1. Verify all the following packages are installed on the project: `vitest fast-check @stryker-mutator/core @stryker-mutator/vitest-runner @stryker-mutator/typescript-checker`
2. Verify Vitest and Stryker configurations correctly include/exclude files. Stryker should not be checking files that only contain test data
3. Verify Stryker config:
    1.  Uses the `clear-text` reporter (other reporters optional).
    2. Uses the TypeScript checker and correctly points to the TS config file.
4. Look for any other configuration issues that might cause problems in the test writing workflow.
5. Report findings to the user.
