# Change log

Record each meaningful project change during the event, newest first. Update this file in the same commit as the change. Use a real timestamp with timezone, for example `YYYY-MM-DDTHH:MM:SS+05:30`.

## Event build log

### 2026-10-24T22:00:00+05:30 (16:30:00 UTC) — Official template migration, conflict resolution, and verification

- Changed: Restored root `LICENSE` and `.prettierignore`; updated `.gitignore` with Playwright, coverage, build cache, and database patterns; integrated organizer template requirements across `AGENTS.md`, `RULES.md`, `AI_USAGE.md`, `SUBMISSION.md`, and `README.md`; created append-only migration history file `docs/history/template-migration-20261024T163000Z-7e4f1a.md`.
- Why: Reconcile existing Relay Miden implementation with official hackathon template repository while preserving all Phase 1/Phase 2 features, design system integrity, and organizer guidelines.
- Validation: Type checking (`npm run typecheck`), linting (`npm run lint`), unit/integration tests (`npm test`), production build (`npm run build`), browser E2E tests (`npm run test:e2e`), and formatting check (`npm run format:check`).
- Limitations: All Git operations reserved for developer; Phase 3 (PaperBridge QR protocol) is planned and not started.

### 2026-10-24T21:05:00+05:30 (15:35:00 UTC) — Phase 2 offline engine recovery and full verification

- Changed: Completed Phase 2 verification audit; updated `docs/architecture.md`, `docs/implementation-plan.md`, and `README.md`; executed full audit across Dexie stores, reactive UI queries, unit tests, and E2E browser tests; created `docs/history/phase-02-recovery-20261024T153500Z-a7f3c2.md`.
- Why: Recover from Codex limit cutoff and establish documented verification for offline task management.
- Validation: `npm run typecheck` passed; `npm run lint` passed (0 warnings); `npm test` (28/28 passed); `npm run build` passed; `npm run test:e2e` (14/14 suites passed across 56 viewports/routes); `npm run format:check` passed.
- Limitations: PaperBridge QR transport and camera access remain planned for Phase 3; LAN transport remains planned for Phase 6.

### 2026-10-24 (exact time unknown) — Phase 2 offline task engine implementation

- Changed: Added Dexie.js `RelayMidenDatabase` with `tasks`, `operations`, and `settings` stores; implemented `TaskRepository` with atomic transactions, soft delete, deterministic sorting, revision tracking, and persistent device UUID; bound UI components to IndexedDB (`useLiveQuery`).
- Why: Provide local task coordination operating under zero-connectivity constraints.
- Validation: Unit tests in `apps/web/src/db/task-repository.test.ts` against `fake-indexeddb`.
- Limitations: Interrupted before execution record and documentation updates were finalized.

### 2026-10-24T19:59:43+05:30 (14:29:43 UTC) — Phase 1 repository initialization, design system, and responsive UI

- Changed: Initialized npm workspaces monorepo; centralized brand palette in `apps/web/src/styles/palette.css`; built responsive desktop sidebar, mobile header/bottom navigation, 8 routes, Express `/health` server, Zod schemas, Vitest/Playwright tests; documented in `docs/history/phase-01-20261024T142943Z-9c4b1e.md`.
- Why: Establish architectural foundation and responsive user interface for offline task coordination.
- Validation: `npm run typecheck`, `npm run lint`, `npm test`, Playwright responsive tests across 7 viewports.
- Limitations: Task persistence and QR transfer were visual previews/mockups pending Phase 2 and 3.

## Template setup — 10 October 2026

- Changed: Added the event README, rules, agent guide, change log, AI usage record, submission checklist, Git ignore rules, and pull request checklist.
- Why: Give participants a consistent starting point for event rules, basic coding patterns, documented changes, and regular commits.
- Validation: Checked local Markdown links, event detail consistency, required documents, and diff whitespace before publishing.
- Limitations: Documentation scaffolding only; no participant project, application, or working demo is included. GitHub publication and template status are verified separately after creation.
