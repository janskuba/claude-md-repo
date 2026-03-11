# Tech Stack Config

<!-- This module documents the tools in your GTM stack and how Claude Code connects to each one. Paste it into the Tech Stack section of any template. Claude Code is most powerful when it can read from and write to your actual tools — this config makes that possible. -->

## Stack Overview

| Category | Tool | Purpose | Connection Method |
|----------|------|---------|-------------------|
| CRM | [e.g., HubSpot / Salesforce] | Source of truth for deals and contacts | [API / MCP Server] |
| Enrichment | [e.g., Apollo / Clay / Clearbit] | Lead and company data enrichment | [API] |
| Sending | [e.g., Instantly / Lemlist / Smartlead] | Email sequence delivery | [API] |
| LinkedIn | [e.g., LinkedIn Sales Navigator] | Prospecting and social selling | [Manual / browser extension] |
| Analytics | [e.g., HubSpot / Amplitude / Mixpanel] | Campaign and product analytics | [API / MCP Server] |
| Data warehouse | [e.g., Snowflake / BigQuery] | Centralized data store | [API / MCP Server] |

## Tool Configurations

### CRM — [YOUR_CRM_NAME]

- **API base URL:** `[YOUR_CRM_API_URL]`
- **Authentication:** `[e.g., API key / OAuth 2.0]`
- **API key env variable:** `[e.g., HUBSPOT_API_KEY]`
- **Rate limits:** `[e.g., 100 requests/10 seconds]`
- **Key objects:** `[e.g., Contacts, Companies, Deals, Activities]`
- **Custom fields used:**
  - `[e.g., lead_score — numeric, 0-100]`
  - `[e.g., icp_tier — picklist: Tier 1, Tier 2, Tier 3]`
  - `[e.g., last_signal_date — date]`
- **MCP server:** `[e.g., @anthropic/hubspot-mcp — if applicable]`

### Enrichment — [YOUR_ENRICHMENT_TOOL]

- **API base URL:** `[YOUR_ENRICHMENT_API_URL]`
- **Authentication:** `[e.g., API key in header]`
- **API key env variable:** `[e.g., APOLLO_API_KEY]`
- **Rate limits:** `[e.g., 50 requests/minute]`
- **Key endpoints:**
  - People search: `[e.g., /v1/people/search]`
  - Company enrichment: `[e.g., /v1/companies/enrich]`
  - Contact enrichment: `[e.g., /v1/contacts/enrich]`
- **Fields to pull:** `[e.g., email, title, company_size, industry, technologies, funding_round]`

### Sending Platform — [YOUR_SENDING_TOOL]

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

### LinkedIn — [YOUR_LINKEDIN_TOOL]

- **Access method:** `[e.g., Sales Navigator manual, Phantombuster, LinkedIn API]`
- **Daily limits:** `[e.g., 25 connection requests/day, 50 profile views/day]`
- **Saved searches:** `[List your key saved searches for prospect monitoring]`
- **Data export method:** `[e.g., CSV export from Sales Navigator, API pull]`

### Analytics — [YOUR_ANALYTICS_TOOL]

- **API base URL:** `[YOUR_ANALYTICS_API_URL]`
- **Authentication:** `[e.g., API key / OAuth]`
- **API key env variable:** `[e.g., AMPLITUDE_API_KEY]`
- **Key events tracked:** `[e.g., page_view, trial_started, feature_activated, upgrade_clicked]`
- **Dashboards to reference:** `[e.g., PLG funnel, campaign attribution, pipeline velocity]`

## File Paths & Local Data

- **Prospect lists:** `[e.g., ./data/prospects/]`
- **Campaign exports:** `[e.g., ./data/campaigns/]`
- **Enrichment cache:** `[e.g., ./data/enriched/]`
- **CRM exports:** `[e.g., ./data/crm/]`

## Environment Variables

Store all API keys in a `.env` file (never commit this file):

```bash
# CRM
[CRM_API_KEY]=[your_key_here]

# Enrichment
[ENRICHMENT_API_KEY]=[your_key_here]

# Sending
[SENDING_API_KEY]=[your_key_here]

# Analytics
[ANALYTICS_API_KEY]=[your_key_here]
```

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
