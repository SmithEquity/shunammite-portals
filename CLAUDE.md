# Shunammite Enterprises — Business Brain

This folder is the operating system for Shunammite Enterprises, LLC (Kelly E. Smith / Kelly Smith Speaks). An AI agent reads this file at the start of every session, loads context in the order below, and does real work inside this folder.

## Architecture (DOE)

Three layers. Respect the boundaries.

- **DIRECTIVES** (`directives/*.md`) — What to do: step-by-step SOPs in plain English, one file per workflow, each ending in quality gates.
- **ORCHESTRATION** (you, the AI) — The decision maker: parse the request, load context, pick the matching SOP, execute, check quality, deliver.
- **EXECUTION** (`execution/`) — How it gets done: deterministic scripts for API calls, file operations, and data processing. If a step should produce the same output every time given the same input, it belongs in a script. If it requires judgment, taste, or reading context, it stays with the AI.

## Directory map

| Path | Purpose |
|---|---|
| `CLAUDE.md` | This file — the constitution, read first every session |
| `context/` | Who we are: identity, voice, values, owner |
| `directives/` | SOPs: what to do, step by step |
| `execution/` | Scripts: the deterministic work |
| `skills/` | Deep domain expertise files (`SKILL_BIBLE_*.md`) |
| `clients/` | One folder per booking client / engagement |
| `brain/` | Dated, linked notes: decisions, history, lessons |
| `sources/` | Raw exports the brain is mined from (transcripts, threads) |
| `.tmp/` | Scratch space for drafts — never committed |
| `*.html`, `*.png` | **The live portal pages** — the delivery layer this business ships. Treat as production. |

## Context loading priority

1. `context/company.md` → Always first (who we are)
2. `context/core_values.md` → Always (how we operate; check work against it)
3. `context/brand_voice.md` → For any content creation
4. `clients/{name}/*.md` → For client-specific work
5. `skills/` relevant files → Domain expertise for the task
6. `directives/` the SOP → The workflow itself

## Orchestration flow

Parse the request → find the matching directive → load context per the priority above → execute → run the directive's quality gates → deliver.

## Standing rules

1. **Never fabricate numbers, testimonials, results, or client names.** Placeholders plus a question beat confident fiction every time.
2. **The portal HTML files are production.** Any edit to them must pass the quality gates in `directives/portal_page_update.md`. Commit every change with a clear message; git is the undo button.
3. **Respect the offer gating rules** (see `skills/SKILL_BIBLE_shunammite_offers.md`): the included Identity Reset coaching session unlocks only after the Identity Audit and Days 1–2 are complete. Purchase alone is not proof of readiness. Never write copy that contradicts this.
4. **Stay inside the visual house.** Use approved brand imagery (`ServicesHeroBanner1.png`, `kelly-portrait.png`, `shunammite-framework-threshold.png`), never off-brand generated artwork.
5. **Date everything in the brain.** Filenames carry dates: `YYYY-MM-DD_slug.md`. An undated fact is a landmine the first time the business changes its mind.
6. **API keys live in `.env` only.** Never committed, never pasted into files.

## Self-annealing protocol

After every task:
- If an error occurred → fix the script and update the directive.
- If a better approach was found → update the relevant skill file.
- If a new edge case appeared → add it to the SOP's edge cases section.

Nothing breaks the same way twice, because every failure becomes an edit to the system.
