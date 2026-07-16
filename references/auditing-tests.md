# Auditing Tests

Prerequisites: read [test-criteria.md](test-criteria.md), [assessing-a-module.md](assessing-a-module.md), and [debrief-template.md](debrief-template.md) before starting.

If prompted to audit the project as a whole, check project-wide code coverage and mutation scores, and recommend areas for more detailed audits or for adding/updating tests. Bias recommendations towards the most important and bug-prone areas of the codebase - core business logic, event-driven code, and complex functions.

If prompted to audit a part of the project, look for modules or functions (within the scope of the prompt) that don't have tests and report these to the user in the post-audit debrief.

For each module within scope of the prompt that has tests, follow [assessing-a-module.md](assessing-a-module.md). Then, if any test criteria are still unmet after the assessment fixes, follow [writing-tests.md](writing-tests.md) to fill the remaining gaps.
