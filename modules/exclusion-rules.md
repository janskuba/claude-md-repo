# Exclusion Rules

<!-- This module defines who NOT to contact. Paste it into the Exclusion Rules section of any template. A clean exclusion list prevents wasted outreach, protects your sender reputation, and avoids embarrassing mistakes like emailing your own customers or competitors. -->

## Competitor Domains

<!-- Add the domains of direct and indirect competitors. Never contact anyone at these companies. -->

- `[e.g., competitor1.com]`
- `[e.g., competitor2.com]`
- `[e.g., competitor3.io]`

## Existing Customer Domains

<!-- Export from your CRM. Update monthly. Never send cold outreach to current customers. -->

- `[Export your active customer domain list from CRM and paste here]`
- Or reference a file: `[e.g., ./data/exclusions/current_customers.csv]`

## Do-Not-Contact List

<!-- People who have explicitly opted out, asked not to be contacted, or had a bad experience. This overrides everything. -->

- `[e.g., ./data/exclusions/dnc_list.csv]`
- Include: previous unsubscribes, legal/compliance blocks, manual opt-outs

## Geographic Exclusions

<!-- Regions you don't sell into or can't legally contact. -->

- [e.g., Countries where you have no entity or compliance coverage]
- [e.g., EU contacts if you're not GDPR-compliant]
- [e.g., Specific states with strict cold outreach laws]

## Industry Exclusions

<!-- Industries outside your ICP or that create risk. -->

- [e.g., Government / public sector]
- [e.g., Education / non-profit (if not your market)]
- [e.g., Heavily regulated industries you can't serve]

## Title Exclusions

<!-- Titles that are never relevant to your sale. -->

- [e.g., Intern, Student, Volunteer]
- [e.g., Titles in departments you don't sell to]

## Email Domain Blacklist

<!-- Domains that indicate low-quality or irrelevant contacts. -->

- `gmail.com` (unless targeting founders/freelancers)
- `yahoo.com`
- `hotmail.com`
- `outlook.com` (personal)
- `[Add any catch-all or spam-trap domains you've identified]`

## Keeping Exclusions Updated

<!-- How to maintain this list over time. -->

1. **Weekly:** Export new customers from CRM and add to existing customer list
2. **Weekly:** Add any bounce-backs or unsubscribes to DNC list
3. **Monthly:** Review competitor list for new entrants
4. **Quarterly:** Audit full exclusion list against CRM data
5. **Before every campaign:** Run prospect list against all exclusion lists before sending

---

## Filled-In Examples

### Example 1: Sales Engagement Platform

**Competitors:** outreach.io, salesloft.com, apollo.io, lemlist.com
**Customer file:** `./data/exclusions/active_customers.csv`
**DNC file:** `./data/exclusions/dnc.csv`
**Geographic exclusions:** China, Russia (no entity)
**Industry exclusions:** Government, education, non-profit
**Title exclusions:** Intern, Student, Executive Assistant

### Example 2: Data Infrastructure Company

**Competitors:** snowflake.com, databricks.com, fivetran.com
**Customer file:** `./data/exclusions/customers.csv`
**Geographic exclusions:** None (sell globally)
**Industry exclusions:** Consumer / B2C companies
**Title exclusions:** Marketing, HR, Finance (not relevant to data infrastructure sale)
