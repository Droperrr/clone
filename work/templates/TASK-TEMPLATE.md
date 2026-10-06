# TASK-XXX — <название>

Status: PROPOSED
Change Class: A (см. governance/CHANGE-CONTROL.md)

## Goal

Что должно измениться в системе.

## Why

Бизнесовая или техническая причина.

## Context

Минимальный контекст и ссылки на Project Memory.

## Requirements

- REQ-...
- ...

## Constraints

- ...

## Scope

Что входит в задачу.

## Out of scope

Что сознательно не входит.

## Dependencies

- ...

## Change classification

Class: A | B | C | D (см. governance/CHANGE-CONTROL.md)
Reason: <почему этот класс>

## Acceptance criteria

1. Given ... When ... Then ...
2. ...

## Code quality acceptance

Для задач, изменяющих код:

- [ ] существующие аналогичные механизмы проверены до создания новой логики;
- [ ] необоснованное дублирование отсутствует;
- [ ] dead/unreachable code не добавлен;
- [ ] новая сложность минимально достаточна и обоснована;
- [ ] новые абстракции имеют реальную ответственность и используются;
- [ ] существующие module boundaries не нарушены;
- [ ] не добавлены необоснованные зависимости;
- [ ] технический долг, если он неизбежен, явно зафиксирован.

## Required verification

- функциональные тесты;
- негативные сценарии;
- lint/typecheck/build, если применимо;
- codebase search на существующие аналоги;
- проверка duplication/dead code/complexity в изменённой области;
- ...

## Expected memory changes

- facts: ...
- architecture: ...
- decisions: ...
- discovery: ...
- lessons: ...
- governance: ...

## Risks / open questions

- ...

---

## Executor Report

После IMPLEMENTED исполнитель сохраняет durable отчёт:
`work/evidence/TASK-XXX/EXECUTOR-REPORT.md`

Шаблон: `work/templates/EXECUTOR-REPORT-TEMPLATE.md`

Краткая версия (для чата):

```text
TASK: TASK-XXX
STATUS: IMPLEMENTED
COMMITS:
- <sha> <message>

CHANGED:
- ...

VERIFIED:
- ...

CODE QUALITY:
- Reuse search: ...
- Duplication: ...
- Dead code: ...
- Complexity: ...
- New abstractions: ...

NOT VERIFIED:
- ...

KNOWN RISKS:
- ...

MEMORY:
- ...
```

---

## Architect Audit

После аудита архитектор сохраняет durable audit:
`work/evidence/TASK-XXX/ARCHITECT-AUDIT.md`

Шаблон: `work/templates/ARCHITECT-AUDIT-TEMPLATE.md`

Краткая версия (для чата):

```text
AUDIT: TASK-XXX
COMMIT(S): <sha>
VERDICT: ACCEPTED | CHANGES_REQUIRED | BLOCKED | REJECTED

CHECKED:
- Functional correctness
- Architecture
- Code quality
- Production concerns, if applicable

CODE QUALITY:
- Duplication: ...
- Dead code: ...
- Complexity: ...
- Abstractions/coupling: ...
- Technical debt: ...

FINDINGS:
- ...

MEMORY UPDATED:
- ...
```
