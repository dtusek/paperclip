# Codex workflow — Paperclip

## Default: LOW token mode
- Start from the named file, symbol, feature, error, or command. Do not scan the repository or preload product documentation.
- Use targeted search (`rg`, exact paths) and read only files required for the current task.
- Read `doc/SPEC-implementation.md` only when behavior/product-contract interpretation is required. Read `doc/GOAL.md`, `doc/PRODUCT.md`, `doc/DEVELOPING.md`, `doc/DATABASE.md`, or long-horizon `doc/SPEC.md` only when the task specifically depends on them.
- Avoid recursive reads of docs, examples, fixtures, generated assets, build output, logs, archives, snapshots, vendored code, and dependency trees.
- Do not invoke sub-agents or broad research unless explicitly requested or clearly necessary.
- Prefer one implementation pass plus targeted verification. Do not repeatedly re-read unchanged files.
- Keep plans, command output, diffs, progress notes, and final summaries concise.

## Modes
- `LOW` is default for normal fixes and small features.
- `NORMAL` may inspect directly related modules, contracts, and tests.
- `DEEP` may scan architecture, broad docs, or run full validation only when explicitly requested or genuinely repository-wide.

## Core invariants
- Keep every domain entity company-scoped and enforce company boundaries.
- For schema/API contract changes, synchronize affected DB schema/exports, shared types/validators/constants, server routes/services, and UI clients/pages.
- Preserve single-assignee tasks, atomic issue checkout, approval gates, budget hard-stop auto-pause, and activity logging for mutations.
- Do not replace strategic docs wholesale unless requested.
- Database changes use `packages/db/src/schema/*`, exported through its index, with migrations generated via `pnpm db:generate` when required.
- Agent bearer keys must never cross company boundaries.

## Verification
Run the smallest relevant test first. `pnpm test` is the normal cheap default when a broader unit-test pass is warranted. Run `pnpm test:e2e`, release smoke, full typecheck, full test run, or full build only when the changed surface requires it or the user explicitly requests full validation.

## Git/PR safety
- Before edits, check `git status -sb`; inspect only relevant diffs. Never overwrite unrelated work or use destructive git commands without explicit approval.
- Preserve upstream/fork conventions and avoid unrelated refactors.
- If creating a PR, use `.github/PULL_REQUEST_TEMPLATE.md`; read it at PR-creation time, not during ordinary coding tasks.

## Completion
Report only: what changed, files changed, checks run, and real remaining risks.