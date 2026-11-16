# 0018: Visit counter and footer stats

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-076

## Context
The footer shows three public numbers. The spec defines the first as unique daily visitors, counted once per visitor per day with bots skipped; `content.md` calls it "total site visits". Which number is shown, and its label, is open question 1. The other two are the public GitHub repository count and the post count. Private analytics are separate (Vercel Web Analytics).

Checked on 2026-11-16: Upstash's free tier allows 500K commands a month with no card. Every external fetch must fail gracefully (CLAUDE.md).

## Decision
Proposed during planning; confirmed or revised in T-076.

**Counting visits**
- A small client component calls `/api/visit` once per page load. Because it needs JavaScript, most crawlers never trigger it.
- The handler rejects known bot user agents and counts only on the production deployment, not on previews or localhost.
- A visitor is identified by a SHA-256 hash of IP address, user agent, the date and a secret salt. The raw IP is never stored.
- The hash is added to a Redis set for that day. Only if it is new does the running total go up. Day sets expire after 48 hours. A day is a UTC day.
- The handler returns the total, and the footer shows it. No cookie is set.

**The other two numbers**
- Repository count: GitHub's public API for the username in the GitHub link from site settings, cached, with the last good value kept in Redis as a fallback. A token is optional and only raises the rate limit.
- Post count: a count of `post` documents in Sanity (decision 0001).

**Failure:** each slot shows a dash at a fixed width. A failed counter never breaks the page.

## Alternatives considered
- HyperLogLog per day: tiny and fast, but approximate; exact sets are small at this scale.
- A cookie or local storage flag: trusts the browser and raises consent questions.
- Counting every request on the server: counts bots, prefetches and previews, and uses far more function calls.
- A third-party counter widget: adds an outside script and gives up control of the data.
- Publishing Vercel Analytics numbers: the spec keeps those private.

## Consequences
- The number is an honest estimate: one person on two networks counts twice, and two people behind one address with identical browsers count once.
- Each new visit costs two or three Redis commands, far inside the free allowance.
- Changing the salt resets deduplication for the current day only.
- The first two tasks (T-076, T-077) cannot finish until open question 1 is answered.
