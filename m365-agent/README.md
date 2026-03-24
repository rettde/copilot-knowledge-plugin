# Compound Knowledge — M365 Copilot Agent

A Declarative Agent for Microsoft 365 Copilot that provides AI-powered workflows for knowledge work. Rebuilt from the [Compound Knowledge Plugin](https://github.com/rettde/compound-knowledge-plugin) for Claude Code.

## The Loop

```
Brainstorm --> Plan --> Confidence (anytime) --> Review --> Work --> Compound
```

Each cycle makes the next one faster. The Plan workflow searches for past learnings saved by Compound. Knowledge compounds.

## Workflows

| Workflow | What it does |
|---|---|
| **Brainstorm** | Brain dump, pull references, find the shape of the problem |
| **Plan** | Structure into an actionable plan grounded in past learnings |
| **Confidence** | Gut-check what you know vs. don't (callable at any point) |
| **Review** | Strategic alignment + data accuracy check |
| **Work** | Execute the plan, produce deliverables |
| **Compound** | Save learnings for next time |

## Prerequisites

- [Microsoft 365 Copilot license](https://www.microsoft.com/microsoft-365/copilot)
- [Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) for VS Code (v5.0+)
- [Node.js](https://nodejs.org/) 18+
- Microsoft 365 developer tenant (or production tenant with sideloading enabled)

## Setup

### 1. Configure SharePoint (optional but recommended)

Create a SharePoint site for knowledge storage:

1. Create a site called "CompoundKnowledge" (or any name)
2. Create two document libraries:
   - `plans` — for plan documents
   - `knowledge` — for saved learnings
3. Update `env/.env.dev` with your SharePoint domain and site name:

```
SHAREPOINT_DOMAIN=yourtenant.sharepoint.com
SHAREPOINT_SITE=CompoundKnowledge
```

If you skip this step, the agent still works — it just won't have persistent knowledge sources. You can paste content directly.

### 2. Provision and deploy

Open this folder in VS Code with Teams Toolkit installed:

```bash
cd m365-agent
```

Then:

1. **Sign in** — Click "Sign in to Microsoft 365" in the Teams Toolkit sidebar
2. **Provision** — Press `F5` or click "Provision" in the Teams Toolkit sidebar
3. **Preview** — The agent opens in Microsoft 365 Copilot

Or use the CLI:

```bash
# Install Teams Toolkit CLI
npm install -g @microsoft/teamsapp-cli

# Provision
teamsapp provision --env dev

# Preview in browser
teamsapp preview --env dev
```

### 3. Publish (for your organization)

To make the agent available to your organization:

1. Click "Publish" in the Teams Toolkit sidebar
2. An admin approves the app in the Teams admin center
3. The agent appears in Microsoft 365 Copilot for all licensed users

## Usage

Open Microsoft 365 Copilot and mention the agent or select it from your agents list. Then:

**Brainstorm:**
> "Brainstorm: I need to figure out our Q2 content strategy"

**Plan:**
> "Plan: Structure a campaign plan for the product launch"

**Review:**
> "Review: Check this plan for strategic alignment before I share it"

**Compound:**
> "Compound: Save what we learned from this session"

The agent detects which workflow you need from your message. You can also use the conversation starters.

## Knowledge Storage

| Feature | How it works |
|---|---|
| **Past learnings** | Stored as markdown files in the SharePoint `knowledge` library |
| **Plans** | Stored in the SharePoint `plans` library |
| **Search** | The agent searches SharePoint via Microsoft Graph |
| **Format** | Same YAML frontmatter + markdown format as the VS Code version |

### Knowledge file format

```markdown
---
type: insight
tags: [trials, conversion, campaigns]
confidence: high
created: 2026-02-15
source: Q1 trial campaign analysis
---

# Trial Conversion Timing

Extended trial periods (30 days vs 7 days) increase conversion rate
but delay revenue recognition. Net positive after 60 days.
```

## Differences from Other Versions

| Feature | VS Code (GitHub Copilot) | M365 Copilot Agent |
|---|---|---|
| Invocation | `#kw-brainstorm` | "Brainstorm: ..." |
| Workflows | 11 separate prompt files | Single agent, all workflows |
| Knowledge store | Local `docs/knowledge/` | SharePoint document library |
| File operations | Direct file write | SharePoint via Graph |
| Deployment | Copy `.github/` folder | Teams Toolkit provision |
| Scope | Per-repository | Per-organization |

## Project Structure

```
m365-agent/
├── appPackage/
│   ├── manifest.json              # Teams app manifest
│   ├── declarativeAgent.json      # Agent config + capabilities
│   └── instructions.md            # All 6 workflows (the brain)
├── env/
│   └── .env.dev                   # Environment variables
├── teamsapp.yml                   # Teams Toolkit config
└── README.md                      # This file
```

## License

MIT
