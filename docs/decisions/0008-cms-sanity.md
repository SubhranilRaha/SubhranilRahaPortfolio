# 0008: Sanity as the CMS, with the Studio embedded at /studio

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-020

## Context
The owner must be able to update the resume, skills, experience, certifications, projects and posts without touching code, on free tiers only. CLAUDE.md already names Sanity with the Studio embedded at `/studio`; this record gives the reasons and the setup.

Checked on 2026-11-16: Sanity 6.23 and next-sanity 13.4 work with Next 16 and React 19.2 or later. On the Free plan quotas are hard caps with no overage, and datasets are public.

## Decision
Proposed during planning; confirmed or revised in T-020.

- Sanity is the only content store. One project, one dataset named `production`.
- The Studio is mounted inside the Next.js app at `/studio` through next-sanity, with its own layout: no site nav, no smooth scrolling, no scene, no analytics, and marked `noindex`.
- Types are generated from the schema and the queries with Sanity TypeGen (T-027).
- Published content is read without a token. A write token exists only for the import script and stays on the owner's machine.

## Alternatives considered
- A separately hosted Studio (`sanity deploy`): keeps Studio code out of the app, but adds a second site to manage and CLAUDE.md asks for `/studio`.
- Payload: capable and self-hosted, but needs a database, which means another service to keep on a free tier.
- Contentful or similar hosted CMS: workable, with tighter free limits and less control over the editing interface.
- A git-based CMS: editing means commits and redeploys, which the spec rules out ("no redeploy").
- Markdown or JSON in the repo: requires touching code.

## Consequences
- The dataset is public: anyone with the project id can read published content. Nothing private may be published. Drafts are handled in T-031.
- The Studio brings peer dependencies (`styled-components`, a React range) that constrain upgrades.
- The Studio's bundle loads only on `/studio`, but it lengthens builds.
- Each site address (local, Vercel, the final domain) must be added as a CORS origin in Sanity before the Studio works there.
- If a free quota is reached, the affected feature is blocked until the month resets. Exact quotas are checked in T-020.
