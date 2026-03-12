---
name: reply-classifier
description: Read reply emails and classify them by intent (interested, objection, not now, unsubscribe) with recommended next actions.
---

# Reply Classifier

## Task

Read incoming reply emails from outbound campaigns and classify each by intent. Output a categorized list with recommended next actions so your team responds fast and appropriately.

## Input Requirements

- Reply emails in one of these formats:
  - CSV with columns: `from_email, from_name, subject, body, received_date, campaign_name`
  - Raw email text (for single-reply classification)
  - File path to a folder of `.eml` or `.txt` files
- Copy frameworks from your CLAUDE.md (for generating suggested responses)

## Instructions

1. **Read each reply** and classify into one of these categories:

| Category | Description | Response SLA |
|----------|-------------|--------------|
| **Interested** | Wants to learn more, asked a question, agreed to meet | Within 1 hour |
| **Objection** | Raised a concern but didn't shut the door (budget, timing, competitor, authority) | Within 4 hours |
| **Not now** | Timing isn't right but didn't say never ("circle back later", "not a priority right now") | Acknowledge + set reminder |
| **Referral** | Pointed you to someone else ("talk to my colleague", "reach out to X") | Within 2 hours |
| **Unsubscribe** | Wants to be removed ("remove me", "stop emailing", "unsubscribe") | Immediate - remove and confirm |
| **Out of office** | Auto-reply, OOO message | No action - re-engage after return date |
| **Not relevant** | Wrong person, wrong company, spam, bounce notification | Archive |

2. **For each classified reply, generate:**
   - **Category** and **confidence level** (high / medium / low)
   - **Suggested response** using your copy frameworks:
     - Interested → propose a specific time, keep momentum
     - Objection → acknowledge, address with one line, soft re-ask
     - Not now → confirm, offer a resource, set a future date
     - Referral → thank them, ask for an intro or permission to use their name
     - Unsubscribe → confirm removal, professional close
   - **CRM action:** what to update (deal stage, next step, contact status, task)

3. **Flag edge cases:** replies that are ambiguous or could be read multiple ways → mark as "needs human review"

## Output Format

CSV with columns:

```
from_email, from_name, company, received_date, category, confidence, suggested_response, crm_action, campaign_name
```

Plus a summary:

```
Total replies processed: N
- Interested: N (respond within 1 hour)
- Objection: N (respond within 4 hours)
- Not now: N (set reminders)
- Referral: N (follow up on referral)
- Unsubscribe: N (remove immediately)
- Out of office: N (no action)
- Not relevant: N (archive)
- Needs human review: N
```

Save to: `./data/replies/classified_[DATE].csv`

### Reply Routing

- **Interested + Referral replies:** Route to Slack `#replies` channel within 1 minute for fastest response. Include: sender name, company, reply snippet, suggested response, and CRM action.
- **Objection replies:** Route to Slack `#replies` with suggested rebuttal from copy frameworks.
- **Unsubscribe:** Auto-log in Google Sheets exclusion tracker (or CRM) - no Slack notification needed.
- **Gmail integration:** If using Gmail MCP connector, Claude Code can draft response emails directly in Gmail based on the suggested responses above. Review before sending.

Configure Slack webhook: set `SLACK_WEBHOOK_URL` in your `.env` file.

## Example Usage

```
/reply-classifier

Input: ./data/replies/inbox_export_march_10.csv
```

Output:
```
Total replies: 24
- Interested: 5 → respond ASAP
  - Sarah Kim (DataFlow): "This looks relevant. Can you send a one-pager?"
    → Suggested: "Sure thing, Sarah. Here's our one-pager [LINK]. Happy to walk through it live - does Thursday 2pm work?"
    → CRM: Move to "Engaged", set task for Thursday

- Objection: 3
  - Mike Chen (Acme): "We just signed a 2-year deal with [COMPETITOR]."
    → Suggested: "Makes sense - [COMPETITOR] is solid for X. Where we're different is Y. Worth keeping in touch for when the renewal comes up?"
    → CRM: Set "Competitor" field, set reminder 18 months out

- Not now: 6
  - Alex Rivera (CloudCo): "Not a priority this quarter."
    → Suggested: "Totally get it. I'll circle back in Q3. In the meantime, here's a relevant case study if useful."
    → CRM: Set follow-up task for July 1

- Unsubscribe: 2 → remove from all sequences immediately
- Out of office: 4 → no action, earliest return: March 17
- Referral: 1 → follow up on referral to VP Engineering
- Not relevant: 2 → archive
- Needs human review: 1 → tone unclear, may be sarcastic
```
