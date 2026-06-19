# Crucible

Crucible makes agents write comprehensive tests using property-based testing with broad arbitraries and mutation scoring, so you don't have to audit for missed edge cases or tests that pass too easily.

After generating tests, outputs a debrief detailing bugs found in application code and issues/limitations in generated tests.

## Usage

Install: `npx skills add gpanakkal/crucible`

- "write tests for [scope]" - add new tests without touching existing ones. Limit scope to a file/module/feature to avoid context bloat.
- "audit tests for [scope]" - search for issues in existing tests
- "verify the testing setup" - validate required dependencies and testing configs

## Opt-out

This skill will be used by default. It can be defaulted to off per-project using either:

- A .no-crucible file in the project root
- "crucible: false" anywhere in AGENTS.md or .claude/settings.json