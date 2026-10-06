# PROJECT-STATE — Current Project State

Last verified: YYYY-MM-DD
Project phase: <Discovery | Implementation | Production>
State confidence: CONFIRMED where explicitly marked below; unresolved items remain OPEN.

> This file is an operational snapshot, not a replacement for detailed Project Memory.
> It points the architect toward authoritative documents.

## 1. Product

<Brief: what the product is, its purpose, and what the planned system includes.>

## 2. Systems and responsibility boundaries

### <System 1>
- <responsibility>;
- <responsibility>.

### <System 2>
- <responsibility>.

## 3. Current architecture

<Key architectural principles and boundaries. What is deliberately separated.>

## 4. Confirmed architectural decisions

- ADR-001 — <summary>;
- ...

See decisions/README.md and individual ADRs for authoritative reasoning and consequences.

## 5. Important confirmed constraints / lessons

- <constraint 1>;
- <constraint 2>.

## 6. Open questions / blockers

- <question 1>;
- <question 2>.

Authoritative list: discovery/open-questions.md.

## 7. Work state

### Active tasks

| Task ID | Name | Status |
|---------|------|--------|
| — | — | — |

Full task index: `work/TASK-REGISTRY.md`. Active task files: `work/active/`.

### Completed tasks

| Task ID | Name | Status | Location |
|---------|------|--------|----------|
| — | — | — | — |

### Milestones

<Current milestone state, last accepted milestone, key accomplishments.>

## 8. Governance already established

The project has an operating governance layer covering architect/executor roles,
task lifecycle, independent architect audit, code-quality gate, architecture change
control, Project Memory rules, task template and audit evidence.

These rules live in `governance/` and are part of the project contract.

## 9. Next controlled step

1. <step 1>;
2. <step 2>.

## 10. Memory integrity

After every substantial accepted task, the architect must verify this snapshot and
update it if project phase, architecture, decisions, constraints, risks, work state,
or next step changed.

This snapshot must never silently turn hypotheses or open questions into facts.