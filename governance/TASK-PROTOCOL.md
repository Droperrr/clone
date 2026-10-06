# Task Protocol

## 1. Task ID

Каждая существенная инженерная задача получает уникальный ID:

`TASK-XXX`

ID используется в коммуникации, task-документе, commit message и audit record.

## 2. Обязательная структура задачи

```text
# TASK-XXX — <название>

Status: PROPOSED | READY | IN_PROGRESS | IMPLEMENTED | AUDIT | CHANGES_REQUIRED | BLOCKED | ACCEPTED | REJECTED

## Goal

## Why

## Context

## Requirements

## Constraints

## Scope

## Out of scope

## Dependencies

## Acceptance criteria

## Required verification

## Expected memory changes

## Risks / open questions
```

## 3. Хорошая задача

Хорошая задача описывает результат, а не микроменеджмент реализации.

Плохая постановка:

> Добавь функцию X в файл Y.

Хорошая постановка:

> Обеспечь идемпотентное создание заказа после успешной оплаты, не создавая дубликат при повторном webhook. Внешняя система остаётся источником истины по подтверждённому заказу. Добавь тесты повторной доставки webhook и ошибки внешнего API.

Конкретная реализация может быть оставлена исполнителю, если архитектурные границы определены.

## 4. Acceptance criteria

Критерии должны быть наблюдаемыми и проверяемыми.

Использовать формулировки:

- Given / When / Then;
- конкретный ожидаемый результат;
- конкретный инвариант;
- конкретная команда проверки.

Избегать критериев вроде «работает корректно» без определения корректности.

## 5. Scope control

Если в процессе обнаружена полезная, но несвязанная проблема, она не должна автоматически раздувать текущую задачу.

Исполнитель сообщает о ней архитектору. Архитектор решает, добавить ли её в текущую задачу или создать отдельную.

## 6. Статусы

### PROPOSED

Задача сформулирована, но ещё не готова к исполнению.

### READY

Задача имеет достаточный контекст и критерии для исполнения.

### IN_PROGRESS

Исполнитель работает.

### IMPLEMENTED

Исполнитель завершил реализацию и отправил отчёт.

### AUDIT

Архитектор выполняет независимую проверку.

### CHANGES_REQUIRED

Обнаружены проблемы, требующие доработки.

### BLOCKED

Работа остановлена внешней зависимостью или нерешённым вопросом.

### ACCEPTED

Работа прошла архитектурный аудит.

### REJECTED

Подход признан неприемлемым и не должен продолжаться в текущем виде.

## 7. Task completion

Задача считается завершённой только в `ACCEPTED`.

`IMPLEMENTED` — промежуточное состояние.

## 8. Lifecycle Transition Ownership

Каждый переход статуса имеет однозначного владельца. Статус, существующий только
в чате, не является authoritative состоянием задачи. Репозиторий — durable source
of truth. Статус должен быть обновлён в task-файле в репозитории **до** или
**одновременно** с коммуникацией изменения.

### Основной поток

| Transition | Owner | Required Artifact | Location | Condition |
|-----------|-------|-------------------|----------|----------|
| → PROPOSED | Architect | Task file created | `work/active/TASK-XXX.md` | Task formulated with Goal, Context, Criteria |
| PROPOSED → READY | Architect | Status updated in task file | `work/active/TASK-XXX.md` (Status field) | Context sufficient, dependencies resolved, criteria clear |
| READY → IN_PROGRESS | Executor | Status updated in task file | `work/active/TASK-XXX.md` (Status field) | Task understood, repo checked, no blocking ambiguities |
| IN_PROGRESS → IMPLEMENTED | Executor | Task file + EXECUTOR-REPORT.md | `work/active/TASK-XXX.md` + `work/evidence/TASK-XXX/EXECUTOR-REPORT.md` | Self-verification passed, commits pushed |
| IMPLEMENTED → AUDIT | Architect | Status updated in task file | `work/active/TASK-XXX.md` (Status field) | Architect begins independent verification |
| AUDIT → ACCEPTED | Architect | ARCHITECT-AUDIT.md + task file moved | `work/evidence/TASK-XXX/` | All acceptance criteria met, quality gate passed |

