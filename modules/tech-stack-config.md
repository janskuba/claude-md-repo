# Tech Stack Config

<!-- This module documents the tools in your GTM stack and how Claude Code connects to each one. Paste it into the Tech Stack section of any template. Claude Code is most powerful when it can read from and write to your actual tools - this config makes that possible. -->

## Stack Overview

| Category | Tool | Purpose | Connection Method |
|----------|------|---------|-------------------|
| CRM | [e.g., HubSpot / Salesforce / Attio] | Source of truth for deals and contacts | [API / MCP Server] |
| Enrichment | [e.g., Apollo / Clay / Clearbit / ZoomInfo] | Lead and company data enrichment | [API] |
| Sending | [e.g., Instantly / Lemlist / Smartlead] | Email sequence delivery | [API] |
| LinkedIn | [e.g., LinkedIn Sales Navigator] | Prospecting and social selling | [Manual / CSV export] |
| Research | [e.g., Perplexity] | Deep company research, signal verification, competitive intel | [API / Manual] |
| Analytics | [e.g., HubSpot / Amplitude / Mixpanel / G2 Buyer Intent] | Campaign and product analytics | [API / MCP Server] |
| Data warehouse | [e.g., Snowflake / BigQuery / Google Sheets] | Centralized data store and reporting | [API / MCP Server / Manual] |
| Notifications | [e.g., Slack / Gmail] | Signal alerts, reply routing, pipeline updates, team notifications | [Webhook / MCP Server / API] |
| Automation | [e.g., n8n / Make / Zapier] | Workflow orchestration between tools | [Webhook / API] |

## Tool Configurations

### CRM - [YOUR_CRM_NAME]

- **API base URL:** `[YOUR_CRM_API_URL]`
- **Authentication:** `[e.g., API key / OAuth 2.0]`
- **API key env variable:** `[e.g., HUBSPOT_API_KEY]`
- **Rate limits:** `[e.g., 100 requests/10 seconds]`
- **Key objects:** `[e.g., Contacts, Companies, Deals, Activities]`
- **Custom fields used:**
  - `[e.g., lead_score - numeric, 0-100]`
  - `[e.g., icp_tier - picklist: Tier 1, Tier 2, Tier 3]`
  - `[e.g., last_signal_date - date]`
- **MCP server:** `[e.g., @anthropic/hubspot-mcp - if applicable]`

### Enrichment - [YOUR_ENRICHMENT_TOOL]

- **API base URL:** `[YOUR_ENRICHMENT_API_URL]`
- **Authentication:** `[e.g., API key in header]`
- **API key env variable:** `[e.g., APOLLO_API_KEY]`
- **Rate limits:** `[e.g., 50 requests/minute]`
- **Key endpoints:**
  - People search: `[e.g., /v1/people/search]`
  - Company enrichment: `[e.g., /v1/companies/enrich]`
  - Contact enrichment: `[e.g., /v1/contacts/enrich]`
- **Fields to pull:** `[e.g., email, title, company_size, industry, technologies, funding_round]`

### Sending Platform - [YOUR_SENDING_TOOL]

- **API base URL:** `[YOUR_SENDING_API_URL]`
- **Authentication:** `[e.g., API key]`
- **API key env variable:** `[e.g., INSTANTLY_API_KEY]`
- **Rate limits:** `[e.g., 200 emails/day per mailbox]`
- **Key endpoints:**
  - Create campaign: `[e.g., /v1/campaigns]`
  - Add leads to campaign: `[e.g., /v1/campaigns/{id}/leads]`
  - Get campaign analytics: `[e.g., /v1/campaigns/{id}/analytics]`
- **Mailbox configuration:**
  - Sending accounts: `[e.g., 5 warmed mailboxes]`
  - Daily send limit per mailbox: `[e.g., 40]`
  - Warmup status: `[e.g., all mailboxes fully warmed]`

### LinkedIn - [YOUR_LINKEDIN_TOOL]

- **Access method:** `[e.g., Sales Navigator manual, Phantombuster, LinkedIn API]`
- **Daily limits:** `[e.g., 25 connection requests/day, 50 profile views/day]`
- **Saved searches:** `[List your key saved searches for prospect monitoring]`
- **Data export method:** `[e.g., CSV export from Sales Navigator, API pull]`

### Analytics - [YOUR_ANALYTICS_TOOL]

