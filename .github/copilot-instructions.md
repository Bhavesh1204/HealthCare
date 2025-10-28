## Repo snapshot

- Single-page React app under `frontend/` (Create React App / `react-scripts`).
- Key folders: `frontend/src/components/` (UI), `frontend/src/data/` (static data like `prakritiQuestions.js`).

## What's important for an AI assistant

- Routing: `frontend/src/App.js` registers routes: `/`, `/login`, `/register`, `/profile`, `/prakriti`, plus added admin/demo routes `/diet`, `/schedule`, `/followups`, `/admin`.
- Persistence: The app simulates back-end storage using `localStorage`. Two conventions are used:
  - `users` — array of user objects (id, name, email, password, premium, prakriti, diet, schedule, followUps).
  - `user` — current session user (duplicate of an entry from `users`).

## Common patterns to follow

- Use functional components with React hooks (useState, useEffect, useNavigate). Example: `Login.js`, `Register.js`, `PrakritiQuiz.js`.
- Navigation: use `useNavigate()` and Routes/Route element syntax. When adding routes, update `App.js`.
- Local data changes: update both the `users` array and the `user` session object together so UI stays consistent (see `PrakritiQuiz.js` for an example of updating both).
- UI style: components use inline style objects or scoped style blocks inside components. Keep new components consistent with this approach unless adding a global stylesheet.

## Build & dev workflow

- Project root (for commands): `frontend/`
- Install deps: `npm install`
- Start dev server: `npm start` (CRA default port 3000)
- Build: `npm run build`
- Tests: `npm test`

## Integration notes & precautions

- There is no external backend by default. If adding an API, create `frontend/.env.local` for base URLs and provide a graceful fallback to `localStorage` for demos.
- When adding dependencies, run `npm install` before `npm start`. Some packages (e.g., `uuid` v9) are ESM-only — prefer `uuid` v8 or use import syntax compatible with CRA's toolchain.

## Examples / quick recipes

- Add a route: import component in `App.js` and add

  <Route path="/new" element={<NewComponent />} />

- Persist derived user data (prakriti): read `user` from `localStorage`, update fields (e.g., `prakriti`, `diet`), then write back and update the `users` list.

## When something breaks

- First run: `npm install` after any `package.json` changes. Then `npm start` and copy terminal/browser console errors.
- Common root causes:
  - missing `npm install` after dependency edits
  - ESM vs CJS incompatibility for certain packages (check package docs)
  - mismatched route/component imports (typos in file paths)

## What I can do next

- Add or update `.github/CODEOWNERS`, `CONTRIBUTING.md`, or a short `frontend/DEVELOPMENT.md` with these commands and conventions.
- Replace `localStorage` with a simple pluggable API adapter (so components can switch to a real backend later).

If this looks good, I can also (re)generate a short `CONTRIBUTING` or `DEVELOPER_SETUP` file and run `npm install` for you. Reply with which one you'd like first.
