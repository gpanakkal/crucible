# Test Debriefs

Format debriefs per the template below. If there is nothing to report in a function subsection, simply write "n/a". Output the debrief into a Markdown file in `debriefs/`.

# Debrief: {moduleName/fileName}

## Summary

**Coverage** (branch)
Before: X% → After: Y%
Lines that could not be covered: {line ranges}

**Mutation score** (total)
Before: X% → After: Y%

### Issues

{bullet list of faulty assumptions, bugs found, issues found in tests, and failing tests. Each list item should begin with the project-root relative path to the file and line number(s) where the issue was found}

## {functionName}

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
