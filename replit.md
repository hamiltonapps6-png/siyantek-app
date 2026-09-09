# Siyantek

Siyantek is an offline-first car maintenance tracker with Arabic, French, and English support.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/siyantek run dev` — run the Expo mobile preview
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Expo Router mobile app with React Native
- AsyncStorage for local, offline persistence
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/siyantek/app/index.tsx` — dashboard, records view, and maintenance/vehicle forms
- `artifacts/siyantek/context/SiyantekContext.tsx` — localized copy and AsyncStorage-backed vehicle state
- `artifacts/siyantek/constants/colors.ts` — Siyantek visual tokens
- `artifacts/siyantek/assets/images/siyantek-icon.png` — app icon

## Architecture decisions

- First build is fully local and offline; no API or database is needed for the requested feature set.
- The dashboard and history are kept in one screen to make the core maintenance loop fast on mobile.
- Arabic uses RTL-aware row/text alignment without forcing a native reload when switching languages.

## Product

- Shows the current vehicle, mileage, service progress, vehicle health, and recent maintenance.
- Lets users add maintenance type, mileage, date, cost, notes, and next-service mileage.
- Stores vehicle details and records on-device with AsyncStorage.
- Supports English, French, and Arabic (including Arabic layout direction).

## User preferences

No additional user preferences recorded.

## Gotchas

- Use the managed `artifacts/siyantek: expo` workflow for the mobile preview so Expo receives the required Replit environment.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
