# claude-md-playbook

The context layer that turns Claude Code into a GTM operator.

Built from 50+ real client engagements at [ColdIQ](https://coldiq.com), the #1 ranked Clay Partner. These aren't theoretical templates - they're the exact context structures that produce results at scale. This is the first CLAUDE.md playbook built specifically for GTM teams.

## How It Works

A `CLAUDE.md` file is a context file that Claude Code reads automatically when you open a session in a project folder. Think of it as operating instructions - your ICP, messaging rules, tool configs, and workflows all live here.

**Without it:** Claude Code gives generic output. You prompt, it guesses.
**With it:** Claude Code knows your ICP, writes in your voice, follows your process, and connects to your tools.

This playbook gives you pre-built CLAUDE.md files for different GTM motions. You copy one, fill in your details, and Claude Code immediately operates with your context.

### What to expect

- **This is a context layer, not automation.** It makes Claude Code dramatically better at GTM tasks, but you're still driving. You type prompts, Claude Code executes with your context.
- **API integrations require setup.** Each tool (Apollo, Instantly, HubSpot, etc.) needs its own API key configured. Budget 30-60 minutes for initial setup.
- **Skills are detailed prompts, not plugins.** They guide Claude Code's behavior for specific tasks. Claude Code reads them fresh each session - it doesn't "learn" between sessions.
- **The `/loop` command** (for automated monitoring) requires a Claude Code Max subscription.

## Quick Start

**5-minute version** (no API keys needed):

1. Clone this repo:
   ```bash
   git clone https://github.com/janskuba/claude-md-playbook.git
   ```
2. Copy a template into your project:
   ```bash
   cp claude-md-playbook/templates/outbound-first.md ~/my-project/CLAUDE.md
   ```
3. Fill in the `[PLACEHOLDER]` sections with your real data
4. Open Claude Code in that folder and try:
   ```
   Write a cold email to a VP of Engineering at a Series B SaaS company
   that just raised funding. Use the ICP and copy frameworks in my CLAUDE.md.
   ```

That's it. No API keys needed for basic prompting. See `getting-started.md` for the full setup with tool integrations.

## What You Can Do

Once your CLAUDE.md is set up, here are real prompts that work:

```
Write 3 cold email variants for our "scaling engineering team" angle.
Target: VP Engineering at Series B companies hiring engineers.
```

```
Classify these replies and draft follow-ups for the interested ones.
Input: ./data/replies/inbox_march.csv
```

```
Build a campaign: 100 Series B SaaS companies in the US,
100-500 employees, hiring SDRs. 3-email sequence, signal-based angle.
```

```
Review my pipeline and flag deals with no activity in 14+ days.
```

```
Scan my target account list for new signals from the past 7 days.
Input: ./data/target_accounts.csv
```

## Repo Structure

```
claude-md-playbook/
├── README.md
├── getting-started.md     # Step-by-step setup guide
├── LICENSE
├── templates/             # Full starter CLAUDE.md files by GTM motion
│   ├── outbound-first.md
│   ├── plg-growth.md
│   ├── abm-enterprise.md
│   ├── founder-led-sales.md
│   ├── minimal-starter.md     ← Start here if the others feel heavy
│   └── agency-client.md       ← Unique: built for agencies managing client outbound
├── modules/               # Plug-in sections you mix and match
│   ├── icp-definition.md
│   ├── signal-map.md
│   ├── copy-frameworks.md
│   ├── tech-stack-config.md
│   ├── exclusion-rules.md
│   ├── campaign-history.md
│   └── data-hygiene.md
├── skills/                # Task-specific instruction files
│   ├── lead-enrichment.md
│   ├── personalization-writer.md
│   ├── signal-monitor.md
│   ├── campaign-builder.md
│   ├── pipeline-reviewer.md
│   └── reply-classifier.md
├── examples/              # Fully filled-in examples
│   ├── example-outbound-saas.md
│   └── example-abm-enterprise.md
├── .env.example
└── .gitignore
```

## The 3 Layers

**Templates** - Complete CLAUDE.md starter files organized by GTM motion. Copy one, fill in placeholders, done. New to this? Start with `minimal-starter.md`. Running an agency? The `agency-client.md` template handles multi-client management with approval workflows - you won't find this anywhere else.

**Modules** - Standalone sections you can plug into any CLAUDE.md. Need a better ICP definition? Grab `modules/icp-definition.md`. Want signal monitoring? Drop in `modules/signal-map.md`. Mix and match.

**Skills** - Detailed instruction files for specific GTM tasks (enrich leads, write personalized copy, build campaigns, classify replies). Place them in your project's `/skills` folder and Claude Code follows them when you reference the task.

## Works With

This playbook references and integrates with the tools GTM teams actually use:

**CRM:** HubSpot, Salesforce, Attio
**Enrichment:** Apollo, Clay, ZoomInfo, Clearbit
**Sending:** Instantly, Lemlist, Smartlead, Outreach
**Research:** Perplexity, LinkedIn Sales Navigator, Crunchbase, G2
**Notifications:** Slack, Gmail
**Reporting:** Google Sheets
**Automation:** n8n, Make

Most tools connect via API keys (configured in your `.env` file) or MCP servers (configured in Claude Code). See `getting-started.md` for setup instructions.

---

Built by [Jan Rasmussen](https://www.linkedin.com/in/jan-rasmussen) @ [ColdIQ](https://www.linkedin.com/company/coldlabs/)
