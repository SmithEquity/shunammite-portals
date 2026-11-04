# New Portal / Funnel Page

## What this workflow is

Building a new portal page (offer page, quiz/diagnostic, enrollment flow) that fits the existing visual house and offer ladder. Used when a new offer, lead magnet, or funnel step is added.

## Prerequisites

- All four context files loaded
- `skills/SKILL_BIBLE_shunammite_framework.md` and `skills/SKILL_BIBLE_shunammite_offers.md`
- An existing page chosen as the structural template (closest in purpose)

## Inputs

| Field | Required | Description |
|---|---|---|
| Purpose | yes | What the page does and where it sits in the offer ladder |
| Template page | yes | Which existing HTML file to mirror structurally |
| Copy source | yes | Owner-provided copy, transcript, or approved draft — never invented |
| Assets | yes | Approved images from this repo only |

## Process

1. **Place it in the ladder.** State explicitly what the page ascends from and to (e.g. audit → reset → pathway → booking). A page with no next step is an orphan.
2. **Clone the structure** of the template page: header branding, footer (email, location, Veteran/Black/Female-Owned line), disclaimer/consent blocks on any form.
3. **Draft copy in brand voice**, using only facts from context files or the owner.
4. **Wire forms** to the correct GH365 webhook — confirm the pipeline name with the owner before going live.
5. **Add the page to README.md** portal list and cross-link it from the relevant existing pages.
6. **Quality gates**, then commit.

## Quality gates

- [ ] Header/footer branding matches the other portals exactly
- [ ] Every form carries the consent + educational disclaimer language
- [ ] Page links into the ladder (at least one entry link from an existing page, one ascension link out)
- [ ] Zero fabricated testimonials, results, or numbers
- [ ] Brand voice check against `context/brand_voice.md`
- [ ] Mobile rendering checked

## Edge cases

- No suitable template exists → propose structure to the owner before building.
- Copy requires facts not in context files → placeholders + a question list, never confident fiction.
