# CLAUDE.md — Subhranil Raha Portfolio

Personal portfolio told as a developer story: one commit's journey from `git init` to production.
Read `docs/specs/0001-portfolio.md` for WHAT we build, `docs/tasks/TASKS.md` for WHERE we are,
`docs/decisions/` for WHY, and `docs/progress.md` for where the last session stopped.

## Stack
- Next.js (App Router) + TypeScript (strict) + Tailwind CSS
- 3D: three.js via react-three-fiber + drei; scroll motion: GSAP ScrollTrigger + Lenis
- CMS: Sanity (Studio embedded at `/studio`)
- Blog: Hashnode GraphQL API (read only)
- Stats: Upstash Redis (public visit counter), Vercel Web Analytics (private)
- Contact: Next.js route handler + Resend
- Hosting: Vercel
- Package manager: pnpm

## Workflow rules (always follow)
1. Work on ONE task from `docs/tasks/TASKS.md` at a time. Plan it, wait for approval, then build.
2. Mark the task "In progress" when you start and "Done" (with the date) when its "done when" check passes.
3. Never silently expand scope. New work you discover goes into TASKS.md as a new task, not into the code.
4. Any significant technical choice gets a decision record in `docs/decisions/` (copy `0000-template.md`).
   To change a decision, write a new record that supersedes the old one; never edit history.
5. Commit after each task: `T-012: short description`. One task per commit.
6. At the end of every session, update `docs/progress.md`: done, half-finished, next.
7. If a requirement is unclear, ask. Do not guess content, names, dates or links.

## Code conventions
- Server Components by default. Use `"use client"` only for interactivity, 3D and animation.
- No hard-coded copy, dates or links in components. All content comes from Sanity
  (or Hashnode for posts). The only exception is the fixed UI chrome (button labels, aria text).
- All Sanity queries live in `src/sanity/queries.ts` and are typed (Sanity TypeGen).
- Environment variables are read through one typed module (`src/env.ts`) that fails fast if any are missing.
- Never read, print or commit `.env*` files except `.env.example`.
- Components: one per file, PascalCase, colocated styles via Tailwind. No `any`.
- Every external fetch handles errors and has a sensible fallback (a section never crashes the page).
- Images go through `next/image` (or the Sanity image URL builder) with width, height and alt text.

## Design rules
- Inspired by the *method* of mengto.github.io/kage (one scroll-driven camera path, chapter shots,
  pinned foreground cutouts, restraint), never its code, artwork, layout copy or Japanese motif.
- Palette: ink-slate background, off-white text, ONE amber accent, muted steel for secondary.
  No purple gradients, neon grids, glassmorphism cards or emoji in UI.
- Type: one display font for headings, one monospace font for labels, captions and commands. Self-hosted via `next/font`.
- Humor: at most one small monospace caption per section, from the CMS. Never in headings, facts or About text.
- Experience = commit-graph scroll. Projects = horizontal deployment track.
  Writing = stacked-card scroll. Certifications = CI-checks panel.
  No other section may reuse these four patterns.
- All images come from Sanity via the image URL builder: responsive sizes, WebP/AVIF, blur placeholder,
  required alt text, lazy-loaded below the fold. Reduced-motion users get lists, not pinned scrolls.
- Accessibility: every animation respects `prefers-reduced-motion`; all text is real HTML (not in the canvas);
  keyboard navigable; visible focus states; WCAG AA contrast.
- Mobile gets the same 3D experience at adaptive quality; only reduced-motion users and devices
  that fail the performance monitor get the static scene image. Test every 3D task on a real phone.

## Skills
Project skills live in `.claude/skills/`. Use `threejs`, `scroll-world-storytelling` and
`cinematic-scroll-storytelling` for the scene and scroll, `scroll-progress-timeline` for the
experience/projects progress UI, `pointer-trail-emitter` and `ambient-section-particles` for effects,
`editorial-portfolio-chapters` for layout, `optimize-web-animations` before finishing any 3D task,
and `audit-reference-originality` before launch.

## Verification (run before marking any task Done)
- `pnpm lint` and `pnpm typecheck` pass with zero errors
- `pnpm build` succeeds
- The changed page was opened in the browser and checked at 375 px and 1440 px widths
- For 3D or animation tasks: steady 60 fps on desktop, no layout shift, reduced-motion path works
