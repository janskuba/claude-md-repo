---
name: campaign-builder
description: Build a complete micro-campaign from ICP segment definition to campaign-ready output files.
---

# Campaign Builder

## Task

Build a complete micro-campaign end-to-end: define the segment, build the prospect list, enrich it, generate personalized copy, and output files ready for import into your sending platform.

## Input Requirements

- **Segment definition:** ICP tier + signal type + any additional filters (e.g., "Tier 1 SaaS companies, 100-500 employees, hiring SDRs, US-based")
- **Campaign goal:** [e.g., book meetings, drive event registrations, promote content]
- **Volume target:** [e.g., 100 prospects]
- **Channel:** `email` | `linkedin` | `multi_channel`
- **Sequence length:** [e.g., 3 emails over 14 days]
- **Messaging angle:** `signal_based` | `problem_led` | `social_proof`
- **Sending platform:** [e.g., Instantly, Lemlist, Smartlead]

## Instructions

### Phase 1: Prospect List

1. Query your enrichment tools using the segment definition
2. Filter to prospects matching ICP tier criteria
3. Find 2–3 contacts per company matching target personas
4. Verify email addresses
5. Run against exclusion lists (competitors, customers, DNC)
6. Output: raw prospect list

### Phase 2: Enrichment & Scoring

1. Enrich each prospect: company data, tech stack, funding, recent news
2. Identify the primary buying signal per prospect
3. Score: Tier 1 / Tier 2 / Tier 3
4. Write a 1-sentence personalization note per prospect
5. Remove Tier 3 prospects (unless volume target requires them)
6. Output: enriched, scored prospect list

### Phase 3: Copy Generation

1. Select message templates from your copy frameworks based on the messaging angle
2. Write the email sequence:
   - Email 1: first touch (signal-based or problem-led)
   - Email 2: value-add follow-up (Day 3–4)
   - Email 3: social proof (Day 7–8)
   - Email 4 (optional): breakup (Day 14)
3. Personalize each email per prospect using their signal and personalization note
4. For multi-channel: write LinkedIn connection request + DM
5. Quality check: every message has prospect-specific detail, is under word limit, uses soft CTA
6. Output: personalized sequences per prospect

### Phase 4: Campaign Package

1. Format prospect data for your sending platform's import template
2. Map columns to platform fields. Common formats:
   - **Instantly:** `email, first_name, last_name, company_name, custom1, custom2, ...` (custom fields map to `{{custom1}}` variables in sequences)
   - **Lemlist:** `email, firstName, lastName, companyName, icebreaker, ...` (icebreaker field maps to `{{icebreaker}}` variable)
   - **Smartlead:** `email, first_name, last_name, company, custom1, custom2, ...` (similar to Instantly)
3. Create the sequence in platform format with timing rules
4. Generate a campaign summary: segment, volume, messaging angle, sequence outline, expected send dates
5. Output all files to campaign folder
6. **Notification:** Post campaign summary to Slack `#campaigns` channel and/or email to team via Gmail
7. **Tracking sheet:** If using Google Sheets for reporting, append a new row to your campaign tracker with: campaign name, date, segment, volume, and status

## Output Format

Campaign folder at `./data/campaigns/[CAMPAIGN_NAME]/`:

```
[CAMPAIGN_NAME]/
├── prospects.csv              # Platform-ready prospect list
├── sequence.csv               # Email sequence with personalization
├── linkedin_messages.csv      # LinkedIn messages (if multi-channel)
├── campaign_summary.md        # Campaign overview for review
└── exclusions_applied.log     # Record of what was excluded and why
```

`campaign_summary.md` includes:
- Segment definition
- Volume: total prospects, tier breakdown
- Sequence: number of steps, timing, messaging angle
- Personalization: sample of 3 emails (best, median, weakest personalization)
- Ready for approval: yes/no

## Example Usage

```
/campaign-builder

Segment: Series B SaaS companies, 100-500 employees, hiring SDRs, US
Goal: Book meetings
Volume: 100 prospects
Channel: email
Sequence: 3 emails over 14 days
Angle: signal_based
Platform: Instantly
```

Output: `./data/campaigns/series_b_sdr_hiring_march/` with 100 prospects, 3-step email sequence personalized per prospect, ready for Instantly import.
