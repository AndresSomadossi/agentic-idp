# IDP Templates — Catalog

**Purpose**  
This catalog is the authoritative index of available scaffolds in the **IDP templates**.  
Agents MUST read this file before suggesting or listing stacks/technologies.

- **Status:** Active
- **Last updated:** YYYY-MM-DD
- **Conventions:** Use the **Templates Index** (machine-readable) to enumerate options; use **Template Details** to render human guidance.

---

## Templates Index

<!--
This index is intentionally machine-friendly.
Fields:
- id: unique short id (kebab-case)
- name: human-readable title
- category: backend | frontend | fullstack | library | infra
- runtime: bun | node | deno | go | python | rust | other
- language: typescript | javascript | go | python | rust | other
- frameworks: array of primary frameworks
- layers: list of notable architectural layers included
- recommended_use: short when-to-use one-liner
- template_path: relative path to the template’s root directory
- entrypoints: key entry files (relative paths)
- ci: supported CI examples included
- testing: primary test stack
-->

```yaml
templates:
  - id: backend-bun-ts
    name: Backend — Bun + TypeScript, Drizzle, Zod, Azure Blob
    category: backend
    runtime: bun
    language: typescript
    frameworks: []
    layers:
      - api-handler
      - routing
      - entities
      - database
      - storage
      - processing
      - config
    recommended_use: "High-throughput TypeScript backend on Bun with FP patterns, strong typing, and blob storage."
    template_path: templates/backend-bun-ts
    entrypoints:
      - backend/index.ts
      - backend/routes.ts
    ci: github-actions
    testing: bun-test

  - id: backend-node-ts-express
    name: Backend — Node.js + TypeScript (Express/Effect/Zod)
    category: backend
    runtime: node
    language: typescript
    frameworks: [express]
    layers: [routing, handlers, entities, database, config, testing]
    recommended_use: "Conventional Node/TS API with Express; broad ecosystem compatibility."
    template_path: templates/backend-node-ts-express
    entrypoints:
      - src/index.ts
      - src/routes.ts
    ci: github-actions
    testing: vitest

  - id: frontend-nextjs-ts
    name: Frontend — Next.js + TypeScript (App Router)
    category: frontend
    runtime: node
    language: typescript
    frameworks: [nextjs]
    layers: [ui, state, api-client, auth, testing]
    recommended_use: "Production React/Next app with App Router and sensible defaults."
    template_path: templates/frontend-nextjs-ts
    entrypoints:
      - app/page.tsx
    ci: github-actions
    testing: playwright

  - id: fullstack-turbo-nextjs-nest
    name: Fullstack — Turborepo (Next.js + NestJS)
    category: fullstack
    runtime: node
    language: typescript
    frameworks: [turborepo, nextjs, nestjs]
    layers: [apps, packages, shared-config, ci]
    recommended_use: "Monorepo with shared types and build pipelines for web + API."
    template_path: templates/fullstack-turbo-next-nest
    entrypoints:
      - apps/web/app/page.tsx
      - apps/api/src/main.ts
    ci: github-actions
    testing: vitest