# 0019: Contact pipeline

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-080

## Context
The spec asks for a contact form with name, email and message, server-side validation, a honeypot and a rate limit, sent through Resend to the owner's public email. CLAUDE.md specifies a Next.js route handler. Resend's free tier allows 100 emails a day and 3,000 a month (checked 2026-11-16), so an unprotected endpoint could exhaust it.

## Decision
Proposed during planning; confirmed or revised in T-080.

- **One endpoint**, `/api/contact`, accepting JSON.
- **One schema.** A zod schema in `src/lib/contact.ts` is used by both the form and the endpoint, with length limits on every field.
- **Honeypot.** A hidden field that people never fill. If it has a value the endpoint answers 200 and sends nothing, so a bot gets no signal.
- **Minimum fill time.** Submissions faster than a person could type are dropped the same way.
- **Rate limit.** A sliding window per visitor hash in Redis, plus a daily cap across all visitors set below Resend's daily allowance. The numbers are fixed in T-080.
- **Sending.** Plain-text email through Resend, to the address in the environment, with reply-to set to the sender.
- **Nothing is stored.** Messages are not written to Redis or anywhere else.
- **Failure.** Typed error responses; the form maps them to fields, shows a wait message on a rate limit, and always offers a mailto link when sending fails.

The sender address depends on open question 7. With a verified domain it is an address on that domain. Without one, Resend's shared test sender is the only option; its delivery limits are checked in T-080.

## Alternatives considered
- A CAPTCHA or Turnstile: stronger against bots, but it adds an outside script and friction for real visitors.
- A hosted form service: little code, but another account and visitors' messages passing through a third party.
- A Server Action: fine technically; CLAUDE.md names a route handler.
- A mailto link only: no abuse risk, but the spec asks for a form.

## Consequences
- The honeypot and timing checks stop simple bots only. If abuse appears, a CAPTCHA is the next step and needs a new record.
- The daily cap means a burst of real messages on one day could be refused; the mailto link covers that case.
- The endpoint needs Redis (T-076) and three environment variables before it can be built.
- Without a verified sending domain, mail may land in spam or be limited to the account's own address.
