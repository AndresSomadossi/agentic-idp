# Frontend — Next.js + TypeScript (App Router)

**ID:** `frontend-nextjs-ts`  
**Category:** frontend • **Runtime:** Node.js • **Lang:** TypeScript  
**Testing:** Playwright • **Lint:** ESLint/Biome

## Overview
Production-grade **Next.js (App Router)** setup with TypeScript, sensible ESLint/TS config, and e2e testing via Playwright. CI-ready.

## When to use
- You’re building a modern React app with server components and file-based routing.
- You want SSR/ISR and a batteries-included DX.

## Folder Structure
~~~text
app/
├── (routes)/         # Grouped routes
└── page.tsx          # Home page
~~~

_Add typical folders as needed: `app/api/`, `components/`, `lib/`, `styles/`, `hooks/`._

## Patterns
- **Data fetching:** `fetch` in server components; cache appropriately.
- **Types:** share `@types` package in monorepos; strict TS.
- **Env:** surface client-safe vars via `NEXT_PUBLIC_*`.

## Commands
~~~bash
pnpm install
pnpm dev
pnpm build
pnpm start
pnpm test:e2e
~~~

## Environment (example)
~~~env
NEXT_PUBLIC_API_BASE_URL=https://api.example.com
NODE_ENV=development
~~~

## Notes
- Prefer RSC for data-heavy pages; client components only when needed.
- Add `playwright.config.ts` and basic smoke tests.
