# Change Control

## 1. Purpose

Проект коммерческий и интеграционно-зависимый. Изменения должны быть управляемыми и трассируемыми.

## 2. Classes of change

### Class A — Local implementation

Не меняет внешние контракты, source of truth или архитектурные границы.

Может выполняться в рамках обычной задачи.

### Class B — Contract change

Меняет API, schema, event, webhook, DB contract или поведение, от которого зависят другие компоненты.

Требует проверки всех consumers и explicit acceptance criteria.

### Class C — Architecture change

Меняет ownership, source of truth, системные границы, интеграционную модель или ключевой ADR.

Требует решения архитектора и фиксации ADR до принятия реализации.

### Class D — Business/legal change

Меняет бизнес-правила, договорные обязательства, обработку персональных данных, оплату, возвраты или иные коммерчески/юридически значимые правила.

Не должна быть внедрена исполнителем по собственной инициативе.

## 3. Backward compatibility

Перед Class B/C изменением нужно определить:

- кто использует текущий контракт;
- можно ли сохранить backward compatibility;
- нужен ли migration period;
- нужен ли rollback;
- как будет обнаружен частичный rollout.

## 4. Database changes

Для schema/migration changes необходимо проверить:

- совместимость приложения и схемы на переходном этапе;
- существующие данные;
- индексы и ограничения;
- rollback/recovery strategy;
- объём и время миграции для production объёма данных.

## 5. External integrations

Изменение поведения интеграции должно учитывать:

- timeout;
- retry;
- idempotency;
- rate limits;
- authentication;
- partial failure;
- versioning;
- внешний source of truth.

## 6. Emergency changes

Срочный production workaround допускается только как явно обозначенный временный шаг. После стабилизации он должен быть либо заменён нормальной реализацией, либо зарегистрирован как технический долг с владельцем и причиной.
