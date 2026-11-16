# 0020: SEO and share image

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-083

## Context
The spec asks for per-page metadata, an Open Graph image, `sitemap.ts`, `robots.ts` and Person JSON-LD, with a Lighthouse SEO score of 100. The SEO title, description and keywords are editable in Sanity. The site is a single page plus a 404 page and the Studio; projects have no pages of their own (decision 0003).

## Decision
Proposed during planning; confirmed or revised in T-083.

- **Metadata** is generated from the SEO fields in `siteSettings`: title, description, keywords, canonical URL, Open Graph and Twitter tags. The base URL comes from `NEXT_PUBLIC_SITE_URL`.
- **The share image is generated**, not uploaded. `opengraph-image.tsx` draws the name and title line from Sanity in the display font over the scene still, at 1200 x 630.
- **Sitemap** lists the home page. **Robots** allows the site, disallows `/studio` and `/api`, and names the sitemap. `/studio` is also marked `noindex`.
- **Person JSON-LD** is built only from fields that exist in Sanity: name, title line, site URL, social links and location. Whether the current employer is included is settled in T-084.
- **Search Console** is verified by DNS or by a meta tag, whichever fits the domain setup (T-093).

## Alternatives considered
- An uploaded share image in Sanity: full control over the picture, but it goes stale when the name or title changes, and it is one more thing to produce.
- No share image: links to the site would preview as plain text.
- Hand-written meta tags: the framework's metadata support covers this with less risk of mistakes.

## Consequences
- The share image updates when the settings change, through the same cache tag as the page.
- The generator needs the display font in a format it accepts and the still from the asset brief; both are confirmed in T-083.
- A long name or title must still fit; T-083 checks the layout with the real text.
- No project has its own search or share entry in v1.
