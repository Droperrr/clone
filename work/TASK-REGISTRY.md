# TASK-REGISTRY

> **Role:** Convenience index of all project tasks. Authoritative task state is in the
> task file itself (Status field), not in this registry. This registry is a catalog
> for quick overview and must not become a second source of truth.
>
> **Update rule:** Architect updates registry when creating, changing status,
> or completing a task. Executor may update only for IN_PROGRESS → IMPLEMENTED.
> Registry can be regenerated from `work/active/` and `work/evidence/` at any time.

---

## Active Tasks

*Tasks in `work/active/` requiring action from executor or architect.*

| Task ID | Name | Status | File | Last Updated |
|---------|------|--------|------|---------------|
| — | — | — | — | — |

## Completed Tasks

*Tasks in `work/evidence/` with final status (ACCEPTED or REJECTED).*

| Task ID | Name | Status | Location | Last Updated |
|---------|------|--------|----------|---------------|
| — | — | — | — | — |