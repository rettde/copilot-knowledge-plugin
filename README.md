# Compound Knowledge for GitHub Copilot

Workflows for knowledge work that compounds over time. Rebuilt for [GitHub Copilot](https://github.com/features/copilot) from the original [Compound Knowledge Plugin](https://github.com/EveryInc/compound-knowledge-plugin) by [Every, Inc.](https://every.to) for Claude Code.

Read the story: [How to Build a Command Center That Keeps You Sane](https://every.to/p/the-agent-that-saved-my-brain)

## The Loop

```
#kw-brainstorm  --> Brain dump, pull references, find the shape
#kw-plan        --> Structure into an actionable plan
#kw-confidence  --> Gut-check what you know vs. don't (callable at any point)
#kw-review      --> Strategic alignment + data accuracy check
#kw-work        --> Execute the plan, produce deliverables
#kw-compound    --> Save learnings for next time
```

Each cycle makes the next one faster. `#kw-plan` searches `docs/knowledge/` for past learnings saved by `#kw-compound`. Knowledge compounds.

## Install

Copy the `.github/` directory into the root of any project:

```bash
# Clone this repo
git clone https://github.com/rettde/copilot-knowledge-plugin.git

# Copy the .github folder to your project
cp -r copilot-knowledge-plugin/.github /path/to/your/project/
```

Or manually copy the files:

```
your-project/
├── .github/
│   ├── copilot-instructions.md          # Global Copilot instructions
│   └── prompts/                         # Reusable prompt files
│       ├── kw-brainstorm.prompt.md      # Brain dump and organize
│       ├── kw-plan.prompt.md            # Structure into a plan
│       ├── kw-confidence.prompt.md      # Gut-check confidence
│       ├── kw-review.prompt.md          # Strategic + data review
│       ├── kw-work.prompt.md            # Execute the plan
│       ├── kw-compound.prompt.md        # Save learnings
│       ├── review-strategic-alignment.prompt.md
│       ├── review-data-accuracy.prompt.md
│       ├── research-knowledge-base.prompt.md
│       ├── research-past-work.prompt.md
│       └── research-stale-knowledge.prompt.md
```

**Requirements:** VS Code with GitHub Copilot extension (v1.99+). Prompt files are a built-in feature — no additional extensions needed.

## Getting Started

Open GitHub Copilot Chat in VS Code and type:

```
#kw-brainstorm I need to figure out our Q2 content strategy
```

When you're ready to commit to a direction:

```
#kw-plan
```

After any meaningful session, save what you learned:

```
#kw-compound
```

Next time you brainstorm or plan something related, those learnings surface automatically.

## Workflows

### Brainstorm
Start here. Paste a meeting transcript, brain dump raw thoughts, or describe a problem. Auto-searches your knowledge base and past plans for relevant context, then extracts key decisions, open questions, constraints, and tensions.

### Plan
Structure a brainstorm into an actionable plan. Searches for past work and saved learnings. Outputs a Pyramid Principle plan (lead with the answer) in three detail tiers — Quick for gut checks, Standard for most plans, Deep for multi-quarter strategies.

### Confidence
Callable at any point in the loop. Pauses to honestly assess what's known and not known — in plain language, not a table. Produces a "confident about / less confident about / my recommendation" breakdown, then offers specific actions to close gaps.

### Review
Two reviewer perspectives check your work simultaneously:
- **Strategic Alignment** — Is the goal clear? Is the hypothesis falsifiable? Are we solving the right problem?
- **Data Accuracy** — Are numbers sourced? Are baselines explicit? Is data fresh?

Findings are grouped P1 (blocks shipping) / P2 (should fix) / P3 (nice to have).

### Work
Execute a plan. Break it into tasks, group by dependency, run independent tasks together. Writes execution log back to the plan file so `#kw-compound` has concrete material to learn from.

### Compound
Extract 1-3 learnings from a session. Checks for stale knowledge that the new learning contradicts. Saves to `docs/knowledge/` with searchable YAML frontmatter.

## How It Works

1. You brainstorm and plan something
2. `#kw-plan` searches `docs/knowledge/` — finds past insights
3. You execute and review
4. `#kw-compound` saves what you learned to `docs/knowledge/`
5. Next time you plan something related, step 2 finds it

No configuration needed. Works with any project that has a `plans/` directory.

The knowledge files are plain markdown, git-tracked, and greppable:

```markdown
# docs/knowledge/trial-conversion-timing.md
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

## Customization

Edit `.github/copilot-instructions.md` to add:

- **Business context and goals** — used by the strategic alignment reviewer
- **Data source hierarchy** — used by the data accuracy reviewer
- **Style guides and conventions** — used during execution

If your project doesn't have custom instructions, the workflows still work — they just won't have project-specific context.

## Differences from the Claude Code Version

| Feature                | Claude Code Plugin             | Copilot Version                          |
| ---------------------- | ------------------------------ | ---------------------------------------- |
| Invocation             | `/kw:brainstorm`               | `#kw-brainstorm` in Copilot Chat         |
| Config file            | `CLAUDE.md`                    | `.github/copilot-instructions.md`        |
| Skills                 | `skills/*/SKILL.md`            | `.github/prompts/*.prompt.md`            |
| Agents                 | `agents/**/*.md`               | `.github/prompts/*.prompt.md`            |
| Parallel task agents   | `<parallel_tasks>` XML tags    | Natural language instructions            |
| Plugin marketplace     | Claude Code plugin registry    | Copy `.github/` directory into project   |
| Pipeline mode          | `disable-model-invocation`     | Not applicable                           |

## M365 Copilot Agent

There's also a version for **Microsoft 365 Copilot** as a Declarative Agent. It consolidates all 6 workflows into a single agent that you deploy via Teams Toolkit. See [`m365-agent/README.md`](m365-agent/README.md) for setup and deployment instructions.

## License

MIT
