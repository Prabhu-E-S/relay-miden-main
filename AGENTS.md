# Agent guide for hackathon projects

## Event requirements

- Read [RULES.md](RULES.md) before working. Build project implementation from scratch at the event; do not import a pre-built project.
- Libraries, APIs, and public datasets are allowed. Document their sources and use.
- Use Codex during development and briefly record its actual contribution in [AI_USAGE.md](AI_USAGE.md).
- Prepare a code repository, short project description, and working demo in [SUBMISSION.md](SUBMISSION.md).

## Use basic coding patterns

- Prefer straightforward, idiomatic code: small functions, clear names, simple data structures, and modules with one clear responsibility.
- Use the project's existing patterns. Add an abstraction only when an actual repeated need makes the code easier to understand.
- Choose the simplest implementation that meets the current requirement. Avoid unnecessary layers, generic frameworks, premature optimization, and speculative features.
- Keep dependencies few and purposeful. Reuse appropriate standard libraries and established libraries instead of reimplementing them.
- Validate inputs, handle errors explicitly, and show useful failure messages. Do not hide failures behind fabricated success or demo data.
- Keep changes focused. Explain the reason for non-obvious decisions in short comments or project documentation.

## Document every meaningful change

- Update [CHANGELOG.md](CHANGELOG.md) in the same commit as each meaningful change. Record the date and time with timezone, what changed, why, the affected files or feature, validation performed, and known limitations.
- Update [README.md](README.md) whenever setup, commands, environment requirements, project behavior, or demo instructions change.
- Update [AI_USAGE.md](AI_USAGE.md) whenever Codex or other AI assistants make a meaningful contribution. Record the task, assistance, human review status, checks, and any corrections. Brief summaries are enough; full chat transcripts are unnecessary.
- Keep claims accurate. Distinguish implemented and verified behavior from planned or incomplete work. Never invent test results, deployment success, AI usage, or commit timestamps.

## Make regular, timely commits (Developer responsibility)

1. Inspect `git status` before editing. Preserve teammates' work and identify files belonging to the current task.
2. Finish a small, coherent change, run appropriate checks, and update its documentation.
3. Review the diff and explicitly stage only the files for that change.
4. **Commit after each completed milestone. While actively building, aim for a commit about every 30 minutes when meaningful changes are ready.** Do not leave the entire night's work for one final commit.
5. Commit completed work before a handoff, a long break, or the end of a work session. If work is incomplete, document its state and use an honest `wip:` message for a useful checkpoint.
6. Use short, descriptive messages, such as `feat: add project search`, `fix: handle empty results`, or `docs: explain local demo setup`.
7. Do not create empty commits to satisfy the clock. Do not backdate commits, squash away the event development record, force-push, or rewrite shared history.
8. Push committed checkpoints to the team's repository regularly, when network access is available and the team has authorized that remote. Resolve conflicts with care.

The 30-minute target is this repository's working convention. It does not replace event rules or organizer instructions.

## Check work and protect credentials

- Use the project's actual install, run, lint, test, and build commands. Add them to the README as soon as they exist; this template does not prescribe a stack.
- Run checks appropriate to the change. For a documentation-only change, check links and consistency. For code changes, verify the changed behavior and any relevant existing tests.
- Report what ran and what passed, failed, or could not be checked. If a command fails, investigate or document the limitation before handoff.
- Keep credentials, API keys, approved QR codes, and private participant data out of commits and logs. Use environment variables and sanitized examples; never put live keys in `.env.example`.

## Before submission

- Complete [SUBMISSION.md](SUBMISSION.md), replacing all participant placeholders.
- Confirm the README gives reproducible setup and demo steps.
- Check that the working demo matches the submitted code and that known limitations are disclosed.
- Update the changelog and AI usage record, commit the final coherent change, and push it.
- Record the final submitted commit SHA in the submission details. Documentation may record that SHA in a subsequent commit; do not claim later implementation changes belong to the earlier demo.
- Follow the organizers' actual submission method and timing. The event wrap-up is by 10:00 AM IST on the final day.

---

## Relay Miden project policies

### Git policy for AI agents

**AI agents must not execute Git commands under any circumstances unless the developer explicitly changes this restriction.** This includes:

- `git status`, `git diff`, `git add`, `git commit`, `git push`, `git pull`, `git fetch`, `git branch`, `git checkout`, `git reset`, `git init`, `git log`, `git rev-parse`.
- Do not create commits, branches, tags, or pull requests.
- Do not modify Git remotes or repository history.
- Do not edit or touch the `.git` directory.

The developer is solely responsible for manually reviewing changes, running Git operations, creating meaningful commits, and pushing checkpoints. The organizer commit guidance above defines developer workflow expectations.

### Append-only execution history

Every AI development execution must create a new unique Markdown history file under `docs/history/`.

- File naming pattern: `phase-XX-YYYYMMDDTHHMMSSZ-unique.md`.
- For migration, maintenance, or audit work, use a descriptive prefix and unique timestamp (e.g., `template-migration-YYYYMMDDTHHMMSSZ-unique.md`).
- Use UTC timestamps with a unique random or hash suffix (e.g., `9c4b1e`, `a7f3c2`).
- Never overwrite, modify, reuse, or delete previous history entries.
- Every history file must include:
  - Objective / Prompt
  - Timestamp
  - Agent / tool used
  - Files created
  - Files modified
  - Implementation details
  - Commands executed
  - Actual validation results
  - Known limitations
  - Next steps

### README updates

Update [README.md](README.md) whenever project behavior, setup, dependencies, architecture, or implementation status changes. Maintain accurate links to all history entries and documentation.

### Design preservation

The Phase 1 visual interface has been approved and must be strictly preserved:

- Centralized brand palette:
  - `--color-primary`: `#004225` (forest green)
  - `--color-background`: `#F5F5DC` (beige / cream)
  - `--color-action`: `#FFB000` (amber)
  - `--color-accent`: `#FFCF9D` (peach)
- Brand colors must remain centralized in `apps/web/src/styles/palette.css`.
- Priority indicators must remain colored text without colored background pills.
- Dashboard metric icons must not have colored background boxes.
- Preserve desktop dashboard, fixed sidebar, mobile header and bottom navigation, task cards, typography, and responsive layouts.
- Do not introduce gradients, glassmorphism, or decorative elements.

### Phase scope discipline

Implement only the currently authorized phase. Do not implement future phases without explicit user instruction:

- Phase 1 (Setup, Design System, Responsive UI) is implemented and verified.
- Phase 2 (Offline Task Management Engine) is implemented and verified.
- Phase 3 (PaperBridge QR Protocol) and subsequent phases (4 through 10) are planned and must not be implemented until authorized.

### Backend independence and offline integrity

Phase 2 task management is strictly offline:

- All task CRUD, queries, live counters, filters, and device identity are stored in browser IndexedDB via Dexie.js (`relay-miden-db`).
- The Express server provides only a `/health` endpoint (`GET /health` -> `{ "status": "ok", "service": "relay-miden-server", "phase": 2 }`).
- Do not add task endpoints to the backend or route task data to any external service.
