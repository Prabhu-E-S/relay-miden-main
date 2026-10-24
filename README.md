# Relay Miden

**When networks fail, communication shouldn't.**

Relay Miden is an offline-first, multilingual task-coordination platform created for the **DevDay Exchange Community Hackathon: Kochi** (24–25 October 2026). When infrastructure collapses during natural disasters or power blackouts, emergency response and mutual aid fail because tools assume constant connectivity. Relay Miden is built to coordinate relief workers, volunteers, and affected community members under three severe operational constraints:

1. **No public internet connection.**
2. **No shared network between devices.**
3. **No common language between users.**

---

## Event details

| Detail       | Information                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------- |
| Hackathon    | **DevDay Exchange Community Hackathon: Kochi**                                                     |
| Dates        | **24–25 October 2026** _(Confirmed date correction; original template stated 10–11 October 2026)_  |
| Venue        | JAIN University, Kochi — rooms 2008 and 2009                                                       |
| Registration | [Luma Event Page](https://luma.com/z10nz8gp)                                                       |
| Location     | [Venue Map](https://maps.app.goo.gl/Eme7gR7NDXSNRANu5)                                             |
| Team         | Solo participant: PRABHU E S (`Prabhu-E-S`)                                                        |
| Working demo | Local development server (`http://127.0.0.1:5173`) or production preview (`http://127.0.0.1:4173`) |

**Quick Links:** **[RULES.md](RULES.md)** · **[AGENTS.md](AGENTS.md)** · **[AI_USAGE.md](AI_USAGE.md)** · **[CHANGELOG.md](CHANGELOG.md)** · **[SUBMISSION.md](SUBMISSION.md)** · **[Architecture](docs/architecture.md)** · **[Design System](docs/design-system.md)** · **[Implementation Plan](docs/implementation-plan.md)** · **[Development History](docs/history/)**

---

## Project overview

- **Project name:** Relay Miden
- **Problem statement:** Natural disasters, extreme weather, and grid failures cut off cellular and internet access. Relief teams and local communities still need to register emergency requests, allocate clean water and medical aid, track progress, and coordinate volunteers without centralized cloud servers or common spoken languages.
- **Target users:** Disaster response coordinators, community shelter managers, frontline mutual-aid volunteers, and non-technical residents who require simple, robust, visual, and localized coordination.
- **Core constraints:**
  1. _Zero Internet:_ All core operations run client-side in the browser using local storage.
  2. _Zero Shared Network:_ Future synchronization transfers state device-to-device via optical QR codes (PaperBridge) and ad-hoc LAN.
  3. _Zero Common Language:_ Visual iconography, standardized structured task fields, and multilingual interfaces (English, Malayalam, Tamil).

---

## Technology stack

Relay Miden is structured as an npm workspaces monorepo containing `apps/web`, `apps/server`, and `packages/shared`.

| Layer                          | Technology            | Version                 | Purpose                                                    |
| ------------------------------ | --------------------- | ----------------------- | ---------------------------------------------------------- |
| **Frontend Framework**         | React                 | `19.3.1`                | Declarative user interface                                 |
| **Build Tool & Dev Server**    | Vite                  | `8.3.5`                 | Fast ESM module bundling                                   |
| **Language & Typing**          | TypeScript            | `6.0.3`                 | Strict type safety across workspaces                       |
| **Styling**                    | Tailwind CSS          | `4.3.3`                 | Utility styling integrated via `@tailwindcss/vite`         |
| **Client Database**            | Dexie.js (IndexedDB)  | `4.4.7`                 | Offline storage for tasks, operations, and device identity |
| **Reactive DB Hooks**          | `dexie-react-hooks`   | `4.4.0`                 | Reactive component updates via `useLiveQuery`              |
| **Icons**                      | Lucide React          | `1.61.0`                | Functional iconography without filled tiles                |
| **Routing**                    | React Router          | `8.5.0`                 | Declarative client-side routing                            |
| **Schema Validation**          | Zod                   | `4.6.7`                 | Runtime schema validation in `@relay-miden/shared`         |
| **Typography**                 | `@fontsource/dm-sans` | `5.3.0`                 | Locally bundled DM Sans typography                         |
| **Backend Process**            | Express               | `5.3.0`                 | Minimal Node.js loopback service (`GET /health`)           |
| **Runtime & Package Manager**  | Node.js / npm         | `>=24.0.0 <25` / `>=11` | Monorepo execution and workspaces                          |
| **Unit & Integration Testing** | Vitest                | `5.0.5`                 | In-memory unit tests with `fake-indexeddb`                 |
| **End-to-End Testing**         | Playwright            | `1.64.1`                | Cross-viewport browser automation                          |
| **Linting & Code Quality**     | ESLint & Prettier     | `10.13.0` / `3.9.10`    | Static analysis and code style consistency                 |

No paid APIs, cloud databases, external CDNs, or tracking services are used.

---

## Setup and development instructions

### Prerequisites

- **Node.js**: `24.x LTS` (`>=24.0.0 <25`)
- **npm**: `11.x` (`>=11.0.0`)
- **Supported OS**: Windows (PowerShell supported), macOS, Linux
- Modern browser with IndexedDB support (Chromium, Firefox, Safari, Edge)

### 1. Installation

Install all dependencies using npm workspaces:

```sh
npm ci
```

For browser end-to-end testing, ensure Playwright Chromium is installed:

```sh
npx playwright install chromium
```

### 2. Environment configuration

Copy the example environment configuration (optional for basic local operation):

```sh
cp .env.example .env
```

| Variable       | Default in `.env.example` | Role                                                            |
| -------------- | ------------------------- | --------------------------------------------------------------- |
| `PORT`         | `3001`                    | Port for Express health backend                                 |
| `HOST`         | `127.0.0.1`               | Express bind address (strictly loopback)                        |
| `VITE_API_URL` | `http://127.0.0.1:3001`   | Public frontend URL pointer; Phase 2 UI does not call task APIs |

_All `VITE_` variables are public browser values. Never store secrets in `.env`._

### 3. Running development servers

Start both frontend and backend concurrently:

```sh
npm run dev
```

Alternatively, run workspaces individually:

```sh
npm run dev:web     # Frontend: http://127.0.0.1:5173
npm run dev:server  # Express health backend: http://127.0.0.1:3001/health
```

### 4. Running checks, lint, and tests

Run the complete validation suite:

```sh
# Static type checking across all workspaces
npm run typecheck

# ESLint analysis with zero warning tolerance
npm run lint

# Unit and integration tests (Vitest)
npm test

# Production build of all packages
npm run build

# End-to-end browser test suite (Playwright)
npm run test:e2e

# Code style compliance check
npm run format:check
```

### 5. Running the production preview

```sh
# Compile all workspace packages
npm run build

# Preview production frontend build on port 4173
npm run preview -w @relay-miden/web

# Run compiled backend process
npm run start -w @relay-miden/server
```

---

## Project status and ten-phase roadmap

| Phase  | Scope                                                                                                  |           Status           | Evidence & Verification                                                                                                                                               |
| :----: | ------------------------------------------------------------------------------------------------------ | :------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1**  | Repository setup, design system, responsive UI, Express health endpoint, architecture                  | **Implemented & Verified** | Verified 24 Oct 2026. Full responsive layout (320px–1440px), centralized palette, 8 routes. See [phase-01 history](docs/history/phase-01-20261024T142943Z-9c4b1e.md). |
| **2**  | Offline task engine: IndexedDB (Dexie), Zod schemas, atomic operations, revisions, device identity     | **Implemented & Verified** | Verified 24 Oct 2026. 28 Vitest tests, 14 Playwright E2E suites passing. See [phase-02 recovery history](docs/history/phase-02-recovery-20261024T153500Z-a7f3c2.md).  |
| **3**  | PaperBridge QR protocol: versioned envelopes, compact encoding, optical camera transfer, deduplication |        **Planned**         | Next authorized phase. UI currently displays layout placeholders.                                                                                                     |
| **4**  | Multilingual communication: localized task templates and full UI in English, Malayalam, Tamil          |        **Planned**         | Navigation dictionary and language selector in place; full translation pending.                                                                                       |
| **5**  | Two-way QR lifecycle: peer acknowledgments, bidirectional status transitions, conflict semantics       |        **Planned**         | Architecture defined in [docs/architecture.md](docs/architecture.md).                                                                                                 |
| **6**  | Local Wi-Fi communication: LAN transport, peer discovery, and local subnet packet transfer             |        **Planned**         | Architecture defined; Express loopback foundation in place.                                                                                                           |
| **7**  | Offline queue and synchronization: durable outbox, idempotent retries, causal reconciliation           |        **Planned**         | Revision/parentRevision metadata already captured in Phase 2 operations.                                                                                              |
| **8**  | PWA and mobile readiness: service worker caching, Web App Manifest, offline startup                    |        **Planned**         | Asset structure and local fonts in place.                                                                                                                             |
| **9**  | Final UI and mission control: integrated operational triage, accessibility audit, field polish         |        **Planned**         | Design system tokens established in [docs/design-system.md](docs/design-system.md).                                                                                   |
| **10** | Testing and demo preparation: edge cases, device rehearsals, failure modes                             |        **Planned**         | Test frameworks configured and active.                                                                                                                                |

---

## Detailed feature status

### Implemented and verified features (Phases 1 & 2)

- **Offline database (`relay-miden-db`)**: IndexedDB stores for `tasks`, `operations`, and `settings` with compound indexes.
- **Atomic task mutations**: Every task creation, update, status advance, reopen, or soft-deletion executes inside an atomic Dexie transaction creating both the task record and an immutable `TaskOperation`.
- **Revision and lineage tracking**: Monotonic revision increments with `parentRevision` linking for future synchronization conflict detection.
- **Persistent anonymous identity**: Random device UUID generated and persisted in `settings` on initial launch; identifies record origin without personal data.
- **Reactive UI queries (`useLiveQuery`)**: Dashboard counters (Total, Open, In Progress, Critical) and task lists update in real time on mutation.
- **Search and filtering**: Real-time client-side search across title, location, description, and status/priority filters with deterministic sorting.
- **Approved design system**: Exact centralized brand palette in `apps/web/src/styles/palette.css`:
  - Forest Green (`#004225`), Beige (`#F5F5DC`), Amber (`#FFB000`), Peach (`#FFCF9D`).
  - Text-only priority indicators (no background pill fills).
  - Clean metric icons (no background box fills).
- **Responsive navigation**: Fixed 224px desktop sidebar, mobile header, bottom navigation bar with 5 destinations, and touch targets >= 44px.
- **Express health endpoint**: `GET /health` returns `{ "status": "ok", "service": "relay-miden-server", "phase": 2 }`.

### Implemented but unverified features

- None. All implemented features for Phase 1 and Phase 2 have been verified with automated unit and E2E test suites.

### Planned features (Phases 3–10)

- Versioned PaperBridge QR encoding/decoding and optical camera scanning.
- Complete Malayalam and Tamil task templates and translation.
- Two-way peer acknowledgment receipts.
- Local Wi-Fi subnet transport and peer discovery.
- Service worker caching for zero-network startup (PWA).

### Known limitations

- **QR Send & Receive**: Routes `/send` and `/receive` render layout interfaces with real local task selectors, but optical scanning and QR generation are scheduled for Phase 3.
- **Language Dictionary**: Language switching applies to navigation and primary labels; full multilingual task templates are scheduled for Phase 4.
- **Server Scope**: The Express server is an architectural stub for future LAN transport; all Phase 2 task coordination operates without backend interaction.
- **Offline Startup**: The app runs offline once loaded, but full PWA offline startup caching arrives in Phase 8.

---

## Development history and permanent policies

Every AI development execution creates an append-only Markdown record in `docs/history/` under the format `phase-XX-YYYYMMDDTHHMMSSZ-unique.md` or a descriptive migration prefix. Previous records are never modified, deleted, or overwritten.

- [Phase 1: Repository initialization and verification — 2026-10-24](docs/history/phase-01-20261024T142943Z-9c4b1e.md)
- [Phase 2: Offline engine recovery and verification — 2026-10-24](docs/history/phase-02-recovery-20261024T153500Z-a7f3c2.md)
- [Official Template Migration, Conflict Resolution & Full Verification — 2026-10-24](docs/history/template-migration-20261024T163000Z-7e4f1a.md)

_Note: All Git operations (commits, branches, pushes) are reserved for developer execution as mandated in [AGENTS.md](AGENTS.md). The original MIT [LICENSE](LICENSE) is preserved._
