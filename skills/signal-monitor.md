---
name: signal-monitor
description: Scan target accounts for new buying signals and output a prioritized alert list.
---

# Signal Monitor

## Task

Scan a list of target accounts for new buying signals across multiple sources. Output a prioritized alert list so your team acts on the hottest signals first.

This skill pairs well with `/loop` for scheduled, recurring monitoring (e.g., run every Monday morning).

## Input Requirements

- A target account list (CSV) with at minimum: `company_name`, `company_domain`
- Signal categories to monitor (from your CLAUDE.md signal map): `hiring` | `funding` | `tech_adoption` | `content_social` | `intent` | `competitive` | `timing` | `all`
- Lookback window: `24h` | `7d` | `30d`

## Instructions

1. **Load the target account list** and the signal map from your CLAUDE.md
2. **For each account, check for signals:**
   - **Hiring:** New job postings matching your ICP's relevant roles (check LinkedIn Jobs, company careers page)
   - **Funding:** New funding announcements (check Crunchbase, press, TechCrunch)
   - **Leadership changes:** New executives in target departments (check LinkedIn)
   - **Tech stack changes:** Added or removed relevant technologies (check BuiltWith, job postings mentioning new tools)
   - **Content/social:** Prospect or company posted about relevant topics (check LinkedIn, company blog)
   - **Intent:** Website visits, G2 category research, content downloads (if intent data available)
   - **Competitive:** Negative competitor reviews, competitor contract renewals (if data available)
   - **Web research verification:** For P0 signals, use Perplexity to verify and enrich - confirm the hiring post is still active, check if the funding has a press release with details, pull recent company news for context
3. **Prioritize signals:**
   - P0: Act within 48 hours (high-intent signals like hiring, funding, competitor churn)
   - P1: Act within 1 week (medium-intent like tech adoption, content activity)
   - P2: Use as context in next outreach (timing signals, milestones)
4. **Deduplicate:** If same signal detected from multiple sources, consolidate into one entry
5. **Enrich:** For P0 signals, identify the best contact to reach out to and suggest an outreach angle

## Output Format

Prioritized alert list (CSV or markdown):

```
priority, company_name, signal_type, signal_detail, source, detected_date, suggested_contact, suggested_angle, action_deadline
```

Summary stats:
- Total accounts scanned
- Accounts with new signals
- P0 / P1 / P2 signal breakdown

Save to: `./data/signals/signal_scan_[DATE].csv`

### Routing Alerts

- **P0 signals:** Send immediately to Slack `#signals` channel with: company name, signal type, suggested contact, and recommended outreach angle
- **P1 signals:** Include in weekly Slack digest to `#signals`
- **Gmail notification:** For teams without Slack, send a summary email to your team's shared inbox with the P0 alert list

Configure Slack webhook: set `SLACK_WEBHOOK_URL` in your `.env` file, or use the Slack MCP connector in Claude Code.

## Example Usage

```
/signal-monitor

Input: ./data/target_accounts.csv
Categories: all
Lookback: 7d
```

Output:
```
P0 Signals (act within 48h):
- DataFlow Inc - HIRING - 3 Data Engineer roles posted 2 days ago - Source: LinkedIn Jobs
  → Contact: Alex Chen (VP Engineering) - Angle: "scaling your data team"

- Acme Corp - FUNDING - $25M Series B announced yesterday - Source: Crunchbase
  → Contact: Sarah Kim (CTO) - Angle: "post-raise infrastructure scaling"

P1 Signals (act within 1 week):
- CloudStack - TECH_ADOPTION - Added Snowflake to tech stack - Source: BuiltWith
  → Contact: Mike Johnson (Head of Data) - Angle: "Snowflake pipeline observability"

Summary: 50 accounts scanned, 8 with new signals (3 P0, 3 P1, 2 P2)
```

## Scheduled Monitoring

To run this on a recurring schedule, use:

```
/loop signal-monitor --every monday --input ./data/target_accounts.csv --categories all --lookback 7d
```

This creates a weekly signal digest that compounds your account intelligence over time.
