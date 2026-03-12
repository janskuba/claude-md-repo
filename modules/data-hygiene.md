# Data Hygiene

<!-- This module defines rules for cleaning and maintaining CRM and prospect data. Paste it into any template where data quality matters (spoiler: all of them). Dirty data kills outbound - duplicates waste send volume, stale contacts hurt deliverability, missing fields break personalization. -->

## Hygiene Rules

### Deduplication

- **Match on:** email address (primary), then company domain + first name + last name (secondary)
- **When duplicates found:** keep the record with the most complete data. Merge fields from the other record if they fill gaps.
- **Cross-list dedup:** before any campaign, deduplicate prospect list against CRM contacts, existing customer list, and DNC list

### Required Fields

Every prospect record must have these fields populated before entering a campaign:

| Field | Required | Validation |
|-------|----------|------------|
| `email` | Yes | Valid format, not a catch-all domain, not personal domain (unless targeting founders) |
| `first_name` | Yes | Not blank, not "Unknown", properly capitalized |
| `last_name` | Yes | Not blank, properly capitalized |
| `company_name` | Yes | Not blank, matches the domain |
| `title` | Yes | Not blank, not generic ("Employee", "Staff") |
| `company_domain` | Yes | Valid domain, resolves to a live website |
| `linkedin_url` | Recommended | Valid LinkedIn profile URL |

Records missing required fields → move to `./data/needs_review/` instead of campaign list.

### Stale Contact Detection

A contact is considered stale if:
- **Title changed:** LinkedIn title doesn't match CRM title (check quarterly)
- **Left company:** No longer at the company in your CRM (check via enrichment tool refresh)
- **Email bounced:** Hard bounce in any previous campaign
- **No engagement:** In CRM for 12+ months with zero activity (no opens, replies, meetings)

**Action for stale contacts:**
1. Re-enrich via [YOUR_ENRICHMENT_TOOL] to get updated data
2. If they changed companies: update record if new company fits ICP, otherwise archive
3. If email bounced: remove from all active campaigns, attempt to find new email
4. If no engagement for 12+ months: archive, don't delete (may re-engage later)

### Data Standardization

- **Titles:** Normalize to standard forms (e.g., "VP of Sales" and "Vice President, Sales" → "VP Sales")
- **Company names:** Remove Inc., LLC, Ltd., Corp. suffixes for consistency
- **Locations:** Use consistent format: City, State (US) or City, Country (international)
- **Phone numbers:** E.164 format if captured
- **Industries:** Map to your ICP industry categories, not freeform text

## CSV Cleaning Workflow

When you receive a raw CSV for campaign use:

1. **Load and inspect:** read the file, report row count, column names, and % of missing values per column
2. **Deduplicate:** identify and remove duplicate rows (report how many removed)
3. **Validate required fields:** flag rows missing required fields, move to needs_review
4. **Standardize:** normalize titles, company names, locations per rules above
5. **Validate emails:** check format, remove obviously invalid (e.g., test@, noreply@, info@)
6. **Enrich gaps:** for records missing key fields, attempt to fill via enrichment API
7. **Cross-reference exclusions:** remove matches against competitor, customer, and DNC lists
8. **Output:** cleaned CSV + hygiene report (rows in, rows out, rows flagged, issues found)

Save cleaned file to: `./data/cleaned/[ORIGINAL_FILENAME]_clean.csv`
Save hygiene report to: `./data/cleaned/[ORIGINAL_FILENAME]_hygiene_report.md`

## CRM Hygiene Schedule

| Task | Frequency | Description |
|------|-----------|-------------|
| Dedup CRM contacts | Weekly | Find and merge duplicate contact records |
| Re-enrich stale contacts | Monthly | Refresh data for contacts not updated in 90+ days |
| Bounce list cleanup | After each campaign | Remove hard bounces from all active lists |
| Title/company validation | Quarterly | Re-enrich top 20% of pipeline contacts to catch job changes |
| Archive inactive | Quarterly | Move 12+ month inactive contacts to archive |
| Customer list sync | Weekly | Export current customers from CRM for exclusion list |

---

## Filled-In Examples

### Example 1: Pre-Campaign CSV Clean

**Input:** `raw_prospects_march.csv` - 500 rows from Apollo export

**Hygiene report:**
- Rows in: 500
- Duplicates removed: 23 (matched on email)
- Missing required fields: 18 (moved to needs_review - 12 missing titles, 6 missing emails)
- Invalid emails removed: 7 (3 catch-all, 2 noreply@, 2 invalid format)
- Exclusions matched: 14 (5 existing customers, 3 competitors, 6 DNC)
- Titles standardized: 45 (e.g., "Vice President of Engineering" → "VP Engineering")
- **Rows out: 438 clean, campaign-ready records**

### Example 2: Quarterly CRM Hygiene

**Scope:** 3,200 contact records in HubSpot

**Results:**
- Duplicates merged: 89
- Job changes detected: 156 (re-enriched, 34 moved to new companies that fit ICP)
- Hard bounces cleaned: 67
- Archived (12+ months inactive): 312
- **Net contacts after hygiene: 2,732 (reduced noise by 15%)**
