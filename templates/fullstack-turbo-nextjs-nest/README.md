# Fullstack — Turborepo (Next.js + NestJS)

**ID:** `fullstack-turbo-nextjs-nest`  
**Category:** fullstack • **Runtime:** Node.js • **Lang:** TypeScript  
**Testing:** Vitest/Playwright • **CI:** GitHub Actions

## Overview
Monorepo using **Turborepo** with **Next.js** (web) and **NestJS** (API), shared TypeScript types/config, and unified build/test pipelines. Caching-enabled builds, isolated app deployment, and consistent tooling across the stack.

## When to use
- You want type-safe web + API in one repo with shared packages.
- You need fast, incremental builds and independently deployable apps.

## Workspace Layout
~~~text
apps/
├── web/            # Next.js app
│   └── app/
│       └── page.tsx
└── api/            # NestJS app
    └── src/
        └── main.ts
packages/
├── shared/         # Shared types/utils
├── tsconfig/       # Base tsconfig(s)
└── eslint-config/  # Base lint config
~~~

## Patterns
- **Shared types:** `packages/shared` consumed by both apps.
- **Codegen (optional):** Generate OpenAPI from Nest → client SDK under `packages/shared`.
- **Env:** per-app `.env` files (`NEXT_PUBLIC_*` for client). Never leak server secrets to the web app.
- **Caching:** Use Turborepo remote/local caching; cache `pnpm` store in CI.
- **Isolated deploys:** Build and deploy `apps/web` and `apps/api` separately; version shared packages independently if needed.
- **Testing:** `vitest` for units; `playwright` for e2e (web), `supertest` for API integration.

## Commands
~~~bash
# install
pnpm install

# dev (run both or filter)
pnpm dev -r
pnpm dev --filter=web
pnpm dev --filter=api

# build
pnpm build -r

# test
pnpm test -r
pnpm test --filter=web
pnpm test --filter=api

# lint
pnpm lint -r
~~~

## Environment (examples)
~~~env
# apps/web
NEXT_PUBLIC_API_BASE_URL=http://localhost:3001
NODE_ENV=development
~~~

~~~env
# apps/api
PORT=3001
DATABASE_URL=postgres://user:pass@host:5432/db
JWT_SECRET=change-me
NODE_ENV=development
~~~

## CI (GitHub Actions) tips
- Cache `~/.pnpm-store` and Turborepo outputs.
- Use `pnpm -r build` for the full workspace; or matrix builds per app.
- Enable incremental Next.js and NestJS builds; upload build artifacts if deploying from CI.

## Notes
- Provide Dockerfiles per app for containerized deploys.
- Consider `changesets` for versioning `packages/*`.
- Add `eslint` and `tsconfig` presets in `packages/*` to unify rules.
- If you need SSR + authenticated API calls, forward cookies from `web` to `api` using a fetch wrapper in `packages/shared`.