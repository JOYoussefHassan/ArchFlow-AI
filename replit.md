# ArchForge

ArchForge is a browser-based software architecture workbench that helps developers model systems, validate their relationships, and generate implementation plans and coding-agent prompts.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/archforge run dev` — open ArchForge in the Replit preview
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/archforge/index.html` — standalone application source: markup, styles, SVG canvas, and vanilla JavaScript.
- `artifacts/archforge/.replit-artifact/artifact.toml` — Replit preview and service routing configuration.
- The API server and database are not used by ArchForge.

## Architecture decisions

- Keep the app self-contained in one HTML file so it can also run when opened directly in a modern browser.
- Use local browser storage for project persistence; no account, backend, or external AI provider is needed for core behavior.
- Keep graph records as the authoritative model; SVG is only their interactive visual representation.
- Architecture analysis and prompt/roadmap generation must be described as deterministic rules, never as live AI.

## Product

- A visual architecture editor with a component library, node and connection inspector, and network boundaries.
- Project validation, dependency-aware implementation tasks, and coding-agent prompt generation.
- Local project persistence and JSON-based architecture import/export.

## User preferences

- The requested deliverable is one self-contained `index.html` using only HTML, CSS, vanilla JavaScript, and SVG; no React, frontend framework, external runtime library, or backend.

## Gotchas

- Keep application styles and behavior in `index.html`; the Replit preview serves this file, while direct-file use must remain functional without Vite.
- Never import user-provided strings as executable code; validate imported JSON before replacing the current project.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
