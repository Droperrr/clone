# Project Operating System

Универсальная, переносимая операционная система для совместной работы архитектора
и исполнителя над коммерческими проектами. Не содержит application code, доменных
требований или архитектуры конкретного продукта.

## Что внутри

| Компонент | Назначение |
|-----------|-----------|
| `governance/` | Протоколы: bootstrap/recovery, роли, task lifecycle, memory, audit, change control |
| `work/` | Структура задач: шаблоны, active/evidence, task registry |
| `facts/` | Структура для Project Memory FACTs |
| `requirements/` | Структура для требований |
| `architecture/` | Структура для архитектурных документов |
| `decisions/` | Структура для ADR |
| `discovery/` | Структура для открытых вопросов и discovery |
| `lessons/` | Структура для lessons learned |
| `PROJECT-STATE.md` | Операционный snapshot проекта (шаблон) |
| `INITIALIZATION.md` | Процедура инициализации нового проекта |

## Что это НЕ

- ❌ Application template (нет кода, нет фреймворка, нет стека)
- ❌ CI/CD pipeline
- ❌ Project management tool
- ❌ Domain-specific framework

## Быстрый старт

1. Клонируй этот репозиторий как основу нового проекта.
2. Следуй `INITIALIZATION.md` — 7 шагов от клонирования до первой задачи.
3. Заполни project identity, PROJECT-STATE, и начальную Project Memory.
4. Создай первую задачу через формальный lifecycle: PROPOSED → READY → ...

## Ключевые принципы

- **Repo = durable source of truth.** Чат — временный канал.
- **IMPLEMENTED ≠ ACCEPTED.** Только независимый аудит архитектора подтверждает приёмку.
- **Durable evidence.** Executor reports и architect audits сохраняются в `work/evidence/`.
- **Project Memory.** FACT, REQUIREMENT, DECISION, HYPOTHESIS, OPEN QUESTION, LESSON — строго разделены.
- **Bootstrap/recovery.** Новый архитектор восстанавливает контекст из репозитория без чтения чатов.

## Идентичность

Операционная система различает несколько независимых слоёв идентичности:

| Слой | Где определяется | Пример |
|------|-----------------|--------|
| **Governance identity** | `governance/` | Правила работы архитектора и исполнителя |
| **Project identity** | `PROJECT-STATE.md`, `facts/project-context.md` | «Онлайн-бронирование инвентаря» |
| **Product identity** | `requirements/`, `architecture/` | Конкретный продукт и его архитектура |
| **Repository identity** | `README.md`, remote URL | GitHub repo проекта |
| **AI Instructions identity** | `governance/CHATGPT-PROJECT-INSTRUCTIONS.md` | Инструкции для ChatGPT/Claude/etc. |

При инициализации нового проекта заполняются все пять слоёв, начиная с project identity.

## Portability

Операционная система не зависит от:
- Конкретного GitHub аккаунта или организации;
- Конкретной ОС или VM;
- Внешнего chat-контекста;
- Конкретного домена или стека.

Единственные зависимости: Git, Markdown-совместимый просмотрщик, AI-ассистент (ChatGPT/Claude/etc.) для роли архитектора.

## Структура репозитория

```
.
├── README.md
├── PROJECT-STATE.md                  # Шаблон операционного snapshot
├── INITIALIZATION.md                 # Процедура инициализации нового проекта
├── governance/
│   ├── BOOTSTRAP-PROTOCOL.md         # Восстановление контекста
│   ├── PROJECT-OPERATING-PROTOCOL.md # Главный протокол
│   ├── MEMORY-PROTOCOL.md            # Правила Project Memory
│   ├── TASK-PROTOCOL.md              # Жизненный цикл задач
│   ├── EXECUTOR-WORKFLOW.md          # Протокол исполнителя
│   ├── ARCHITECT-WORKFLOW.md         # Протокол архитектора
│   ├── AUDIT-PROTOCOL.md             # Стандарт независимого аудита
│   ├── CHANGE-CONTROL.md             # Управление изменениями
│   └── CHATGPT-PROJECT-INSTRUCTIONS.md # Инструкции для AI-ассистента
├── work/
│   ├── README.md
│   ├── TASK-REGISTRY.md              # Индекс задач (derived)
│   ├── active/                       # Активные задачи
│   ├── evidence/                     # Durable evidence (executor reports, audits)
│   └── templates/
│       ├── TASK-TEMPLATE.md
│       ├── EXECUTOR-REPORT-TEMPLATE.md
│       └── ARCHITECT-AUDIT-TEMPLATE.md
├── facts/                            # Project Memory: FACT
├── requirements/                     # Project Memory: REQUIREMENT
├── architecture/                     # Project Memory: архитектура
├── decisions/                        # Project Memory: DECISION (ADR)
├── discovery/                        # Project Memory: OPEN QUESTION, discovery
└── lessons/                          # Project Memory: LESSON
```

## Provenance

Разработано как извлекаемая операционная система из production-проверенного governance.
Формализовано через полный цикл: независимый аудит → устранение разрывов → экстракция → харденинг.