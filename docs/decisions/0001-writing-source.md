# 0001: The Writing section reads post cards from Sanity

- **Status:** Accepted
- **Date:** 2026-11-16
- **Task:** T-001

## Context
The spec planned to pull the latest posts, with cover, reading time, tags and a post count, from the Hashnode GraphQL API. On 2026-05-13 Hashnode ended free API access: "Every API request, queries and mutations, now requires a Pro plan on your publication." On 2026-11-16 the endpoint `gql.hashnode.com` redirected to that announcement. The spec also requires free tiers only.

## Decision
Chosen by the owner on 2026-11-16.

Posts are a Sanity document type, `post`: title, link, publish date, reading time in minutes, tags and an optional cover image with alt text. The Writing section shows the latest four and ends with a card that links to the Hashnode publication URL from site settings. The footer's post count is the number of `post` documents.

There is no Hashnode API integration and no hourly refresh. Posts update through the same webhook as all other content (decision 0010).

## Alternatives considered
- Hashnode GraphQL with a Pro plan: keeps posts automatic, but breaks the free-tier rule.
- Hashnode RSS feed: a plain request to a Hashnode-hosted feed returned HTTP 429 from a bot checkpoint, so free server-side access is unverified. Working around a checkpoint is not acceptable.
- Moving the blog to a platform with a free read API: a far bigger change than the problem warrants.

## Consequences
- Adding a post takes about a minute in Studio after publishing it on Hashnode. The runbook (T-094) covers the steps.
- The model does not care where a link points. Whether cards may link to posts outside Hashnode is open question 2.
- The section must render cleanly with fewer than four posts and with none.
- The spec, CLAUDE.md and `content.md` still describe the API until T-001 corrects them.
- The source sits behind one query, so an automatic source can replace it later through a new record.
