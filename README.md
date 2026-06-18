# Crucible

A skill for coding agents enabling them to write robust unit test suites without user intervention.

## What it does

When prompted to write tests, models will generate property-based unit tests using branch coverage and mutation score as guiding metrics. Properties will generate inputs (including implicit inputs) across the full range of possible input configurations. Also generates a debrief post-run detailing bugs found in application code and limitations in generated tests.

## Usage

Install: `npx skills add gpanakkal/crucible`

- "write tests for [scope]" - add new tests without touching existing ones. Limit scope to a file/module/feature to avoid context bloat.
- "audit tests for [scope]" - search for issues in existing tests
- "verify the testing setup" - validate required dependencies and testing configs

## Opt-out

This skill will be used by default. It can be defaulted to off per-project using either:

- A .no-crucible file in the project root
- "crucible: false" anywhere in AGENTS.md or .claude/settings.json