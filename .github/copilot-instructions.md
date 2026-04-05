<!-- Copilot instructions for contributors and AI coding agents -->
# Project overview for AI agents

This is a single-page React application bootstrapped with Create React App. Key facts:

- **Runtime / build:** Uses `react-scripts` (see [package.json](package.json)).
- **Development Docker image:** `Dockerfile.dev` installs dependencies and runs `npm run start`.
- **Production image:** `Dockerfile` is a multi-stage build that runs `npm run build` and serves `build/` with `nginx`.

# What to read first

- [package.json](package.json) — canonical npm scripts and dependencies.
- [Dockerfile.dev](Dockerfile.dev) — how the dev container is built and started.
- [Dockerfile](Dockerfile) — production multi-stage build and nginx deployment.
- `src/` — React entry points: `src/index.js`, `src/App.js` (UI component examples).

# Architecture & intent (concise)

- Single React app served directly in development by `react-scripts start` (hot reload on localhost:3000).
- For production, the repository uses a builder stage to produce a static `build/` folder then serves it via `nginx`.
- No backend services are present in this repository; integration with APIs happens client-side via fetch/XHR from the SPA.

# Developer workflows (explicit commands)

- Local dev (node):

  - Install deps: `npm install`
  - Start dev server: `npm start` (opens at http://localhost:3000)

- Dev container (Dockerfile.dev):

  - Build: `docker build -f Dockerfile.dev -t frontend-dev .`
  - Run: `docker run -p 3000:3000 frontend-dev`

  Note: `Dockerfile.dev` copies files at build time and runs `npm run start` inside container.

- Production image (multi-stage Dockerfile):

  - Build image: `docker build -t frontend-prod .`
  - Run: `docker run -p 80:80 frontend-prod`

- Tests: `npm test` (uses `react-scripts test` - interactive watch by default).

# Project-specific patterns and conventions

- This repo follows Create React App conventions: single `src/` entry, `public/index.html`, and `react-scripts` toolchain.
- No custom Webpack, Babel, or CI scripts are present—assume default CRA behavior unless you find an `eject`.
- Docker usage is minimal: `Dockerfile.dev` for simple containerized dev and `Dockerfile` for production static hosting.

# Integration points to watch for

- Static assets: `public/` (index.html, manifest, etc.) — assets are copied into the final `build/`.
- Entry points: `src/index.js` bootstraps the app and mounts the React tree.

# Examples for code edits

- To add a new UI component: create `src/components/MyComponent.js`, export it, and import in `src/App.js`.
- To add a dev dependency used by the build: update `package.json` and ensure `npm install` runs in Dockerfile.dev if required.

# When in doubt

- Follow existing CRA patterns in `src/` (functional components, testing with `@testing-library/react`).
- Prefer modifying `src/` and `public/` files; avoid changing Dockerfiles unless adjusting container behavior.

---
If anything here is unclear or you want examples for specific tasks (adding a route, adding CI, or switching to a bind-mounted dev container), tell me which area to expand.
