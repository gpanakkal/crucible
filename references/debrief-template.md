# Test Debriefs

Record the outcome of every test writing/fixing/auditing pass in a debrief.

## Where and how to write the debrief

- **Standalone**: output the debrief into a Markdown file in `debriefs/`, formatted per the template below.
- **Embedded in another workflow**: if the enclosing workflow specifies how, when, and where to write reports or debriefs, follow those instructions for the output file and the general format. However, always write the Summary section exactly as templated below, placed under the relevant subheading of the workflow's report (if any), adjusting heading depth to fit the surrounding document. If the debrief will be written into a file with other contents, title the section "Crucible Summary" instead of "Summary".

If there is nothing to report in a subsection or issue category, simply write "n/a".

## Debrief: {moduleName/fileName} {yyyy-mm-dd}

### Summary

**Coverage** (branch)
Before: X% → After: Y%
Lines that could not be covered: {line ranges}

**Mutation score** (total)
Before: X% → After: Y%

#### Issues

{Use a sub-heading for each of the following categories: functions with unclear purposes (i.e., purposes you did not have high confidence in), faulty assumptions, bugs found, issues found in tests, and failing tests. Under each sub-heading, bullet-list the issues found, or write "n/a" if there are none. Each list item should begin with the project-root relative path to the file and line number(s) where the issue was found.}

---

### {functionName}

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
