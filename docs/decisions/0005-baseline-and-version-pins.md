# 0005: Baseline and version pins

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-014

## Context
CLAUDE.md sets the stack: Next.js App Router, TypeScript strict, Tailwind, pnpm. The latest published versions do not all work together. Checked against the npm registry and vendor docs on 2026-11-16:

- `typescript@latest` is 7.0.2. `typescript-eslint` 8.72 supports `>=4.8.4 <6.1.0`, and the Next.js docs note that TypeScript 7 "does not currently provide the JavaScript compiler API". The newest 6.x is 6.0.3.
- `@react-three/fiber` 9.8.2 requires `react >=19 <19.4`. React is at 19.3.1. Sanity 6 and next-sanity 13 need React 19.2 or later.
- Next.js is at 16.4.6. `next lint` was removed in Next 16, so ESLint runs directly.
- This machine has Node 26.11 and no pnpm.
- The repo is not empty, so the official generator cannot scaffold into it directly.

## Decision
Proposed during planning; confirmed or revised in T-014.

- Next.js 16.4.x with the App Router, a `src/` directory and the `@/*` import alias.
- React 19.3.x.
- TypeScript 6.0.x with `strict` and `noUncheckedIndexedAccess`.
- Tailwind CSS 4.
- ESLint 10 with a flat config using `eslint-config-next` (core web vitals and TypeScript rules), `no-explicit-any` as an error, plus Prettier with the Tailwind plugin.
- pnpm, pinned through the `packageManager` field.
- A Node LTS version that Vercel offers, pinned in `.nvmrc` and `engines`. The exact version is checked in T-014 and T-018.
- Scripts: `lint` runs ESLint, `typecheck` runs `next typegen` then `tsc --noEmit`.
- Environment variables go through one hand-written module, `src/env.ts`, validated with zod and split into server and client parts. It starts with one variable and grows as integrations arrive (T-016).
- Next's Cache Components mode stays off (decision 0010). The React Compiler stays off.
- The skeleton is generated with `create-next-app` in a scratch folder and copied in.

## Alternatives considered
- TypeScript 7: Next can type-check with it through the project's `tsc`, but the lint rules cannot run on it yet.
- TypeScript 7 for the build and 6 for lint: two compilers to keep in step for no gain.
- `@t3-oss/env-nextjs` for the env module: a fine library, but the module is about forty lines and one fewer dependency.
- npm: CLAUDE.md names pnpm.

## Consequences
- TypeScript moves to 7 when `typescript-eslint` supports it; React moves to 19.4 when react-three-fiber allows it. Each move is a new record.
- pnpm has to be installed before T-014, with the owner's approval.
- Because the env module fails fast, every integration task must add its variables to `src/env.ts`, `.env.example` and Vercel together, or the build stops.
- Recent pnpm versions block dependency install scripts by default; the ones Next and Sanity need are approved in T-014.
