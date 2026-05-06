# Workspace

## Overview

pnpm workspace monorepo using TypeScript. This is the **Replit2Api** project — an AI API proxy server that routes requests to OpenAI, Anthropic, Claude, Gemini, and OpenRouter models, with a management portal frontend.

**Version**: 1.1.7 (from GitHub: Akatsuki03/Replit2Api)

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite (api-portal)
- **Cloud storage**: Google Cloud Storage (for config persistence in production)

## Artifacts

- **api-server** — Express API proxy server, handles AI model routing, settings, updates
- **api-portal** — React frontend management UI (preview at `/`)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## API Routes

- `GET /api/healthz` — health check
- `GET /api/setup-status` — check if PROXY_API_KEY and AI integrations are configured
- `GET /api/update/status` — update status from GitHub
- `POST /api/update/apply` — pull latest code from GitHub and restart
- `GET /settings/sillytavern` — SillyTavern mode setting
- `POST /settings/sillytavern` — toggle SillyTavern mode
- `GET/POST /v1/chat/completions` — OpenAI-compatible chat proxy
- `GET /v1/models` — list available models

## Environment Variables Required

- `PROXY_API_KEY` — API key clients use to authenticate to this proxy
- `AI_INTEGRATIONS_OPENAI_API_KEY` / `AI_INTEGRATIONS_OPENAI_BASE_URL` — OpenAI integration
- `AI_INTEGRATIONS_ANTHROPIC_API_KEY` / `AI_INTEGRATIONS_ANTHROPIC_BASE_URL` — Anthropic integration
- `AI_INTEGRATIONS_GEMINI_API_KEY` / `AI_INTEGRATIONS_GEMINI_BASE_URL` — Gemini integration
- `AI_INTEGRATIONS_OPENROUTER_API_KEY` / `AI_INTEGRATIONS_OPENROUTER_BASE_URL` — OpenRouter integration
- `DEFAULT_OBJECT_STORAGE_BUCKET_ID` — GCS bucket for cloud persistence (optional in dev)
- `GITHUB_TOKEN` — GitHub token for authenticated update checks (optional)

## GitHub Source

Repository: https://github.com/Akatsuki03/Replit2Api

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
