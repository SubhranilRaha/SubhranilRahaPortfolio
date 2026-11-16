# Spec 0001: Portfolio v1

## Problem
Recruiters and engineers need to understand, in under a minute, who Subhranil is, what he has
built, and where he is heading, and to contact him or download his resume. The owner must be able
to update resume, skills, experience, certifications and projects without touching code.

## Story
The page follows one commit from `git init` to production. Each section is a chapter:

| # | Chapter label | Section |
|---|---|---|
| – | `provisioning` | Loading screen |
| – | – | Nav bar (sticky) with section links and a Resume download button |
| 00 | `git init` | Hero |
| 01 | `dependencies` | Technical skills |
| 02 | `README.md` | About |
| 03 | `git log` | Experience |
| 04 | `deployments` | Projects |
| 05 | `docs/` | Writing (Hashnode) |
| 06 | `checks passed` | Certifications & training |
| 07 | `TODO:` | Where I'm heading |
| 08 | `open a pull request` | Contact |
| – | `exit 0` | Footer |

A fixed Three.js canvas sits behind the HTML. Scrolling drives one continuous camera path that
rises "up the stack": terminal → toolchain → pipeline → cloud network → cluster → GPU racks.

## In scope
- All sections above, content from `content.md` imported into Sanity
- CMS-editable: site settings (name, title, about, socials, SEO), resume PDF, skill groups,
  experience, projects (cover image required + gallery up to 6), certifications, roadmap milestones,
  section captions
- Experience: pinned commit-graph scroll (EY on `main`, other roles as merging branches)
- Projects: pinned horizontal deployment-track scroll with a pipeline progress bar
- Writing: latest Hashnode posts, revalidated automatically; cards link to Hashnode
- Footer stats: unique daily visitors (counted once per visitor per day, bots skipped),
  public GitHub repo count, Hashnode post count
- Contact form: name, email, message; server-side validation, honeypot and rate limit; sent via Resend
- Custom cursor on fine-pointer devices only
- Loader with real progress (assets loaded), max 3 s before content shows
- SEO: per-page metadata, Open Graph image, `sitemap.ts`, `robots.ts`, Person JSON-LD
- Custom 404 page
- On-demand revalidation from a Sanity webhook so edits appear without a redeploy

## Out of scope (v1)
- Authentication, comments, likes, newsletter
- Multi-page blog hosted on this site (posts stay on Hashnode)
- Dark/light theme toggle (dark only)
- Internationalisation
- 3D anywhere except the landing scroll scene

## Acceptance criteria
- Every CMS field change appears on the live site within 60 s, with no redeploy
- Resume button always downloads the latest PDF uploaded in Sanity
- Lighthouse (mobile): Performance ≥ 85, Accessibility ≥ 95, Best Practices ≥ 95, SEO = 100
- Largest Contentful Paint < 2.5 s on a mid-range phone; the 3D bundle is lazy-loaded
- Works with JavaScript-driven 3D disabled or reduced motion on: all content readable
- No console errors; no secrets in the repo; all env vars documented in `.env.example`
- Originality audit against the Kage reference passes

## Non-functional
- Free tier only: Vercel Hobby, Sanity Free, Upstash Free (no card), Resend Free
- Phone number never appears on the site
- Client names from EY work appear only if confirmed (see `[CHECK]` items in `content.md`)
