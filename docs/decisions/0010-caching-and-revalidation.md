# 0010: Caching and revalidation

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-027

## Context
The spec requires on-demand revalidation from a Sanity webhook, and the acceptance criterion is that every CMS change appears on the live site within 60 seconds with no redeploy. The site is one page with one editor and little traffic.

Checked against the Next.js and Sanity docs on 2026-11-16:
- In Next 16, `revalidateTag` takes a second argument. With `'max'`, the first request after a change is still served the old content while a fresh render runs. With `{ expire: 0 }`, the next request waits for the fresh render.
- `parseBody` from `next-sanity/webhook` validates the webhook signature and waits about 3 seconds for Sanity's content to settle.
- Sanity recommends `defineLive` for most apps. Since next-sanity 13 it no longer guarantees immediate updates without an extra function.
- Two caches sit in the path: Sanity's API CDN and Next's data cache.

## Decision
Proposed during planning; confirmed or revised in T-027.

- The home page is rendered statically. Next's Cache Components mode stays off; caching uses `fetch` options.
- One helper, `sanityFetch` in `src/sanity/fetch.ts`, wraps the client's fetch. It caches each query under a tag named after the document type, with a one-hour timed refresh as a safety net.
- The client used for these fetches sets `useCdn: false`, so a re-render reads fresh data from the API. These fetches happen only on a re-render, so the volume is tiny.
- `/api/revalidate` checks the signature with `parseBody`, then calls `revalidateTag(<document type>, { expire: 0 })`.
- The webhook in Sanity fires on create, update and delete of published documents of the site's types.

## Alternatives considered
- Sanity Live (`defineLive`): Sanity's default, but it holds a connection open per visitor and needs more setup than one page and one editor justify.
- `revalidateTag(tag, 'max')`: Next's recommended profile. On a quiet site the owner would publish, reload, and still see the old page once.
- `revalidatePath('/')`: enough for the home page, but `/resume`, the share image and the 404 page would each need listing.
- Timed refresh only: cannot reach 60 seconds without refreshing constantly.
- A deploy hook: is a redeploy, which the spec rules out.
- Cache Components (`'use cache'` with `cacheTag`): the newer model, with no benefit for a single static page.

## Consequences
- The first visitor after an edit waits for one fresh render; everyone else gets cached HTML.
- If a webhook is missed, the change appears within the hour. The runbook covers checking the webhook log.
- Every query must pass the right tag, or its content will not update on publish. The helper makes the tag a required argument.
- To confirm in T-027: that Next accepts a timed refresh and tags on the same fetch (Sanity's own example helper treats them as exclusive), and that the Free plan includes webhooks.
