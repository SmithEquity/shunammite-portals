# Shunammite Enterprises — Portal Files

Hosted portal pages for Shunammite Enterprises, LLC featuring Kelly Smith Speaks.

## Portals
- **Shared Access Gateway** — `portal-access-gateway.html`
- **Identity Reset Experience** — `identity-reset-experience.html`
- **Becoming Whole 90-Day Enrollment** — `becoming-whole-90day.html`
- **Becoming Whole Course Portal** — `becoming-whole-portal.html`
- **Book Kelly** — `book-kelly-v2.html`
- **Identity Audit Funnel** — `identity-audit-funnel-v2.html`

## NotebookLM MCP Server

This repo's `.mcp.json` registers the [NotebookLM MCP server](https://www.npmjs.com/package/notebooklm-mcp), which lets Claude Code query the **The Shunammite's Memory** notebook (the Shunammite Framework knowledge base) directly.

- **Notebook share link:** https://notebooklm.google.com/notebook/bac5ba7d-0d00-48d2-bf24-58b99e7986ba

### One-time setup (on your local machine)

Querying the notebook requires a Google sign-in, so the full workflow runs locally:

1. Open a Claude Code session in this repo — it auto-detects `.mcp.json` and prompts you to approve the `notebooklm` server. (Or install it globally: `claude mcp add --scope user notebooklm -- npx notebooklm-mcp@latest`)
2. Ask Claude to run the server's `setup_auth` tool. A browser window opens — sign into Google once; the session is saved for future use.
3. Ask Claude to register the notebook using the share link above (the `add_notebook` tool), e.g. *"Add my NotebookLM notebook The Shunammite's Memory: \<share link\>"*.
4. From then on: *"Ask The Shunammite's Memory about …"* works in any session — questions are answered by Gemini grounded in the notebook's sources, and you can also add sources or generate Audio Overviews.

> **Note for remote (cloud) Claude Code sessions:** the environment's network policy must allow `notebooklm.google.com` and `accounts.google.com` for the server to reach NotebookLM; otherwise use a local session.
