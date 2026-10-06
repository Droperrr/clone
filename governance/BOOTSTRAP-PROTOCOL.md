# Project Operating System — Architect Bootstrap Protocol

## Purpose

This protocol defines how a fresh architect context reconstructs the project before making architectural decisions or assigning implementation work.

The goal is that loss of ChatGPT context must not cause loss of project context.

## Core rule

The repository is the durable project memory. The chat is a working session, not the source of truth.

A fresh architect must not rely on remembered chat context when required information can be recovered from Git.

## Bootstrap sequence

Read in this order:
1. README.md
2. governance/CHATGPT-PROJECT-INSTRUCTIONS.md
3. governance/PROJECT-OPERATING-PROTOCOL.md
4. governance/MEMORY-PROTOCOL.md
5. PROJECT-STATE.md
6. facts/project-context.md
7. facts/current-state.md
8. relevant requirements/
9. relevant architecture/
10. decisions/README.md and all relevant ADRs
11. discovery/open-questions.md
12. lessons/lessons-learned.md
13. work/README.md
14. work/TASK-REGISTRY.md
15. all files in work/active/, when present
16. relevant work/evidence/ for accepted milestones, when present
17. relevant implementation code only after the project model is understood

Do not blindly read every historical document if current state and indexes identify the relevant subset. The objective is reconstruction of the current model, not indiscriminate context loading.

## Reconstruction check

After bootstrap, the architect must be able to state from repository evidence:
- what the product is;
- what systems participate;
- what has already been implemented;
- what the current architecture is;
- which decisions are authoritative;
- what requirements are binding;
- what is confirmed versus hypothesized;
- which questions remain open;
- which tasks are active and their lifecycle state;
- what the last accepted changes were;
- what the next controlled step is.

If any item cannot be reconstructed reliably, the architect must not guess. It must inspect the relevant repository documents/code or mark the information OPEN.

## Project State

PROJECT-STATE.md is the operational snapshot of the project.

It is intentionally concise and must not duplicate detailed architecture or requirements. It points the architect toward authoritative documents.

Update it when a substantial change affects project phase, implementation state, architecture, important decisions, critical constraints, blockers, active work, accepted milestones, or the next controlled step.

## Task reconstruction

If `work/active/` contains tasks, inspect them before proposing new work.
Also check `work/TASK-REGISTRY.md` for an overview of all tasks (active + finalized).

IMPLEMENTED is not accepted until independently audited.

If a task is AUDIT or CHANGES_REQUIRED, resolve that state before treating the work
as complete.

For finalized tasks, `work/evidence/TASK-XXX/` contains the durable artifacts:
task file, EXECUTOR-REPORT.md, ARCHITECT-AUDIT.md.

## Conflict handling

If repository documents disagree:
1. do not guess;
2. identify the conflicting statements;
3. determine whether the conflict is stale knowledge, implementation defect, requirement change, or a new architectural question;
4. apply the Project Operating Protocol and Memory Protocol;
5. update affected documents while preserving causal history.

Code does not automatically override architecture, and an old document does not override a newer confirmed decision merely because it is in a different directory.

## Memory completeness check

At the end of every substantial architect session, ask:

Did this session create durable knowledge that the next architect would need?

If yes, record it in the appropriate memory category before considering the session complete.

Relevant categories: FACT, REQUIREMENT, DECISION, HYPOTHESIS, OPEN QUESTION, LESSON, architecture/integration constraint, task/audit evidence.

## Fresh-context acceptance test

A fresh architect context passes bootstrap only when it can produce a short project handoff containing:
1. current project state;
2. current architecture;
3. authoritative decisions;
4. open blockers;
5. active work;
6. last accepted milestone;
7. next action.

The handoff must cite repository paths as evidence.

## Important limitation

No memory protocol can guarantee that every transient thought from a chat is preserved. The unit that must survive context changes is durable knowledge.

If something matters for future decisions, it must be promoted from chat into Project Memory.