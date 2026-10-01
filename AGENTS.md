# Base44 Dev Environment

## What this repo is

`firebase-framework-tools` is a **library monorepo** (npm packages for Firebase App Hosting adapters), not a runnable web application. There is no web UI in the root packages.

## What runs in the preview

The Base44 preview serves the **Next.js starter app** at `starters/nextjs/basic/` — a self-contained Next.js 15 app demonstrating SSG, SSR, and ISR. It needs no external credentials; the only env var (`MESSAGE`) defaults to `"Hello!"`.

## How it's wired

- `docker-compose.base44.yml` runs `node:22-bookworm-slim`, bind-mounts the repo, runs `npm ci` then `next dev -H 0.0.0.0 -p 3000` inside `starters/nextjs/basic`.
- `starters/nextjs/basic/next.config.mjs` has `allowedDevOrigins` set from `BASE44_PUBLIC_HOST_SUFFIX` so the preview origin can reach the dev server.
- Port 3000 is the web entry point.

## Developing the library packages

The root monorepo uses lerna + npm workspaces. To build/test the library packages (not the preview):

```bash
npm install        # install workspace deps at repo root
npm run build      # build all packages via scripts/build.js
npm test           # run tests via scripts/test.js
```

These are separate from the preview's Next.js dev server.
