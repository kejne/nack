# Repository Guidelines

## Issue Tracking (Beads)
This repository uses **beads** (`bd`) as the source of truth for issues and work tracking.

- Use `bd` for all tasks; do **not** create Markdown files like `TODO.md`, `NOTES.md`, or ad-hoc checklists to track work.
- Create/claim work with `bd create`, `bd ready`, `bd update <id> --status in_progress`, and close with `bd close`.
- The repo is already onboarded when `.beads/` exists (otherwise run `bd quickstart` or `bd init`).

## Project Structure
- `cmd/`: Entry points for binaries (controllers and helpers).
- `controllers/`, `internal/controller/`: Controller logic and shared reconciliation code.
- `pkg/`: Reusable libraries (JetStream APIs, reloader, boot config, codegen helpers).
- `config/`, `deploy/`: CRDs and Kubernetes manifests (RBAC, examples).
- `tests/`: KUTTL e2e test assets and scenarios.

## Build, Test, and Development Commands
```bash
make build        # build all binaries
make test         # go vet + go test (envtest, -race, -cover)
make test-e2e      # KUTTL end-to-end tests (requires kubectl-kuttl)
make generate      # regenerate Kubernetes client/codegen output
```

## Development Process (TDD Required)
All development must be done using **TDD**:
1) Write a failing test that captures the behavior/bug.
2) Implement the minimal change to make it pass.
3) Refactor with tests staying green.

Prefer `make test` while iterating; add/adjust tests alongside production changes.

## Coding Style & Naming
- Go formatting: `gofmt` (`go fmt ./...`).
- Keep controller-specific code in `controllers/`/`internal/`; keep reusable code in `pkg/`.

## Commits & Pull Requests
- Commit subjects are short and imperative; common prefixes include `fix:`, `add:`, and `bump:`.
- PRs should link relevant `bd` issues, describe behavior changes, and include test updates.

## Session Completion (Required)
Before ending a session: file follow-up `bd` issues, run quality gates (at least `make test` for code changes), then `git pull --rebase`, `bd sync`, `git push`, and confirm `git status` is up to date.
