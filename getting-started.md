# Getting Started

Step-by-step guide from zero to running GTM workflows in Claude Code.

## Step 1: Pick a template (2 minutes)

| If you... | Use this template |
|-----------|------------------|
| Just want to try it out | `templates/minimal-starter.md` |
| Run cold outbound | `templates/outbound-first.md` |
| Have a product-led growth motion | `templates/plg-growth.md` |
| Do account-based marketing | `templates/abm-enterprise.md` |
| Are a founder doing your own sales | `templates/founder-led-sales.md` |
| Are an agency managing client outbound | `templates/agency-client.md` |

```bash
# Copy your chosen template into your project folder
cp templates/outbound-first.md ~/my-project/CLAUDE.md
```

## Step 2: Fill in your context (15-30 minutes)

Open your new `CLAUDE.md` and replace every `[PLACEHOLDER]` with your real data. The critical sections:

1. **Identity & Objective** - What you sell and what "success" means
2. **ICP Definition** - Who you're targeting (titles, company size, industry)
3. **Copy Frameworks** - Your tone, messaging angles, and rules

That's enough to start. You can fill in Signal Map, Exclusion Rules, and Campaign History later.

**Tip:** Look at the `examples/` folder for fully filled-in versions. `example-outbound-saas.md` shows what a completed file looks like for a SaaS company.

## Step 3: Try it without any tools (5 minutes)

Open Claude Code in your project folder and try these prompts:

```
Write a 3-email cold outbound sequence targeting our Tier 1 ICP.
Use the messaging angles from my CLAUDE.md.
```

```
I'm reaching out to a VP of Engineering at a company that just raised
a Series B. Write a personalized first touch using my copy frameworks.
```

```
Review this email draft and tell me if it follows my CLAUDE.md rules:
[paste your email]
```

This works with zero API keys. Claude Code reads your CLAUDE.md and writes accordingly.

## Step 4: Add skills (5 minutes)

Copy the skills folder into your project:

```bash
cp -r skills/ ~/my-project/skills/
```

Now you can reference specific workflows:

```
Use the lead-enrichment skill to process ./data/prospects/march_list.csv
```

```
Use the reply-classifier skill to sort these replies: ./data/replies/inbox.csv
```

## Step 5: Connect your tools (30-60 minutes)

This is optional but unlocks the full power. Connect the tools you actually use.

### API keys

```bash
# Copy the env template
cp .env.example ~/my-project/.env

# Edit and add your keys
nano ~/my-project/.env
```

Only fill in the tools you use. You don't need all of them.

### MCP servers (recommended for CRM and notifications)

MCP servers give Claude Code direct read/write access to your tools. Configure them in Claude Code's settings.

**Available MCP connectors:**
- Attio - CRM access
- HubSpot - CRM access
- Slack - Send notifications and alerts
- Gmail - Read and send emails
- Google Sheets - Read and write spreadsheets
- Apollo - Prospecting and enrichment
- Fireflies - Meeting transcripts and notes

To set up: Open Claude Code > Settings > MCP Servers > Add the connector for your tool.

### Tool-by-tool setup

**CRM (pick one):**
- HubSpot: Get API key from Settings > Integrations > API Key. Add `HUBSPOT_API_KEY=` to `.env`
- Salesforce: Get API key from Setup > API. Add `SALESFORCE_API_KEY=` to `.env`
- Attio: Use the MCP connector (recommended) or API key from Settings

**Enrichment:**
- Apollo: API key from Settings > Integrations. Add `APOLLO_API_KEY=` to `.env`
- Clay: API key from Settings > API. Add `CLAY_API_KEY=` to `.env`

**Sending (pick one):**
- Instantly: API key from Settings > Integrations. Add `INSTANTLY_API_KEY=` to `.env`
- Lemlist: API key from Settings. Add `LEMLIST_API_KEY=` to `.env`
- Smartlead: API key from Settings. Add `SMARTLEAD_API_KEY=` to `.env`

**Research:**
- Perplexity: API key from perplexity.ai/settings. Add `PERPLEXITY_API_KEY=` to `.env`

**Notifications:**
- Slack: Create a webhook at api.slack.com/apps. Add `SLACK_WEBHOOK_URL=` to `.env`

## Step 6: Build your first campaign

With everything connected, try a full workflow:

```
Build a campaign targeting Series B SaaS companies in the US,
100-500 employees. 50 prospects, 3-email sequence over 10 days.
Use the signal-based messaging angle. Export for Instantly.
```

Claude Code will:
1. Reference your ICP to filter targets
2. Use your copy frameworks for messaging
3. Apply your exclusion rules
4. Format the output for your sending platform

## Common issues

**"Claude Code isn't reading my CLAUDE.md"**
- Make sure the file is named exactly `CLAUDE.md` (case-sensitive) and is in the root of your project folder

**"API calls are failing"**
- Check your `.env` file has the correct key names (match `.env.example`)
- Verify your API key is active and has sufficient credits
- Check rate limits - most APIs throttle at 50-100 requests/minute

**"The output is too generic"**
- Your ICP section is probably too vague. Be specific: exact titles, company sizes, industries, and signals
- Add real examples to your Copy Frameworks section - Claude Code matches your style better with examples

**"I don't know which sections to fill in first"**
- Start with: Identity, ICP Definition, Copy Frameworks. That covers 80% of the value.
- Add Signal Map and Exclusion Rules when you start running campaigns
- Campaign History builds over time as you log results

## Need help?

- Check the `examples/` folder for fully filled-in references
- Use `modules/` to grab individual sections and customize them
- For professional setup and ongoing GTM execution: [ColdIQ](https://coldiq.com)
