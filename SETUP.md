# Setup — Design Dept Website

Bootstrap manifest for a fresh clone. Walked by the `machine-parity` skill.

Alongside Getbumpr, this is the lowest-friction project here: **no build step, no
dependencies, no secrets.** A clone is immediately workable.

## Prerequisites

| Tool | Why | Install |
|---|---|---|
| Node | only to run a local static server via `npx` | `brew install node` |

## Clone

```bash
git clone https://github.com/khoivinh/design-dept-site.git ~/Developer/"Design Dept Website"
```

The remote is named **`design-dept-site`**; the local directory name contains spaces, so
quote it. Unquoted shell loops over `~/Developer/*` silently skip this repo.

## Secrets

**None.** No `.env`, no API keys, no CLI auth needed for development.

## Bootstrap

**Nothing to install.** There is no `package.json`, no `node_modules`, no preprocessor.

## Verify

```bash
cd ~/Developer/"Design Dept Website"
npx serve -l 8080
```

Files are served from the repo root (`index.html` is at top level — unlike Getbumpr, which
serves from `src/`). Load `localhost:8080` and click through to `contact.html`.

## Gotchas

- **`sms-consent.html` is parked and deliberately unlinked.** It is reachable by URL but has
  no navigation entry, pending a decision on whether the SMS program restarts. Do not "fix"
  the missing link.
- Contact address is `hello@designdept.com` sitewide (changed from `admin@` on 2026-07-26).
  It routes through Cloudflare Email Routing.
- A separate, dormant 2013-era repo for the *old* Design Dept site exists in iCloud at
  `Documents/Design Dept/Identity/Web Site/Code`. It is unrelated to this one, is permanently
  unpushed by decision, and should be left alone.
- **Deployment target is not recorded in this repo** — there is no `wrangler.toml`, `CNAME`,
  or CI workflow. Confirm before assuming a `git push` publishes anything.
