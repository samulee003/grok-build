# Ark Agent Plan workflow

Volcengine Ark Agent Plan's sole role in this workflow is to supply the model
API key/credentials used for inference. Ark does **not** own product
direction, planning, staging, or acceptance -- those responsibilities stay
local, handled by Grok Build and its own project agents. Do not send
credentials, unrelated files, or tool output to Ark beyond what is required to
obtain or refresh the API key.

## Task contract

Before changing files, identify:

- objective and measurable acceptance criteria;
- allowed repository areas and required artifacts;
- verification commands;
- dependencies and risks; and
- conditions that require pausing to re-scope the plan locally.

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

Use the project agents in that order unless a local plan update specifies a
different dependency order. Keep local permission prompts and sandbox
boundaries enabled at all times; Ark's role as an API key provider never
grants it authority to bypass them.
