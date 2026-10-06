# Executor Report Template

Save as `work/evidence/TASK-XXX/EXECUTOR-REPORT.md` when task reaches IMPLEMENTED.

```text
# EXECUTOR REPORT — TASK-XXX

Task: TASK-XXX — <task name>
Status: IMPLEMENTED
Date: YYYY-MM-DD

## Commits

- <sha> <message>
- <sha> <message>

## Changed

- <what was changed — files, modules, components>
- <any related refactoring and why>

## Verified

- <command / check performed>
- <test results>
- <lint / typecheck / build status>

## Code Quality

- Reuse search: <existing mechanisms checked, reused or why not>
- Duplication: <no / accepted with rationale>
- Dead code: <none added / removed N unused symbols>
- Complexity: <minimal sufficient / justified complexity noted>
- New abstractions: <none / N, with responsibility>

## Not Verified

- <what could not be verified and why>

## Known Risks

- <known limitations, edge cases, assumptions>

## Memory

- <Project Memory files updated, or why not required>
```