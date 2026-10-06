# Architect Audit Template

Save as `work/evidence/TASK-XXX/ARCHITECT-AUDIT.md` when architect completes audit.

```text
# ARCHITECT AUDIT — TASK-XXX

Task: TASK-XXX — <task name>
Date: YYYY-MM-DD

## Verdict

ACCEPTED | CHANGES_REQUIRED | BLOCKED | REJECTED

## Commits Audited

- <sha> <message>

## Checked

### Functional correctness
- <acceptance criteria met / not met>
- <error handling>
- <idempotency / retry behavior>

### Architecture
- <ADR compliance>
- <source of truth / ownership>
- <contract boundaries>
- <existing consumers not broken>

### Code quality
- Duplication: <found / acceptable / requires fix>
- Dead code: <found / none>
- Complexity: <acceptable / excessive with rationale>
- Abstractions/coupling: <appropriate / issues noted>
- Technical debt: <none / explicitly recorded>

### Production concerns (if applicable)
- <data integrity / transactions>
- <security / auth>
- <migrations / deployment>
- <observability / error visibility>

## Findings

- [CRITICAL] <description> — <location>
- [HIGH] <description> — <location>
- [MEDIUM] <description> — <location>
- [LOW] <description> — <location>

## Code Quality Summary

- Duplication: ...
- Dead code: ...
- Complexity: ...
- Abstractions/coupling: ...
- Technical debt: ...

## Memory Updated

- <files updated or why not required>

## Next Action

- <if CHANGES_REQUIRED: what exactly to fix, priority order>
- <if ACCEPTED: task closed, next controlled step>
- <if REJECTED: rationale, alternative approach if known>
```