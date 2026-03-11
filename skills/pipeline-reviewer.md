---
name: pipeline-reviewer
description: Analyze CRM pipeline data to identify risks, recommend actions, and generate a weekly pipeline summary.
---

# Pipeline Reviewer

## Task

Analyze your CRM pipeline to surface stale deals, flag risk signals, recommend next actions, and generate a concise weekly pipeline summary.

## Input Requirements

- **CRM data source:** one of:
  - CRM API connection (configured in tech stack section of CLAUDE.md)
  - Exported CSV with columns: `deal_name, company, amount, stage, owner, created_date, last_activity_date, close_date, next_step, contacts`
  - File path: `[e.g., ./data/crm/pipeline_export.csv]`
- **Pipeline stages:** [List your pipeline stages in order, e.g., "Discovery → Demo → Proposal → Negotiation → Closed Won/Lost"]
- **Review scope:** `all` | `my_deals` | `team:[TEAM_NAME]`

## Instructions

### 1. Pipeline Health Scan

For each open deal, check:

- **Stale deals:** No activity in [e.g., 14+ days]. Flag with days since last activity.
- **Slipping close dates:** Close date is in the past or within 7 days with no recent activity.
- **Stuck in stage:** Deal has been in the same stage for longer than [e.g., 2x the average for that stage].
- **Single-threaded:** Only one contact engaged. Enterprise deals need 3+ contacts.
- **No next step:** Next step field is empty or vague ("follow up").
- **Upside-down deal:** Amount is below your average deal size for the stage - may not be worth the effort.

### 2. Risk Classification

Classify each deal:

| Risk Level | Criteria |
|------------|----------|
| **Red** | 2+ risk signals, stale 21+ days, or close date passed |
| **Yellow** | 1 risk signal, or approaching stage time limit |
| **Green** | Active, on track, multi-threaded, clear next step |

### 3. Action Recommendations

For each Yellow and Red deal, recommend a specific next action:

- Stale → "Send a value-add resource to re-engage [CONTACT_NAME]"
- Single-threaded → "Identify and engage a second stakeholder - suggest [TITLE]"
- Slipping → "Propose a mutual action plan with revised timeline"
- No next step → "Schedule a [SPECIFIC_MEETING_TYPE] for [SUGGESTED_DATE]"
- Stuck → "Diagnose: is the champion still engaged? Check last interaction."

### 4. Pipeline Summary

Generate a weekly summary:

- **Total pipeline:** $ value, deal count
- **By stage:** deal count + $ value per stage
- **Coverage ratio:** pipeline value ÷ quota target = X:1
- **Weighted pipeline:** $ value × stage probability
- **Velocity:** average days per stage, average deal cycle length
- **Movement this week:** deals advanced, deals created, deals lost, deals won
- **Risk overview:** Red / Yellow / Green count + total $ at risk

## Output Format

Markdown report saved to `./data/reports/pipeline_review_[DATE].md`:

```markdown
# Pipeline Review - [DATE]

## Summary
- Total pipeline: $X (N deals)
- Weighted pipeline: $X
- Coverage: X:1 against $[QUOTA] target
- Deals at risk: N ($X value)

## Risk Alerts
### Red (Immediate Action)
- [DEAL_NAME] - [COMPANY] - $X - [RISK_REASON] - Action: [RECOMMENDATION]

### Yellow (Monitor)
- [DEAL_NAME] - [COMPANY] - $X - [RISK_REASON] - Action: [RECOMMENDATION]

## Stage Distribution
| Stage | Deals | Value | Avg Days |
|-------|-------|-------|----------|

## Wins & Losses This Week
- Won: [DEALS]
- Lost: [DEALS] - Reasons: [LOSS_REASONS]

## Recommendations
1. [TOP_PRIORITY_ACTION]
2. [SECOND_PRIORITY_ACTION]
3. [THIRD_PRIORITY_ACTION]
```

## Example Usage

```
/pipeline-reviewer

Source: CRM API (HubSpot)
Scope: my_deals
```

Output:
```
Pipeline Review - 2026-03-15

Summary: $1.2M pipeline (18 deals), weighted $480K, 3.2:1 coverage

Red Alerts:
- Acme Corp - $85K - No activity in 23 days, single-threaded
  → Action: Re-engage via LinkedIn. Identify VP Engineering as second thread.

- DataFlow - $120K - Close date was March 10, no next step defined
  → Action: Send mutual action plan with revised March 28 close date.

Yellow:
- CloudStack - $45K - In Demo stage for 18 days (avg is 10)
  → Action: Propose a technical deep-dive to move to Proposal.
```
