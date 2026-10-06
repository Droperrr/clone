# Work Management

Этот каталог хранит состояние инженерной работы: задачи, их lifecycle и evidence аудита.

## Статусы

`PROPOSED → READY → IN_PROGRESS → IMPLEMENTED → AUDIT → ACCEPTED`

При необходимости:

`AUDIT → CHANGES_REQUIRED → IN_PROGRESS`

или `BLOCKED` при внешней зависимости.

Полная таблица переходов: `governance/TASK-PROTOCOL.md` §8.

## Правила

- `IMPLEMENTED` не означает принятую работу.
- Только архитектор переводит задачу в `ACCEPTED` после независимого аудита.
- Task ID используется в коммуникации и commit message.
- Завершённая существенная задача должна иметь audit evidence:
  `EXECUTOR-REPORT.md` (от исполнителя) и `ARCHITECT-AUDIT.md` (от архитектора).
- Если задача изменила понимание проекта, Project Memory обновляется до её принятия.
- Статус задачи в репозитории является authoritative. Статус только в чате — не authoritative.

## Структура

```
work/
├── TASK-REGISTRY.md              # Индекс всех задач (active + evidence)
├── active/                       # Задачи, требующие действия
│   └── TASK-XXX-<slug>.md       #   (PROPOSED → AUDIT, CHANGES_REQUIRED, BLOCKED)
├── evidence/                     # Durable evidence (создаётся при IMPLEMENTED)
│   └── TASK-XXX/
│       ├── TASK-XXX.md           #   Task definition (после ACCEPTED/REJECTED)
│       ├── EXECUTOR-REPORT.md    #   Durable executor report
│       └── ARCHITECT-AUDIT.md    #   Durable architect audit
└── templates/                    # Шаблоны рабочих документов
    ├── TASK-TEMPLATE.md
    ├── EXECUTOR-REPORT-TEMPLATE.md
    └── ARCHITECT-AUDIT-TEMPLATE.md
```

### TASK-REGISTRY.md

Индекс-каталог всех задач. **Не является вторым source of truth.**
Authoritative state задачи — Status field в task-файле.
Registry обновляется при изменении статуса; при расхождении — корректируется по task-файлу.

### active/

Задачи, требующие действия от исполнителя или архитектора.
Файл остаётся здесь пока задача не достигнет ACCEPTED или REJECTED.

### evidence/

Durable evidence directory. Создаётся при IMPLEMENTED (executor report) и пополняется
при AUDIT (architect audit). После ACCEPTED/REJECTED сюда перемещается task-файл.

**Важно:** наличие evidence в этом каталоге НЕ означает, что задача ACCEPTED.
CHANGES_REQUIRED задача имеет ARCHITECT-AUDIT.md в `evidence/`, но task-файл
остаётся в `active/`. Authoritative статус — в task-файле.
