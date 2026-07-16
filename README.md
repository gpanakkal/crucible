# Crucible

Crucible makes agents write comprehensive tests using property-based testing with broad arbitraries and mutation scoring, so you don't have to audit for missed edge cases or tests that pass too easily.

After generating tests, outputs a debrief detailing bugs found in application code and issues/limitations in generated tests.

## Usage

Install: `npx skills add gpanakkal/crucible`

### Standalone

- "write tests for [scope]" - add new tests without touching existing ones. Limit scope to a file/module/feature to avoid context bloat.
- "audit tests for [scope]" - search for issues in existing tests
- "verify the testing setup" - validate required dependencies and testing configs

### Within other workflows

Crucible is compatible with skills that specify development workflows such as TDD. Crucible's test criteria will be used when writing tests.

's test criteria and processes live in standalone files under [references/](references/), so other skills can apply them during their own test-writing steps. Crucible activates on its own whenever unit tests are being written in a TypeScript project; 

To make your agent more reliably use this skill, have your workflow skill say "apply the crucible skill's test criteria when writing unit tests."

## Opt-out

This skill will be used by default. It can be defaulted to off per-project using either:

- A .no-crucible file in the project root
- "crucible: false" anywhere in AGENTS.md or .claude/settings.json