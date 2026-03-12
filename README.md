# claude-md-playbook

The context layer that turns Claude Code from a chatbot into a GTM engine.

Built from 50+ real client engagements at [ColdIQ](https://coldiq.com), the #1 ranked Clay Partner. These aren't theoretical templates - they're the exact context structures that produce results at scale. This is the first CLAUDE.md playbook built specifically for GTM teams.

## What is a CLAUDE.md?

CLAUDE.md is a file that Claude Code reads automatically when you open a session in a project folder. It's the operating memory for everything the agent does - your ICP, messaging rules, tool configs, and workflows all live here. Without it, Claude Code gives generic output. With it, Claude Code becomes your GTM infrastructure.

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
│   └── agency-client.md      ← Unique: built for agencies managing client outbound
├── modules/            # Plug-in sections you mix and match
│   ├── icp-definition.md
│   ├── signal-map.md
│   ├── copy-frameworks.md
│   ├── tech-stack-config.md
│   ├── exclusion-rules.md
│   ├── campaign-history.md
│   └── data-hygiene.md
├── skills/             # Task-specific instruction files
│   ├── lead-enrichment.md
│   ├── personalization-writer.md
│   ├── signal-monitor.md
│   ├── campaign-builder.md
│   ├── pipeline-reviewer.md
│   └── reply-classifier.md
├── examples/           # Fully filled-in examples
│   ├── example-outbound-saas.md
│   └── example-abm-enterprise.md
├── .env.example
└── .gitignore
```

## The 3 Layers

**Templates** - Complete CLAUDE.md starter files organized by GTM motion (outbound, PLG, ABM, founder-led, agency). Copy one into your project folder, fill in the placeholders, and you're running. If you're an agency managing outbound for clients, the `agency-client.md` template is purpose-built for multi-client management with approval workflows and reporting - you won't find this anywhere else.

**Modules** - Standalone sections you can plug into any CLAUDE.md. Need a better ICP definition? Grab `modules/icp-definition.md`. Want to add signal monitoring? Drop in `modules/signal-map.md`. Messy CRM data? Use `modules/data-hygiene.md`. Mix and match to build exactly what you need.

**Skills** - Task-specific instruction files that teach Claude Code how to perform individual GTM tasks (enrich leads, write personalized copy, build campaigns, classify replies). Place them in your project's `/skills` folder or reference them directly.

## Quick Start

1. Clone this repo:
   ```bash
   git clone https://github.com/janskuba/claude-md-playbook.git
   ```
2. Copy the template closest to your GTM motion into your project as `CLAUDE.md`:
   ```bash
   cp claude-md-playbook/templates/outbound-first.md ~/my-project/CLAUDE.md
   ```
3. Replace the `[PLACEHOLDER]` sections with your real data (ICP, tech stack, messaging, etc.)
4. Open Claude Code in that folder - done.

## Works With

This playbook references and integrates with the tools GTM teams actually use:

**CRM:** HubSpot, Salesforce, Attio
**Enrichment:** Apollo, Clay, ZoomInfo, Clearbit
**Sending:** Instantly, Lemlist, Smartlead, Outreach
**Research:** Perplexity, LinkedIn Sales Navigator, Crunchbase, G2
**Notifications:** Slack, Gmail
**Reporting:** Google Sheets
**Automation:** n8n, Make

Most tools connect via API keys (configured in your `.env` file) or MCP servers (configured in Claude Code). See `modules/tech-stack-config.md` for setup details.

---

Built by [Jan Rasmussen](http://www.linkedin.com/in/jan-rasmussen) @ [ColdIQ](https://www.linkedin.com/company/coldlabs/)
