# Design Dept Website — Status

Last updated: 2026-07-26

**Status:** In progress · **Stack:** Vanilla HTML/CSS, static (Cloudflare Pages) · No build step.

Marketing + legal site for Design Dept. Partners LLC at `designdept.com`. Five linked pages (index,
contact, privacy, terms, cancellations) plus one **unlinked** page (`sms-consent.html`), one shared
`styles.css`, one SVG logo. Each page carries its own inlined header/footer — there are no partials,
so nav and footer edits must be repeated across every file.

## Current state
- Cloned into the workspace 2026-07-25; repo is `khoivinh/design-dept-site`.
- Legal entity name corrected sitewide to **Design Dept. Partners LLC** (two wrong variants removed).
- Broken Terms-page logo fixed — it pointed at a stale `/figmaAssets/` path.
- Contact info now `hello@designdept.com` / `+1 (646) 725-1260` sitewide, replacing the gmail
  address and the 855 toll-free number. (`admin@` shipped briefly on 2026-07-25, then was swapped
  out on 2026-07-26 — it turned out to be void.)
- **SMS program removed from the linked site** — SMS sections stripped from privacy, terms, and
  cancellations, and all nav/footer/sitemap references gone.
- **`sms-consent.html` restored 2026-07-26 as a parked, deliberately unlinked page** — the channel is
  dormant but may return. No nav link, no footer link, no sitemap entry (nav/footer appear on every
  page, so any entry would surface on Contact). It names **no messaging number** and opens with an
  "not currently active" disclosure; all carrier-required disclosures are present and ready.
- Contact page reworked: SMS block out, physical address in (1328 Bergen St, Brooklyn, NY 11213).
- Repaired two truncated files (`contact.html`, `cancellations.html`) that were missing their
  closing tags — see the devlog.
- All shipped and verified live: `453bcea` (entity name + logo), `7b83aa1` (contact info, SMS
  removal, truncation repairs), `729989b` (`admin@` → `hello@`), `7c73966` (SMS page parked, contact
  meta aligned).

## Next steps
- **To reactivate SMS:** add the messaging number to `sms-consent.html`, drop the inactive-program
  disclosure, switch the conditional phrasing to present tense, re-add the sitemap entry, and decide
  separately whether it earns a nav/footer link (that would put it on Contact).
- **Decide whether to keep the 855 number's A2P 10DLC registration.** Withdrawing was the earlier
  call, but if the channel returns, keeping it may beat re-registering. The number is no longer
  published on the site either way.
- Optional: a `404.html` so missing paths actually 404 instead of returning the homepage with a 200 —
  the general form of the bug that hid both the broken logo and the deleted SMS page.
- Decide on commit identity: new commits use `982380+khoivinh@users.noreply.github.com` (repo-local),
  while all prior history uses `public@subtraction.com` — GitHub's email-privacy block forces this
  unless the setting is disabled.
- Point internal links at extensionless URLs (`/contact` not `/contact.html`) to skip the 308 hop.
- Consider a version-controlled `_headers` file instead of relying on Pages defaults.

## Pointers
- Live: <https://designdept.com> · Pages project: `design-dept.pages.dev`
- Deploy: `git push origin main` — Cloudflare Pages auto-builds. No build command, no wrangler.
- **All Cloudflare config lives in the dashboard**, not the repo. Nothing here records it but this file.
- Two edge behaviors that make live HTML differ from source, both expected: email addresses are
  obfuscated into `/cdn-cgi/l/email-protection`, and `.html` is stripped via 308 redirect.
- Missing assets return **200 + `text/html`** (Pages serves `index.html` as fallback) — check
  `content-type`, not status, when verifying assets. Same trap applies to deleted pages.
- **Never grep the live site for an email address** — obfuscation means it's never in the HTML.
  Decode `data-cfemail` instead: first hex byte is an XOR key, XOR it against each following byte.
  See `docs/2026-07-26-devlog.md`.
- Devlogs: `docs/`
