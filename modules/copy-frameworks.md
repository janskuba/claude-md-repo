# Copy Frameworks

<!-- This module defines your messaging templates and tone rules. Paste it into the Copy Frameworks section of any template. Good outbound copy is short, specific, and earns the next step - not the deal. Every template here follows that principle. -->

## Tone Rules

- **Voice:** [e.g., Direct, peer-to-peer, no corporate speak]
- **Length:** First touch emails under 100 words. LinkedIn messages under 50 words. Follow-ups under 75 words.
- **Personalization:** Every message must include at least one specific detail about the prospect or their company that couldn't apply to anyone else.
- **CTA:** Always a soft ask. Never "book a demo." Use: quick question, worth a look, make sense to chat, relevant to share.
- **Avoid:** Buzzwords ("synergy," "leverage," "cutting-edge"), fake urgency, self-centered language ("We're the leading..."), exclamation marks, emojis in email.

## First Touch Templates

### Cold Email - Signal-Based

```
Subject: [SIGNAL_REFERENCE] - [SHORT_HOOK]

[FIRST_NAME],

Saw [SPECIFIC_SIGNAL - e.g., you're hiring 3 SDRs / just raised your Series B / posted about X].

[ONE_SENTENCE connecting signal to your product's value - what changes for them].

[SOCIAL_PROOF - e.g., "We helped [SIMILAR_COMPANY] do X in Y timeframe."]

[SOFT_CTA - e.g., "Worth a quick look?"]

[YOUR_NAME]
```

### Cold Email - Problem-Led

```
Subject: [PROBLEM_STATEMENT]

[FIRST_NAME],

Most [PERSONA_TITLE]s at [COMPANY_STAGE] companies [DESCRIBE_COMMON_PROBLEM - e.g., "spend 10+ hours/week manually building prospect lists"].

[ONE_SENTENCE about how your product solves this differently].

[PROOF_POINT - e.g., metric, customer result, or case study reference].

[SOFT_CTA]

[YOUR_NAME]
```

### LinkedIn Connection Request

```
[FIRST_NAME] - [BRIEF_CONTEXT for connecting, e.g., "saw your talk at SaaStr" / "we're both in the B2B outbound space"]. Would be great to connect.
```

### LinkedIn DM (Post-Connection)

```
Thanks for connecting, [FIRST_NAME].

[ONE_SENTENCE referencing something specific - their recent post, company news, mutual connection].

[BRIDGE to your product - what you help companies like theirs do].

[SOFT_CTA - e.g., "Happy to share how if useful."]
```

## Follow-Up Templates

### Follow-Up 1: Value-Add (Day 3–4)

```
Subject: Re: [ORIGINAL_SUBJECT]

[FIRST_NAME],

[SHARE_SOMETHING_USEFUL - e.g., a relevant article, case study, data point, or industry insight]. Thought this might be relevant given [CONTEXT_FROM_FIRST_EMAIL].

[RESTATE_CTA - softer than first touch]

[YOUR_NAME]
```

### Follow-Up 2: Social Proof (Day 7–8)

```
Subject: Re: [ORIGINAL_SUBJECT]

[FIRST_NAME],

[SPECIFIC_CUSTOMER_RESULT - e.g., "[COMPANY_NAME] was dealing with the same [PROBLEM]. After [TIME_PERIOD], they [RESULT - e.g., increased reply rates by 3x / cut list building time by 80%]."]

[SOFT_CTA]

[YOUR_NAME]
```

### Follow-Up 3: Breakup (Day 14)

```
Subject: Re: [ORIGINAL_SUBJECT]

[FIRST_NAME],

Not trying to clog your inbox. If [YOUR_PRODUCT_CATEGORY] isn't a priority right now, no worries.

If it is, happy to share how [SHORT_VALUE_PROP].

Either way - [GENUINE_CLOSER, e.g., "good luck with the Series B" / "hope the SDR hiring goes well"].

[YOUR_NAME]
```

## Reply Handling

### Positive Reply

Action: Respond within 1 hour. Keep momentum. Don't over-explain. Propose a specific time or next step.

```
Great to hear, [FIRST_NAME]. How about [SPECIFIC_DAY/TIME]? Happy to keep it to 15 min.
```

### Objection: "Not the right time"

Action: Acknowledge, add value, set a future anchor.

```
Totally get it, [FIRST_NAME]. [OPTIONAL: share one quick resource]. Happy to circle back in [TIMEFRAME - e.g., next quarter]. When would make sense?
```

### Objection: "We already use [COMPETITOR]"

Action: Don't bash the competitor. Differentiate on one specific dimension.

```
Makes sense - [COMPETITOR] is solid for [WHAT_THEY'RE_KNOWN_FOR]. Where we're different is [ONE_SPECIFIC_DIFFERENTIATOR]. Worth a quick comparison?
```

### Objection: "Send me more info"

Action: Send something short and specific, with a clear next step.

```
Sure thing. Here's [SPECIFIC_RESOURCE - one-pager, case study, 2-min video]. Happy to walk through anything live if helpful - does [DAY] work?
```

## Personalization Variables

| Variable | Description | Source |
|----------|-------------|--------|
| `[FIRST_NAME]` | Prospect first name | CRM / enrichment tool |
| `[COMPANY_NAME]` | Prospect company | CRM / enrichment tool |
| `[SIGNAL_REFERENCE]` | Specific buying signal observed | Signal monitoring / research |
| `[PERSONA_TITLE]` | Prospect's job title | LinkedIn / enrichment |
| `[COMPANY_STAGE]` | Growth stage or company size bucket | Crunchbase / enrichment |
| `[SOCIAL_PROOF]` | Relevant customer name or metric | Internal case studies |
| `[COMPETITOR]` | Competitor product they currently use | Tech stack data / research |

---

## Filled-In Examples

### Example 1: DevTools Company

**Tone:** Technical, peer-to-peer, no marketing fluff. Write like an engineer talking to an engineer.

**First touch:**
```
Subject: Your Snowflake migration

Alex,

Saw your team just moved to Snowflake - congrats. Most data teams we talk to hit a wall with pipeline observability about 3 months in.

DataCo cut their pipeline debugging time by 70% after switching from manual monitoring. Worth a quick look?

- Sarah
```

### Example 2: HR Tech Company

**Tone:** Warm, professional, empathetic. HR leaders deal with people problems - mirror that.

**First touch:**
```
Subject: Scaling your People team

Jordan,

Noticed you're hiring 4 HR Business Partners - exciting growth. At that stage, most People teams start drowning in manual processes that worked fine at 200 employees but break at 500.

Acme Corp automated their entire onboarding workflow and saved 15 hours/week. Relevant to share?

- Mike
```
