# Flow — T3 Turbo + Drizzle + NextAuth Monorepo

## Commands
- Dev (all apps): `pnpm dev`
- Build: `pnpm build`
- Lint: `pnpm lint` / `pnpm lint:fix`
- Format: `pnpm format` / `pnpm format:fix`
- Type-check: `pnpm typecheck`
- DB push: `pnpm db:push`
- DB studio: `pnpm db:studio`

## Architecture
- **Monorepo tool**: Turborepo 1.10 with pnpm 8.9 workspaces
- **Package manager**: pnpm

### Apps
| App | Path | Stack |
|-----|------|-------|
| nextjs | `apps/nextjs` | Next.js 13.5, React 18, Tailwind, tRPC client, NextAuth |
| expo | `apps/expo` | React Native 0.72, Expo 49, Expo Router 2, NativeWind |

### Packages
| Package | Path | Purpose |
|---------|------|---------|
| @acme/api | `packages/api` | tRPC server router + procedures |
| @acme/auth | `packages/auth` | NextAuth.js v5 config + Drizzle adapter |
| @acme/db | `packages/db` | Drizzle ORM schema + PlanetScale driver |

### Tooling
| Package | Path | Purpose |
|---------|------|---------|
| @acme/eslint-config | `tooling/eslint` | Shared ESLint (base, nextjs, react presets) |
| @acme/prettier-config | `tooling/prettier` | Shared Prettier + import sorting + Tailwind plugin |
| @acme/tailwind-config | `tooling/tailwind` | Shared Tailwind + PostCSS config |
| @acme/tsconfig | `tooling/typescript` | Shared TypeScript base config |

## Key Tech
- **API**: tRPC 10.40 (end-to-end typesafe RPC)
- **Database**: PlanetScale (MySQL-compatible serverless), Drizzle ORM
- **Auth**: NextAuth.js v5 with Drizzle adapter (Discord provider)
- **Data fetching**: React Query (TanStack Query)
- **Validation**: Zod
- **Styling**: Tailwind CSS 3.3 (web) + NativeWind (mobile)

## Environment Variables
- `DATABASE_URL` — PlanetScale connection string
- `DISCORD_CLIENT_ID` / `DISCORD_CLIENT_SECRET` — Discord OAuth
- `NEXTAUTH_SECRET` — NextAuth session encryption
- `NEXTAUTH_URL` — NextAuth callback URL

## Conventions
- TypeScript throughout all packages
- tRPC for all API communication (no REST endpoints)
- Shared types flow from @acme/db → @acme/auth → @acme/api → apps
- Zod schemas for all input validation
- Tooling configs in `tooling/` (not `packages/config/`)
- Tailwind for all styling (NativeWind on mobile)
