# Ark Agent Plan workflow

When a task is supplied by Volcengine Ark Agent Plan, treat Ark as the
planning and acceptance coordinator and Grok Build as the local execution
agent. Do not send credentials, unrelated files, or tool output to the remote
planner.

## Task contract

Before changing files, identify:

- objective and measurable acceptance criteria;
- allowed repository areas and required artifacts;
- verification commands;
- dependencies and risks; and
- conditions that require returning to Ark for replanning.

Keep each execution stage small and reversible. Do not expand the scope
without an explicit plan update.

## Completion report

Every completed stage must report:

1. completed work;
2. modified files;
3. verification commands and results;
4. unresolved issues or risks; and
5. whether the next stage may begin.

Never mark a stage complete when its required build or test checks failed.

## Agent responsibilities

- `ark-architect` researches the repository and proposes a stage plan.
- `ark-implementer` changes only the approved files and runs focused checks.
- `ark-verifier` runs the existing checks and reports evidence without editing.
- `ark-reviewer` performs a read-only quality, compatibility, and security review.

Use the project agents in that order unless the Ark plan specifies a different
dependency order. Keep local permission prompts and sandbox boundaries enabled;
the remote planner must never be treated as an authority to bypass them.
