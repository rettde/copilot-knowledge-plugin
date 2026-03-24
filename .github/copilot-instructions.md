# Compound Knowledge — Copilot Custom Instructions

## What This Is

Compound Knowledge is a set of reusable prompt files for knowledge work that compounds over time. Each cycle of brainstorm → plan → review → execute → compound makes the next cycle faster.

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

## How It Works

1. You brainstorm and plan something
2. `#kw-plan` searches `docs/knowledge/` — finds past insights
3. You execute and review
4. `#kw-compound` saves what you learned to `docs/knowledge/`
5. Next time you plan something related, step 2 finds it

No configuration needed. Works with any project that has a `plans/` directory.

## Knowledge File Format

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

Extended trial periods (30 days vs 7 days) increase conversion rate but delay revenue recognition. Net positive after 60 days.
```

## Project Context

These workflows read your project's `.github/copilot-instructions.md` (this file) for:

- **Business context and goals** — used by the strategic alignment reviewer
- **Data source hierarchy** — used by the data accuracy reviewer
- **Style guides and conventions** — used during execution

Add your project-specific context below this section. The workflows adapt to whatever project they're installed in.

## Design Principles

- **Generic over specific.** No company-specific references in workflow prompts. Project context comes from this file.
- **Opinionated but adaptable.** Strong defaults (Pyramid Principle, P1/P2/P3 severity) that adapt to any project.
- **Local first.** `docs/knowledge/` is the primary knowledge store.
- **Progressive disclosure.** Start with the 6 workflows. Dig deeper as patterns emerge.

---

<!-- Add your project-specific context below -->
