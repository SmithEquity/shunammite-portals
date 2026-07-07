# Portal Page Update

## What this workflow is

Editing an existing portal HTML page: copy changes, link fixes, styling adjustments, new sections. These pages are production — this is the most repeated workflow in the business (see git history: link fixes, button visibility, label matching).

## Prerequisites

- Context loaded: `context/company.md`, `context/core_values.md`, `context/brand_voice.md`
- `skills/SKILL_BIBLE_shunammite_offers.md` if the edit touches offer copy, pricing, or gating rules

## Inputs

| Field | Required | Description |
|---|---|---|
| Page file | yes | Which `*.html` file to edit |
| Change request | yes | What should be different, in plain English |
| Approved assets | if visual | Only images already in this repo |

## Process

1. **Read the page first.** Understand the existing structure, styles, and any inline JS before editing.
2. **Make the edit** matching the page's existing conventions (inline CSS patterns, class names, section structure).
3. **Cross-page sweep.** If the change touches an offer name, price, link, or rule, grep every other portal page for the same string and update all of them (past bug: payment button labels didn't match across pages).
4. **Run quality gates** below.
5. **Commit** with a clear message describing the visible change.

## Quality gates

- [ ] All internal links between portals resolve to files that exist in this repo
- [ ] No fabricated numbers, testimonials, or names introduced
- [ ] Copy passes `context/brand_voice.md` (no banned words, tone matches)
- [ ] Offer copy does not contradict gating rules (coaching session unlock, pricing)
- [ ] Consent/disclaimer language on forms is intact and unmodified
- [ ] Page renders without console errors (open in a browser to check)

## Edge cases

- Change conflicts with a gating rule → fix the copy, never the rule; flag it to the owner.
- Requested image is not in the repo → stop and ask; off-brand generated artwork is banned.
- Edit touches a live webhook URL → confirm with the owner before changing; these are wired to GH365 pipelines.
