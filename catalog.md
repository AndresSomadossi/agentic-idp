# IDP Templates — Catalog

**Purpose**  
This catalog is the authoritative index of available scaffolds in the **IDP templates**.  
Agents MUST read this file before suggesting or listing stacks/technologies.

- **Status:** Active
- **Last updated:** YYYY-MM-DD
- **Conventions:** Use the **Templates Index** (machine-readable) to enumerate options; use **Template Details** to render human guidance.

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
- template_path: relative path to the template's root directory
- entrypoints: key entry files (relative paths)
- ci: supported CI examples included
- testing: primary test stack
- deployments: supported deployment platforms and methods
-->

```yaml
templates:
  - id: backend-bun-ts
    name: Backend — Bun + TypeScript (Drizzle, Zod)
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
    recommended_use: "High-throughput TypeScript backend on Bun with FP patterns and strong typing
    template_path: templates/backend-bun-ts
    entrypoints:
      - backend/index.ts
      - backend/routes.ts
    ci: github-actions
    testing: bun-test
    deployments:
      - platform: "Docker"
        description: "Containerized deployment with Docker"
      - platform: "Railway"
        description: "Direct deployment to Railway platform"
      - platform: "Render"
        description: "Container deployment on Render"

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
    deployments:
      - platform: "Docker"
        description: "Containerized deployment with Docker"
      - platform: "Railway"
        description: "Direct deployment to Railway platform"
      - platform: "Render"
        description: "Container deployment on Render"
      - platform: "Vercel"
        description: "Serverless functions on Vercel"
      - platform: "AWS Lambda"
        description: "Serverless deployment on AWS Lambda"
      - platform: "Azure Functions"
        description: "Serverless deployment on Azure Functions"


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
    deployments:
      - platform: "Vercel"
        description: "Optimized deployment on Vercel"
      - platform: "Netlify"
        description: "Static site deployment on Netlify"
      - platform: "Railway"
        description: "Full-stack deployment on Railway"
      - platform: "Render"
        description: "Static site deployment on Render"
      - platform: "AWS S3 + CloudFront"
        description: "Static hosting on AWS"
      - platform: "Azure Static Web Apps"
        description: "Static hosting on Azure"
      - platform: "VPS"
        description: "Traditional VPS deployment"

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
    deployments:
      - platform: "Vercel"
        description: "Frontend on Vercel, API on Vercel Functions"
      - platform: "Railway"
        description: "Full-stack deployment on Railway"
      - platform: "Render"
        description: "Full-stack deployment on Render"
      - platform: "Docker"
        description: "Containerized deployment with Docker Compose"
      - platform: "Kubernetes"
        description: "Container orchestration with Kubernetes"
      - platform: "VPS"
        description: "Traditional VPS deployment with PM2"
```
---

## No-Go Technologies

**Banned Technologies**  
The following technologies are explicitly NOT supported and should never be suggested:

- **Java** - Not supported in this IDP
- **C#/.NET** - Not supported in this IDP
- **PHP** - Not supported in this IDP
- **Ruby** - Not supported in this IDP
- **Scala** - Not supported in this IDP

**Deployment Platforms**  
Supported deployment options include:
- **Cloud:** AWS, Azure, Google Cloud, Vercel, Netlify, Railway, Render
- **Container:** Docker, Kubernetes
- **Serverless:** AWS Lambda, Azure Functions, Vercel Functions
- **VPS:** DigitalOcean, Linode, Hetzner

---