- **API base URL:** `[YOUR_ANALYTICS_API_URL]`
- **Authentication:** `[e.g., API key / OAuth]`
- **API key env variable:** `[e.g., AMPLITUDE_API_KEY]`
- **Key events tracked:** `[e.g., page_view, trial_started, feature_activated, upgrade_clicked]`
- **Dashboards to reference:** `[e.g., PLG funnel, campaign attribution, pipeline velocity]`

### Research - [e.g., Perplexity]

- **API base URL:** `https://api.perplexity.ai`
- **Authentication:** API key in header
- **API key env variable:** `PERPLEXITY_API_KEY`
- **Rate limits:** [Check current plan limits]
- **Use cases:**
  - Deep company research for ABM account briefs (earnings calls, strategic priorities, competitive landscape)
  - Signal verification - confirm hiring, funding, and tech adoption signals found via other sources
  - Prospect research - recent publications, conference talks, LinkedIn activity context
  - Competitive intelligence - competitor positioning, pricing, recent moves
- **Note:** Can also be used manually (no API needed) for ad-hoc research during account planning

### Notifications - [e.g., Slack]

- **Webhook URL:** `[YOUR_SLACK_WEBHOOK_URL]`
- **MCP server:** `[e.g., Slack MCP connector - available in Claude Code connectors]`
- **Channels to configure:**
  - `#signals` - P0 signal alerts from signal monitor
  - `#replies` - Interested and referral replies from reply classifier
  - `#pipeline` - Weekly pipeline review summaries
  - `#campaigns` - Campaign launch and completion notifications
- **Alert rules:**
  - P0 signals → immediate Slack notification with suggested action
  - Positive replies → route to Slack within 1 minute
  - Pipeline red alerts → daily digest to #pipeline

### Email - [e.g., Gmail / Google Workspace]

- **MCP server:** `[e.g., Gmail MCP connector - available in Claude Code connectors]`
- **API:** Gmail API via Google Cloud Console
- **API key env variable:** `GOOGLE_API_CREDENTIALS` (OAuth 2.0 credentials JSON path)
- **Use cases:**
  - Read and classify incoming reply emails (feeds into reply-classifier skill)
  - Draft follow-up responses based on reply classification
  - Send campaign-related emails when not using a dedicated sending platform
  - Monitor inbox for signal-triggered replies
- **Note:** For high-volume sending, use a dedicated platform (Instantly, Lemlist). Gmail is best for 1:1 follow-ups, founder-led outreach, and reply management.

### Reporting - [e.g., Google Sheets]

- **MCP server:** `[e.g., Google Sheets MCP connector]`
- **API:** Google Sheets API via Google Cloud Console
- **API key env variable:** `GOOGLE_API_CREDENTIALS` (same OAuth credentials as Gmail)
- **Use cases:**
  - Campaign tracking dashboards (import results from sending platforms)
  - Pipeline reporting for teams not using a full BI tool
  - Prospect list management for lightweight setups (founder-led, early-stage)
  - Shared team scorecards and weekly metrics
  - Export enriched data from Claude Code workflows for team review
- **Note:** For teams without a CRM, Google Sheets + Claude Code can serve as a lightweight pipeline tracker. Use structured column headers so Claude Code can read and write to them consistently.

## File Paths & Local Data

- **Prospect lists:** `[e.g., ./data/prospects/]`
- **Campaign exports:** `[e.g., ./data/campaigns/]`
- **Enrichment cache:** `[e.g., ./data/enriched/]`
- **CRM exports:** `[e.g., ./data/crm/]`

## Environment Variables

Store all API keys in a `.env` file (never commit this file). See `.env.example` in the repo root for the full list.

---

## Filled-In Examples

### Example 1: Outbound Stack

| Category | Tool | Connection |
|----------|------|------------|
| CRM | HubSpot | MCP Server (`@anthropic/hubspot-mcp`) |
| Enrichment | Apollo | REST API (API key in header) |
| Sending | Instantly | REST API |
| LinkedIn | Sales Navigator | Manual + CSV export |

### Example 2: PLG Stack

| Category | Tool | Connection |
|----------|------|------------|
| CRM | Salesforce | MCP Server |
| Product analytics | Amplitude | REST API |
| Enrichment | Clearbit | REST API |
| Sending | Customer.io | REST API |
