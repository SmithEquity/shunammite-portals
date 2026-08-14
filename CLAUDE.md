# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Hosted marketing/portal pages for Shunammite Enterprises, LLC (Kelly E. Smith). Every page is a **single self-contained HTML file** at the repo root — inline `<style>`, inline `<script>`, no build step, no package manager, no tests, no framework. External dependencies are limited to Google Fonts and a few CDN/base64 images.

## Build / run / deploy

- **No build, lint, or test tooling exists.** Do not add `npm`/bundler scaffolding unless asked.
- To preview: open the `.html` file directly in a browser, or `python3 -m http.server` from the repo root (needed for the local `.png` assets to resolve).
- **Deployment is GitHub Pages serving `main` at the repo root.** Live URLs are `https://smithequity.github.io/shunammite-portals/<file>.html`. Pushing to `main` publishes immediately — there is no staging environment.
- Because pages cross-link by **absolute** `smithequity.github.io` URLs (not relative paths), a link edit on one page does not follow a file rename. Renaming a file means grepping every other file for the old URL.

## Page inventory and roles

Two visual families, two functional tiers:

| File | Role | Palette family |
|---|---|---|
| `portal-access-gateway.html` | Hub — routes returning users to the right portal | plum/gold |
| `identity-reset-experience.html` | $97 paid enrollment | plum/gold |
| `becoming-whole-90day.html` | $497 paid enrollment | plum/gold |
| `becoming-whole-portal.html` | Logged-in course portal (modules/weeks) | plum/gold |
| `book-kelly-v2.html` | Booking / speaking inquiry form | plum/gold |
| `identity-audit-funnel-v2.html` | Free assessment funnel | dark/gold "deep" |
| `wholeness-wheel.html`, `purpose-clarity-quiz.html`, `breakthrough-barrier-finder.html` | Free interactive lead-capture assessments | dark/gold "deep" |

The three free assessments are near-identical siblings: same `:root` token block, same `showStep(id)` / `goBack(from)` step machine over `<div class="step" id="step-N">` with a `step-results` terminal, same lead-capture-then-score-then-POST flow. **A change to one of these usually needs to be applied to all three.**

## Core architecture

### 1. Design tokens are duplicated per file
Each file redeclares its own `:root` custom properties. There is no shared stylesheet. The plum family (`--plum #4A1942`, `--gold #C9A84C`, `--cream #FAF5ED`) and the deep family (`--deep #1A1208`, same gold, same cream) must stay internally consistent; when adjusting brand color, update every file in that family. `portal-access-gateway.html` uses a distinct numbered scale (`--plum-950`…`--gold-300`) rather than the named tokens — do not assume token names carry across files.

Typography splits the same way: plum-family pages load Cormorant Garamond + Lato + Great Vibes; deep-family pages load Playfair Display + Lato.

### 2. GH365 / LeadConnector webhooks are the only backend
All lead data leaves via a browser `fetch()` POST to a GoHighLevel (LeadConnector) Private Integration webhook:
`https://services.leadconnectorhq.com/hooks/v1/pit-<uuid>`

Assessment pages hoist the URL into a `const WEBHOOK` near the top of their `<script>`; `identity-reset-experience.html` uses `var RESET_WEBHOOK` and guards on `indexOf('https://') === 0` so an unconfigured placeholder is a no-op. Enrollment/inquiry pages inline the URL at the call site.

The POST body shape is a contract with the CRM — keep it exactly:

```js
{
  contact: { firstName, lastName, email, phone },
  tags: ['<slug>', ...],
  customFields: { /* per-page fields, plus consent_* on gated pages */ },
  pipeline: '<CRM pipeline name>',
  stage: '<CRM stage name>'
}
```

`pipeline` and `stage` strings must match pipelines that exist in GH365 — they are not free text. Current values in use: `Identity Audit`, `Identity Reset`, `Becoming Whole Enrollments`, `Book Kelly Inquiries`, `Wholeness Wheel`, `Purpose Clarity Quiz`, `Breakthrough Barrier Finder`.

Failures are swallowed (`.catch(err => console.warn(...))`) — the UI always advances so a CRM outage never blocks the user. Preserve that behavior. Note there is no server: the webhook URL is public in page source by design.

### 3. Clickwrap consent gating (legal requirement)
Every form that captures data is gated behind a checkbox wired to `cwToggle(...)`, which enables the submit/payment control only once checked. Two implementations exist — `cwToggle(cbId, btnId)` toggling `button.disabled` (most pages), and `cwToggle(cbId)` in `identity-reset-experience.html` toggling a `.disabled` class on `<a>` payment links because anchors have no `disabled` attribute.

On submit, three fields ride along in `customFields` and must not be dropped: `consent_given`, `consent_timestamp` (ISO), and `consent_version`. Versions are fixed strings tied to the checkbox copy:

- `Version A — Paid Program Enrollment` (enrollment pages)
- `Version B — Free Tool / Assessment Entry` (free assessments)
- `Version C — Booking / Speaking Inquiry` (`book-kelly-v2.html`)

The consent copy itself is legal text: 18+, links to Privacy Policy / Terms / Coaching & Educational Services Disclaimer on `shunammiteenterprises.com`, and the explicit statement that these are faith-based coaching and educational services, not clinical counseling or licensed mental health treatment. **Do not reword, trim, or "improve" this copy** — if the wording changes, `consent_version` must change with it.

### 4. Payments
Paid pages link out to third-party payment handles rather than processing anything: PayPal (`paypal.me/TheShunammite/<amount>` or `paypal.com/paypalme/...`), Venmo (`venmo.com/TheShunammite`), Cash App (`cash.app/$kellysmith2006/<amount>`). Prices are baked into the URLs — $97 for Identity Reset, $497 for the 90-Day Pathway — so a price change means editing both the displayed copy and every payment URL. The handler POSTs the lead to GH365 first, then `setTimeout(...)` redirects to the payment URL so the fire-and-forget fetch has a chance to leave.

### 5. Course portal state
`becoming-whole-portal.html` keeps progress client-side only, via `localStorage` keys set in `markMediaComplete(btn, storageKey)` and checkpoint gates (`.checkpoint-gate` / `.cg-reflection`). Its `submitCheckpoint(...)` has the GH365 POST commented out as a documented extension point — wiring it should follow the same body shape as above.

### 6. Iframe embedding
`becoming-whole-90day.html` and `becoming-whole-portal.html` open with `<meta http-equiv="X-Frame-Options" content="ALLOWALL">` plus an overflow reset, because they are embedded inside GH365 funnel pages. Keep that block first in `<head>` on those two files.

## Editing conventions

- Keep everything inline and self-contained; do not extract shared CSS/JS into separate files or introduce a build step.
- Local images (`ServicesHeroBanner1.png`, `shunammite-framework-threshold.png`, `kelly-portrait.png`) are referenced by bare relative filename and only resolve when served from the repo root. Some hero images are remote CDN URLs or base64 data URIs — check before assuming a path is local.
- Commit messages in this repo are short, imperative, and name the affected page (e.g. "Fix Identity Audit and 90-Day Pathway links on Book Kelly page").
