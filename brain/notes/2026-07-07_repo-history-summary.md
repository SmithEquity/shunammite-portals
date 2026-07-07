# How the portal system was built (Apr–Jul 2026)

**Source:** git history, summarized 2026-07-07

- **2026-04-10** — Initial commit: four portal files. GH365 webhooks wired into Book Kelly and Identity Audit.
- **2026-04-19** — Identity Audit questionnaire flow fixed and hardened.
- **2026-05-25** — Book Kelly wired to live GH365 webhook; pipeline named "Book Kelly Inquiries."
- **2026-06-22/23** — Three interactive lead-capture artifacts added (Purpose Clarity Quiz, Breakthrough Barrier Finder, Wholeness Wheel), Kelly portrait + personal quotes added, consent/privacy language added to all three forms, Shunammite Framework image swapped in.
- **2026-07-06** — Big compliance + payments day: clickwrap consent on all portals, coaching-education disclaimer links, Identity Reset enrollment form built and wired to GH365, footer emails repaired, Venmo/Cash App added (see [[2026-07-06_add-venmo-cashapp-payment-options]]).
- **2026-07-07** — Second brain initialized (see [[2026-07-07_adopt-second-brain-architecture]]).

Pattern worth noticing: nearly every fix-commit is a cross-page consistency issue (links, labels, footers). That is exactly what the directives' cross-page sweep gates now catch.

Related: [[2026-07-07_portal-file-map]]
