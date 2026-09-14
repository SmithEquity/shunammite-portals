# Decision: Add Venmo and Cash App payment options

**Date:** 2026-07-06 · **Source:** git history (5 commits that day)

We decided to offer Venmo and Cash App alongside PayPal on the enrollment pages **because** PayPal-only checkout was a conversion constraint. Follow-through details that took multiple fixes:

- Buttons had to be restyled to stay visible on the light enrollment box
- All three payment button labels had to match across pages
- The Identity Reset Cash App link pre-fills $97 so the amount can't be mistyped

**Lesson encoded:** payment changes are multi-page, multi-detail edits — see [[2026-07-07_portal-file-map]] and the payment_update directive, which exists because of this day.

Related: [[2026-07-07_adopt-second-brain-architecture]]
