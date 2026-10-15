# Running Mutation Tests

Stryker runs take minutes and compete for CPU with other work on the machine, so treat every run as expensive.

## Command

- If the project documents its own Stryker command (e.g., a scoped config that runs only the colocated tests, in AGENTS.md, CLAUDE.md, or the README), use it in place of the default below.
- Otherwise, use: `pnpm exec stryker run --mutate "<file>:<startLine>-<endLine>"`
- Always scope `--mutate` to the files, and wherever possible the line ranges, in scope of the task. Never run Stryker without `--mutate` unless explicitly asked for a project-wide score.
- If the project has not enabled incremental mode in its Stryker config, pass `--incremental` so reruns only re-test mutants whose code or tests changed. Pass `--force` as well if the stored results seem stale (e.g., after a dependency or config change).

## When to run

- Run once to get the baseline for a module, then once after writing its tests.
- When mutants survive, revise the tests, then rerun only the line ranges that had survivors.
- Do not rerun on a scope whose source and tests are unchanged since the last run; reuse that run's results.
- Do not run when only test files changed, except to confirm that previously surviving mutants are now killed.
- When reviewing tests whose author already reported mutation results for the current code, use those results instead of rerunning, unless the code or tests have changed since.
- Before finishing, check that the mutated scope covers every non-test source file changed in the task (e.g., compare against `git diff --name-only`).

## Waiting on a run

If the environment can run commands in the background and notify you when they finish, use that for long runs instead of polling with sleep loops, and do other work in the meantime.

## Surviving mutants

- Kill survivors by writing or revising tests for the behavior the mutant breaks, not by asserting on implementation details.
- If a mutant survives two targeted attempts, decide whether it is unkillable (e.g., an equivalent mutant, or one only observable through timing or logging). If so, record it under "Unkillable mutants" in the debrief with a one-line reason and move on instead of rerunning further.

## Delegating survivor work

Killing survivors is narrow work that does not need the rest of the task's history. When embedded in a long-running workflow, and subagents are available and the workflow doesn't forbid them, prefer handing it to a fresh subagent with a small context. Give it:

- the list of survivors (file, line, and mutation);
- the source and test file paths;
- the paths to [test-criteria.md](test-criteria.md) and this file;
- the exact mutation command, scoped to the ranges with survivors.

Ask it to return the updated mutation score, the tests it added or changed, and any mutants it judged unkillable, with reasons. Review its test changes against [test-criteria.md](test-criteria.md) before accepting them.