### Ветки

| Transition | Owner | Required Artifact | Location | Condition |
|-----------|-------|-------------------|----------|----------|
| AUDIT → CHANGES_REQUIRED | Architect | ARCHITECT-AUDIT.md with findings | `work/evidence/TASK-XXX/ARCHITECT-AUDIT.md` | Specific defects found; task stays in `work/active/` |
| CHANGES_REQUIRED → IN_PROGRESS | Executor | Status updated in task file | `work/active/TASK-XXX.md` (Status field) | Executor resumes work per findings |
| AUDIT → REJECTED | Architect | ARCHITECT-AUDIT.md + task file moved | `work/evidence/TASK-XXX/` | Approach fundamentally incompatible |
| → BLOCKED (from READY, IN_PROGRESS) | Discoverer | Status + blocker reason in task file | `work/active/TASK-XXX.md` (Status field + blocker note) | External dependency / unresolved question |
| BLOCKED → READY | Architect | Status updated + blocker resolved note | `work/active/TASK-XXX.md` (Status field) | Blocker resolved |
| BLOCKED → IN_PROGRESS | Executor | Status updated | `work/active/TASK-XXX.md` (Status field) | Blocker resolved, executor resumes |

### Правило расположения файлов

- `work/active/` — задачи, требующие действия: PROPOSED, READY, IN_PROGRESS, IMPLEMENTED, AUDIT, CHANGES_REQUIRED, BLOCKED.
- `work/evidence/TASK-XXX/` — директория создаётся при IMPLEMENTED (executor report) и пополняется при ACCEPTED/REJECTED (architect audit + task file).

При IMPLEMENTED executor создаёт `work/evidence/TASK-XXX/EXECUTOR-REPORT.md`.
Task file остаётся в `work/active/` до ACCEPTED или REJECTED.

При ACCEPTED/REJECTED architect:
1. Создаёт/дополняет `work/evidence/TASK-XXX/ARCHITECT-AUDIT.md`.
2. Перемещает task file из `work/active/` в `work/evidence/TASK-XXX/`.
3. Обновляет `work/TASK-REGISTRY.md`.
4. Проверяет и при необходимости обновляет `PROJECT-STATE.md`.

При CHANGES_REQUIRED:
1. Architect создаёт `work/evidence/TASK-XXX/ARCHITECT-AUDIT.md`.
2. Task file остаётся в `work/active/`.
3. Статус обновляется до CHANGES_REQUIRED.

## 9. Cross-Document Consistency

При каждом существенном переходе статуса (READY, IMPLEMENTED, ACCEPTED, REJECTED)
необходимо проверить согласованность:

- task-файл (Status field) ↔ `work/TASK-REGISTRY.md`;
- task-файл ↔ `PROJECT-STATE.md` §7 (Work state);
- `work/active/` ↔ `work/evidence/` (файл находится в правильном каталоге);
- executor report ↔ commits (commit SHA в отчёте соответствует push);
- architect audit ↔ commits (аудируемые commits зафиксированы).

`TASK-REGISTRY.md` является производным индексом. Authoritative state — task-файл.
При расхождении registry обновляется по task-файлу, а не наоборот.

## 10. Silent Lifecycle Changes Prohibited

Статус задачи, объявленный только в чате, не считается authoritative состоянием.

Если governance определяет репозиторий как durable source of truth, любой lifecycle
переход должен быть отражён в репозитории **до** или **одновременно** с коммуникацией
в чате.

Нельзя:
- объявить задачу READY в чате, не обновив task-файл;
- считать задачу ACCEPTED на основании устного одобрения;
- перевести задачу в IMPLEMENTED без durable executor report в репозитории;
- молча изменить статус без обновления TASK-REGISTRY и проверки PROJECT-STATE.
