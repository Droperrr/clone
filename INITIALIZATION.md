# Project Initialization Procedure

This document defines how to take this Project Operating System repository and initialize a completely new project.

## Prerequisites

- A new or existing GitHub repository for the project.
- Project name and brief description.
- Initial understanding of: product purpose, participating systems, key constraints.

## Procedure

### 1. Clone / copy the Operating System

**Step 1a — Clone:**

```bash
git clone <this-repo-url> <new-project-dir>
cd <new-project-dir>
```

**Step 1b — Remove old Git history and create a fresh repository:**

Delete the entire `.git` directory of the cloned template, then initialize
a new independent Git repository. The old remote, history, and refs are
completely removed.

| Platform | Command |
|----------|---------|
| Linux / macOS | `rm -rf .git` |
| Windows PowerShell | `Remove-Item -Recurse -Force .git` |
| Windows CMD | `rmdir /s /q .git` |

Then, on all platforms:

```bash
git init
git add -A
git commit -m "Initial: project setup"
git branch -M main
```

> ⚠️ **Safety:** Run the delete command only inside the newly cloned directory
> (`<new-project-dir>`). Double-check with `pwd` before deleting.

**Step 1c — Verify clean state:**

```bash
# No old remote should remain:
git remote -v
# Expected output: (empty)

# Only the new initial commit exists:
git log --oneline
# Expected output: <sha> Initial: project setup
```

**Step 1d — Connect to new remote:**

```bash
git remote add origin <new-project-repo-url>
git push -u origin main
```

> ⚠️ Replace `<this-repo-url>` with the actual clone repository URL.
> Replace `<new-project-repo-url>` with the new project's GitHub repository URL.
>
> If `git push` fails because the new remote repository is empty, use:
> `git push -u origin main` (the first push creates the branch on the remote).

### 2. Establish Project Identity

Replace the following in the repository:

| File | What to set |
|------|-------------|
| `README.md` | Replace with project-specific README describing product, systems, and quick navigation to governance/state. |
| `governance/CHATGPT-PROJECT-INSTRUCTIONS.md` | Replace `<PROJECT_REPO_URL>` with actual repository URL. Update the first sentence with project context if desired. |
| `PROJECT-STATE.md` | Fill all `<...>` placeholders: product, systems, architecture, constraints, open questions, work state, next step. Update "Last verified" date. |

### 3. Initialize Project Memory

Create initial Project Memory files. Minimum:

```
facts/
├── project-context.md     # What the project is, systems, participants, known current process
├── current-state.md       # Current state of external systems, integrations, constraints
└── terminology.md         # Project-specific terms and definitions

requirements/
└── <initial-requirements>.md   # Client requirements, TЗ, API requirements

architecture/
└── <system-context>.md         # System context diagram, boundaries, integration model

decisions/
├── README.md              # Decision log index
└── ADR-001-<topic>.md     # First architectural decision

discovery/
├── open-questions.md      # Unresolved questions blocking implementation
└── decision-history.md    # Key reasoning chains

lessons/
└── lessons-learned.md     # Sustained conclusions that affect future work
```

### 4. Initialize Work / Task Structures

- `work/active/` — empty; first task will be created here.
- `work/evidence/` — empty; will accumulate durable evidence artifacts.
- `work/TASK-REGISTRY.md` — already initialized (empty tables).

### 5. Initialize Project Instructions

Set the contents of `governance/CHATGPT-PROJECT-INSTRUCTIONS.md` as the ChatGPT Project Instructions field (or equivalent for other AI tools).

### 6. Verify Bootstrap / Recovery

Simulate a fresh architect context:

1. Clone the repository into a temporary directory.
2. Follow `governance/BOOTSTRAP-PROTOCOL.md` without relying on chat context.
3. Verify you can state:
   - what the product is;
   - what systems participate;
   - what the current architecture is;
   - which decisions are authoritative;
   - what questions remain open;
   - which tasks are active;
   - what the next controlled step is.
4. If any item cannot be reconstructed, fix the corresponding Project Memory document.

### 7. Create the First Task

1. Architect formulates the first task in chat.
2. Architect creates `work/active/TASK-XXX-<slug>.md` using `work/templates/TASK-TEMPLATE.md`.
3. Task status: PROPOSED.
4. Architect verifies: context sufficient, dependencies resolved, acceptance criteria clear.
5. Architect transitions to READY (updates Status in task file).
6. Architect records task in `work/TASK-REGISTRY.md`.
7. Architect updates `PROJECT-STATE.md` §7 (Work state) to reflect the new active task.
8. Task is now ready for executor.

## Mandatory vs Optional Components

### Mandatory for every project

| Component | Rationale |
|-----------|----------|
| `governance/` (all files) | Operating protocol — required for architect/executor workflow |
| `PROJECT-STATE.md` | Operational snapshot — required for bootstrap/recovery |
| `work/README.md` | Work management rules |
| `work/templates/` (all) | Task, executor report, architect audit templates |
| `work/TASK-REGISTRY.md` | Task index |
| `work/active/` + `work/evidence/` | Task lifecycle directories |
| `facts/project-context.md` | Project identity and context |
| `facts/current-state.md` | External system state |
| `decisions/README.md` | Decision log index |
| `discovery/open-questions.md` | Open questions registry |
| `lessons/lessons-learned.md` | Lessons log |

### Optional / Conditional

| Component | When needed |
|-----------|-------------|
| `requirements/` | When client/external requirements documents exist |
| `architecture/` files beyond system-context | When architectural complexity warrants separate documents |
| Additional ADRs | Per architectural decision (create when decision is made) |
| `discovery/decision-history.md` | When key reasoning chains need preservation |
| `facts/terminology.md` | When project has domain-specific terminology |
| `facts/technical-context.md` | When technical environment details are material |
| `legal/` | When legal/contractual documents need tracking |
| `.gitignore` | When application code is added |
| `facts/business-process.md` | When business process modeling is needed |

### Chat-to-Task-File Rule

A substantial task must never exist only in chat when execution begins.

The sequence is:

```
Chat proposal → Architect approval → Authoritative task file in work/active/ → READY → Executor
```

Do not create hidden task files before approval.
Do not consider a chat message as authoritative task status.
The repository is the durable source of truth for task state.