---
name: lead-enrichment
description: Enrich a list of companies or contacts with firmographic, technographic, and contact data using available APIs.
---

# Lead Enrichment

## Task

Take a raw list of companies or contacts and enrich each record with structured data from available APIs and web sources. Output a clean, analysis-ready dataset.

## Input Requirements

- A CSV or JSON file containing at least one of:
  - Company names or domains
  - Contact names + company
  - LinkedIn profile URLs
- File path: provide the path to the input file
- Enrichment level: `basic` (company data only) or `full` (company + contact + signals)

## Instructions

1. **Read the input file** and validate the format. Flag any rows missing required fields.
2. **For each company**, pull:
   - Employee count, revenue estimate, industry, founding year
   - Headquarters location, other office locations
   - Funding history (total raised, last round, date)
   - Tech stack (from BuiltWith, job postings, or similar)
   - Recent news (funding, hiring, product launches)
   - LinkedIn company page URL
   - For Tier 1 prospects, use Perplexity for deeper research: recent company news, executive interviews, strategic priorities, competitive moves. This context powers stronger personalization.
3. **For each contact** (if `full` enrichment):
   - Verified email address
   - Current title and seniority level
   - LinkedIn profile URL
   - Time in current role
   - Previous companies
4. **Score each record** against the ICP definition in your CLAUDE.md:
   - Tier 1 / Tier 2 / Tier 3 based on scoring rubric
   - Flag records that don't meet minimum ICP criteria
5. **Check exclusion rules:** remove any records matching competitor domains, existing customers, or DNC lists
6. **Write a personalization note** for each Tier 1 and Tier 2 prospect: one sentence referencing their strongest signal

## Output Format

CSV file with these columns:

```
company_name, company_domain, industry, employee_count, revenue_estimate, funding_stage, last_funding_date, tech_stack, hq_location, contact_name, contact_email, contact_title, contact_linkedin, seniority, signal, tier_score, personalization_note, exclude_reason
```

- Save to: `./data/enriched/[INPUT_FILENAME]_enriched.csv`
- Log summary: total records processed, records enriched, records excluded, tier distribution

## Example Usage

```
/lead-enrichment

Input: ./data/prospects/saas_companies_march.csv
Enrichment level: full
```

Output: `./data/enriched/saas_companies_march_enriched.csv` with 150 records enriched, 12 excluded (3 competitors, 5 existing customers, 4 below ICP minimum), tier distribution: 34 Tier 1, 67 Tier 2, 37 Tier 3.
