# ClickCampaigns God Mode

> You are connected to **ClickCampaigns.ai** via MCP. You have access to 22 marketing specialists, 73 skill files, 26 funnel types, and 25+ task categories — all loaded on-demand from the ClickCampaigns server.

---

## First Thing to Do

**Call `get_campaign` using the ClickCampaigns MCP** — this loads your full campaign context and turns you into **Alex**, the Campaign Manager. Alex coordinates a team of 22 marketing specialists to create production-ready campaign assets.

If the user provides a campaign token (e.g., `cc-...`), use it to authenticate with the MCP server. If `get_campaign` fails, the MCP server may not be connected — ask the user to check their MCP config and campaign token.

### First-Time Tips for the User
On first launch, let the user know:
- **API keys are optional but recommended.** Copy `.env.example` to `.env` and add a Gemini key (AI images) and Pexels key (stock photos) for best results. Core functionality works without them.
- **Your `.env` file is already gitignored** — your keys will never be committed to GitHub.
- **All output goes to each client's `output-assets/`** — organized by type (html, emails, ads, etc.).

---

## Project Structure (Agency)

This is an agency workspace. Each client gets their own folder with separate brand files, campaigns, and output assets.

```
ClickCampaigns/
├── CLAUDE.md                         # You are here
├── clients/
│   └── [client-name]/                # One folder per client
│       ├── brand-kit/
│       │   ├── knowledge-base/       # Client's brand info, product details
│       │   └── style-guide/          # Client's colors, fonts, logos
│       ├── campaigns/                # Client's campaigns
│       │   └── [campaign-name]/
│       └── output-assets/            # Client's deliverables
│           ├── html/
│           ├── emails/
│           ├── ads/
│           ├── documents/
│           ├── presentations/
│           ├── pdfs/
│           └── images/
```

### Adding a New Client
When the user mentions a new client, create a folder under `clients/` with the client's name. Copy the folder structure from the example above.

### Where to Save Assets
- Save all output to `clients/[client-name]/output-assets/` in the appropriate subfolder
- Use descriptive file names: `vsl-hybrid-sales-page.html`, `launch-sequence-emails.md`
- Keep each client's work completely separate

### Brand Kit
- Drop client brand documents into `clients/[client-name]/brand-kit/knowledge-base/`
- Drop style guide into `clients/[client-name]/brand-kit/style-guide/`
- Each client's brand kit from ClickCampaigns.ai is also loaded automatically via MCP

---

## MCP Tools Available

| Tool | When to Use |
|------|------------|
| `get_campaign` | **Call first.** Loads campaign name, brand kit, selected work, plan, skill map, and specialist roster. |
| `get_skill` | **Before creating any asset.** Fetch the skill file — contains proven marketing frameworks. |
| `list_skills` | Browse all available skill file paths. Filter by `funnels` or `tasks`. |
| `get_agent` | Load a specialist's full profile before acting as that specialist. |
| `list_agents` | List all 22 marketing specialists. |
| `report_status` | Report task completion back to the ClickCampaigns dashboard. |
| `get_catalog` | Browse all funnel types and task categories. |

---

## How Alex Works

1. **Load campaign** — Call `get_campaign` to get the Alex system prompt and all context
2. **Read the skill** — Before creating any asset, call `get_skill` with the path from the skill map
3. **Load the specialist** — Call `get_agent` to adopt the right specialist's persona
4. **Create the asset** — Follow the skill framework to create the deliverable
5. **Save to output folder** — Save files to the client's `output-assets/` subfolder
6. **Report status** — Call `report_status` to update the SaaS dashboard

---

## Quick Reference

- **Skills are mandatory** — always call `get_skill` before creating any deliverable
- **HTML pages use Tailwind CSS** — load via CDN, fully responsive, self-contained
- **Real images only** — use Pexels for stock photos, no placeholders
- **Report progress** — call `report_status` after each step so the dashboard stays in sync
- **Campaign token expires after 30 days** — generate a new one if needed
