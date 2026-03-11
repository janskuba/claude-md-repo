---
name: personalization-writer
description: Generate personalized first lines, email copy, or LinkedIn messages based on prospect data and copy frameworks.
---

# Personalization Writer

## Task

Generate personalized outreach messages for a list of prospects. Uses the copy frameworks defined in your CLAUDE.md and adapts each message based on the prospect's specific signals and context.

## Input Requirements

- An enriched prospect list (CSV or JSON) with at minimum: `contact_name`, `company_name`, `contact_title`, `signal`, `personalization_note`
- Message type: `first_line` | `full_email` | `linkedin_connection` | `linkedin_dm` | `follow_up`
- Messaging angle: `signal_based` | `problem_led` | `social_proof` | `content_based`
- Sequence position (for follow-ups): `follow_up_1` | `follow_up_2` | `breakup`

## Instructions

1. **Read the prospect list** and the copy frameworks section of your CLAUDE.md
2. **For each prospect:**
   - Identify their primary signal (hiring, funding, tech adoption, content, etc.)
   - Select the matching message template from copy frameworks
   - Research additional context if needed (recent LinkedIn posts, company news)
   - Write the personalized message following tone rules and length guidelines
3. **Quality checks per message:**
   - Contains at least one detail specific to this prospect (not reusable for anyone else)
   - Under the word limit for the message type
   - CTA is a soft ask (never "book a demo")
   - No buzzwords, no exclamation marks, no emojis
   - Sounds like a human wrote it, not a template
4. **Flag for review:** any prospects where personalization context is thin - don't force a bad personalization

## Output Format

CSV with columns:

```
contact_name, contact_email, company_name, message_type, subject_line, message_body, personalization_source, confidence_score
```

- `confidence_score`: `high` (strong signal + specific context), `medium` (decent context), `low` (thin personalization - review before sending)
- Save to: `./data/outreach/[DATE]_[MESSAGE_TYPE]_personalized.csv`

## Example Usage

```
/personalization-writer

Input: ./data/enriched/saas_companies_march_enriched.csv
Message type: full_email
Angle: signal_based
```

Output:
```
contact_name: Alex Chen
company_name: DataFlow Inc
subject_line: Your 3 new data engineer roles
message_body: Alex, saw DataFlow is hiring 3 data engineers - scaling
the pipeline team. Most data teams at your stage hit observability
issues around month 3. We helped Acme cut pipeline debugging by 70%.
Worth a quick look?
personalization_source: LinkedIn job posting (3 data engineer roles, posted 5 days ago)
confidence_score: high
```
