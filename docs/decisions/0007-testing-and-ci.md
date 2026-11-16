# 0007: Testing and CI

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-019

## Context
The spec and CLAUDE.md define verification as lint, typecheck, build and a browser check. They do not mention automated tests or CI. Several pieces of the build are pure logic that is easy to get subtly wrong and cheap to test: the `content.md` parser, the commit-graph layout, visitor hashing and bot detection, the contact schema, the certification summary. Since Next 16 the build no longer runs ESLint, so nothing checks lint on a push unless something is added.

This is an addition beyond the spec. Whether to keep it is open question 9. If the owner strikes T-019, this record is closed as not adopted.

## Decision
Proposed during planning; confirmed or revised in T-019.

- Vitest for pure logic only. No component tests and no end-to-end tests; browser checks stay manual, as CLAUDE.md describes.
- One GitHub Actions workflow on push and pull request: install with pnpm, then lint, typecheck, test and build.
- `pnpm test` joins the verification list for tasks that add logic.

## Alternatives considered
- No tests: matches the spec as written, but leaves the import script and the two public endpoints checked only by hand.
- Playwright end-to-end tests: valuable for the scroll patterns, but heavy to set up and maintain for a one-page site.
- Relying on the Vercel build alone: catches type errors, not lint or logic errors.

## Consequences
- A few tasks gain a test file (T-030, T-069, T-076, T-080).
- The CI build needs the same environment variables as any build, because `src/env.ts` fails fast. T-019 settles whether CI uses repository secrets or skips the build step and leaves it to Vercel.
- A red workflow does not block Vercel from deploying; it is a signal, not a gate, unless branch protection is added later.
