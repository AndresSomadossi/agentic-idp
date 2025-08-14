# Backend — Node.js + TypeScript (Express/Effect/Zod)

**ID:** `backend-node-ts-express`  
**Category:** backend • **Runtime:** Node.js • **Lang:** TypeScript  
**Testing:** Vitest • **Lint:** ESLint/Biome (pick one) • **DB:** (swap in Drizzle/Prisma)

## Overview
Conventional Node/TS API using **Express**, **Zod** for validation, and optional **Effect** for typed effects. Balanced defaults, broad ecosystem support.

## When to use
- You want mainstream Express patterns and npm ecosystem depth.
- You prefer Node.js over Bun, or need Express middleware compatibility.

## Folder Structure
~~~text
src/
├── config/        # Zod-validated env config
├── db/            # ORM (Drizzle/Prisma) + migrations
├── domain/        # Entities, services, use-cases
├── routes/        # Route registrations + validators
├── middleware/    # Express middlewares (auth, errors, etc.)
├── services/      # External integrations (s3, email, etc.)
└── index.ts       # App entrypoint (http server)
~~~

## Patterns
- **Validation:** Zod schemas per route; parse body/query/headers.
- **Error flow:** Central error middleware; typed error objects.
- **DI:** Pass services/config into route factories.

## Commands
~~~bash
pnpm install
pnpm dev
pnpm test
pnpm lint
pnpm build
~~~

## Environment (example)
~~~env
PORT=3000
NODE_ENV=development
DATABASE_URL=postgres://user:pass@host:5432/db
JWT_SECRET=...
~~~

## Notes
- Add rate limiting & request logging (pino-http).
- If you need typed effects, integrate `effect` for services/fibers.