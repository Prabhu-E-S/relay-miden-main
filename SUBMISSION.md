# Project submission

Complete this file during the hackathon and use it to prepare your submission through the method announced by the organizers. Do not submit your project to the template repository.

## Project

- **Project name:** Relay Miden
- **Short description:** Offline-first, multilingual task-coordination platform designed to function under three severe operational constraints: no public internet connection, no shared network between devices, and no common language between users. In infrastructure blackouts, communities can create, track, and update mutual aid and emergency requests locally using browser IndexedDB, progressing through verified offline lifecycles.
- **Code repository URL:** TODO (Provide final repository URL, e.g., https://github.com/Prabhu-E-S/relay-miden-main)
- **Final submitted implementation commit SHA:** TODO (Developer to populate after final milestone commit)
- **Working demo URL or local demo steps:** Local demo running via `npm run dev` at `http://127.0.0.1:5173` or production preview via `npm run build && npm run preview -w @relay-miden/web` at `http://127.0.0.1:4173`
- **Demo access requirements:** Modern browser with IndexedDB support (Chrome/Chromium, Firefox, Safari, Edge). No internet connection, API keys, or external services required.

## Participants

Participate solo or in a team of up to 4. Remove unused rows.

| Participant name | GitHub handle | Contribution                                               |
| ---------------- | ------------- | ---------------------------------------------------------- |
| PRABHU E S       | Prabhu-E-S    | Architecture, UI design, offline task engine, verification |

## Run and demonstrate

- **Prerequisites and versions:** Node.js >= 24.0.0 < 25, npm >= 11
- **Install command:** `npm ci`
- **Required environment variable names:** None required for local offline operation. Optional development variables documented in `.env.example`: `PORT=3001`, `HOST=127.0.0.1`, `VITE_API_URL=http://127.0.0.1:3001`
- **Start command:** `npm run dev` (starts both frontend at `http://127.0.0.1:5173` and backend at `http://127.0.0.1:3001`) or `npm run dev:web`
- **Demo walkthrough:**
  1. Open `http://127.0.0.1:5173` in a browser.
  2. View the dashboard: note the responsive layout, Forest Green/Beige/Amber/Peach palette, and live summary metric cards.
  3. Navigate to **New Task** (`/create`) or use the desktop quick-create form.
  4. Submit a new task (e.g., "Clean drinking water distribution" at "Ward 4 Community Hall", priority "Urgent", action "Request").
  5. Observe the task instantly appearing on the Dashboard and in the task list (`/tasks`) without network requests.
  6. Open task details (`/tasks/:id`). Advance the lifecycle status (`pending` -> `acknowledged` -> `in_progress` -> `completed`).
  7. Check the activity history log showing atomic revision increments and actor device identity.
  8. Test task search and filtering by status and priority on the Tasks page.
  9. Reload the browser or disconnect network; all tasks, operations, and device identity persist in IndexedDB.
- **Checks performed and results:**
  - TypeScript: `npm run typecheck` passed across `@relay-miden/shared`, `@relay-miden/server`, `@relay-miden/web`.
  - ESLint: `npm run lint` passed with 0 warnings.
  - Vitest: `npm test` passed 28/28 tests across repository and form suites.
  - Build: `npm run build` compiled all packages successfully.
  - Playwright E2E: `npm run test:e2e` passed 14/14 test suites across 56 viewports/routes.
  - Prettier: `npm run format:check` passed.
- **Known limitations or incomplete features:**
  - Phase 3 PaperBridge QR transfer (encoding, scanning, decoding) remains a visual layout placeholder.
  - Phase 6 LAN Wi-Fi sync and transport are not yet implemented.
  - Phase 4 full UI localization (currently English/Malayalam/Tamil dictionary covers navigation and select headings).
  - Phase 8 installable PWA service worker caching is planned.
- **Libraries, APIs, and public datasets used:**
  - React 19, React Router 8, Vite 8, Tailwind CSS 4 (`@tailwindcss/vite`), TypeScript 6, Dexie.js 4 (`dexie`, `dexie-react-hooks`), Lucide React, Zod 4, Express 5, Fontsource DM Sans. No external APIs or cloud datasets are used.
- **AI usage record:** [AI_USAGE.md](AI_USAGE.md)
- **Development change log:** [CHANGELOG.md](CHANGELOG.md)

## Submission checklist

- [ ] The project implementation started from scratch at the event. _(Pending organizer evaluation / developer verification against event rules)_
- [x] I participated solo or with no more than 4 team members in total.
- [x] Codex was used during development and its usage is documented.
- [ ] The code repository URL, short description, and working demo are provided. _(Repository URL and live link pending final confirmation)_
- [x] README setup and demo instructions match the submitted code.
- [x] Actual checks and known limitations are documented.
- [ ] Meaningful changes are documented and committed throughout development. _(Git checkpoint commits to be finalized by developer)_
- [ ] The final implementation is committed and pushed, and its SHA is recorded above. _(Developer manual Git action required)_
- [x] No credentials or private data are included in the repository or demo instructions.
- [ ] The organizers' announced submission method and timing have been followed. _(To be completed at venue wrap-up)_

Event reference: [DevDay Exchange Community: Kochi on Luma](https://luma.com/z10nz8gp). The event wraps up by **10:00 AM IST on 25 October 2026** _(date updated per organizer confirmation)_.
