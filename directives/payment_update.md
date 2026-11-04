# Payment / Pricing Update

## What this workflow is

Changing a price, adding or editing a payment option (PayPal, Venmo, Cash App), or fixing payment links on any enrollment page. Higher-stakes variant of a portal edit — money paths must never be half-updated.

## Prerequisites

- `context/company.md` (current offer ladder and prices)
- `directives/portal_page_update.md` (this directive adds to it, not replaces it)

## Inputs

| Field | Required | Description |
|---|---|---|
| Offer | yes | Which offer the payment change applies to |
| New price / link | yes | Exact amount and/or payment URL |
| Scope | yes | Which pages mention this offer's price or payment |

## Process

1. **Grep every HTML file** for the offer's current price and payment links before changing anything — build the full list of touchpoints.
2. **Update all touchpoints in one commit.** A price that differs between two pages is a trust-breaking bug.
3. **Verify pre-filled amounts.** Cash App / Venmo links that pre-fill an amount must match the stated price exactly (e.g. Identity Reset Cash App link pre-fills $97).
4. **Update `context/company.md`** if the offer ladder pricing changed.
5. **Write a brain note** in `brain/decisions/` if this was a pricing decision, with the reasoning.

## Quality gates

- [ ] `grep` for the old price returns zero hits across all HTML files
- [ ] Every payment button's label, link, and pre-filled amount agree with each other
- [ ] All three payment options (PayPal, Venmo, Cash App) are visible where offered, on both light and dark backgrounds (past bug: buttons invisible on light enrollment box)
- [ ] Current prices: Identity Reset $97 · 90-Day Pathway $497 · Embodiment booking fee $50 — if the edit contradicts these, update `context/company.md` in the same commit

## Edge cases

- Only one page is asked to change but others mention the price → update all, tell the owner what else was touched.
- Payment link is a placeholder → keep it clearly marked as placeholder; never invent a live payment URL.
