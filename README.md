# claude-md-playbook

Ready-to-use CLAUDE.md templates that make Claude Code actually work for GTM teams.

## What is a CLAUDE.md?

CLAUDE.md is a file that Claude Code reads automatically when you open a session in a project folder. It's the operating memory for everything the agent does — your ICP, messaging rules, tool configs, and workflows all live here. Without it, Claude Code gives generic output. With it, Claude Code becomes your GTM infrastructure.

## Repo Structure

```
claude-md-playbook/
├── README.md
├── LICENSE
├── templates/          # Full starter CLAUDE.md files by GTM motion
│   ├── outbound-first.md
│   ├── plg-growth.md
│   ├── abm-enterprise.md
│   ├── founder-led-sales.md
│   └── agency-client.md
├── modules/            # Plug-in sections you mix and match
│   ├── icp-definition.md
│   ├── signal-map.md
│   ├── copy-frameworks.md
│   ├── tech-stack-config.md
│   ├── exclusion-rules.md
│   └── campaign-history.md
├── skills/             # Task-specific instruction files
│   ├── lead-enrichment.md
│   ├── personalization-writer.md
│   ├── signal-monitor.md
│   ├── campaign-builder.md
│   └── pipeline-reviewer.md
├── examples/           # Fully filled-in examples
│   ├── example-outbound-saas.md
│   └── example-abm-enterprise.md
└── .gitignore
```

## The 3 Layers

**Templates** — Complete CLAUDE.md starter files organized by GTM motion (outbound, PLG, ABM, founder-led, agency). Copy one into your project folder, fill in the placeholders, and you're running.

**Modules** — Standalone sections you can plug into any CLAUDE.md. Need a better ICP definition? Grab `modules/icp-definition.md`. Want to add signal monitoring? Drop in `modules/signal-map.md`. Mix and match to build exactly what you need.

**Skills** — Task-specific instruction files that teach Claude Code how to perform individual GTM tasks (enrich leads, write personalized copy, build campaigns). Place them in your project's `/skills` folder or reference them directly.

## Quick Start

1. Clone this repo:
   ```bash
   git clone https://github.com/coldiq/claude-md-playbook.git
   ```
2. Copy the template closest to your GTM motion into your project as `CLAUDE.md`:
   ```bash
   cp claude-md-playbook/templates/outbound-first.md ~/my-project/CLAUDE.md
   ```
3. Replace the `[PLACEHOLDER]` sections with your real data (ICP, tech stack, messaging, etc.)
4. Open Claude Code in that folder — done.

## How ColdIQ Uses This

We run this system across 50+ client engagements. These templates are extracted from what actually works at scale — not theory, not best practices blog posts, but the exact context structures that produce results. Learn more at [coldiq.com](https://coldiq.com).

---

Built by [Jan Rasmussen](https://linkedin.com/in/jan-rasmussen-mitjana-b041a6188) @ [ColdIQ](https://coldiq.com)
