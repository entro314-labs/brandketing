---
name: compile
description: This skill should be used when assembling a marketing brief from approved context store objects, mapping object types to brief sections, filtering by ICP, ranking objects for inclusion, or when the compiler agent needs assembly guidance.
---

# Compile Skill — Brief Assembly Logic

## Section Assembly Rules

### PRODUCT

Select top 3–5 Capability objects ranked by:
`confidence × icp_relevance_score`

Where `icp_relevance_score` is 1.0 if the Capability's `who_cares` includes the target ICP, 0.5 if related, 0.0 if irrelevant.

Synthesize into one paragraph: what the product does, for whom, in what category. Include chosen category framing.

### PRODUCT EVIDENCE

All approved Capability objects, grouped by user-visible area. Format as cards:
- Name | What user can do | Friction removed | Outcome | Proof source

Do not include internal implementation details unless they create a user-visible advantage.

### ICP

Use the matched or highest-confidence Persona object. Format:
- Role, company type, sophistication
- Buying trigger
- What they care about (top 3)
- Typical objections
- Evidence from commercial-truth pipeline

### TOP USE CASES

Filter UseCase objects by ICP match. Rank by `evidence_count × confidence`. Select top 3–5.

Format each as:
- Job statement (framed as an outcome, not a feature)
- Trigger moment
- Relevant capability names
- Evidence count

### KNOWN PAINS

Filter Pain objects by ICP persona match. Rank by `severity × frequency`. Select top 5.

Always include both `surface_pain` and `hidden_pain`. If hidden_pain is missing, flag the entry.

### VOICE OF CUSTOMER

Filter Quote objects tagged to the top pain themes from KNOWN PAINS. Rank by `vividness`. Select top 6–10.

Quotes must remain verbatim — never paraphrase.

### COMPETITORS / ALTERNATIVES

All approved Competitor objects sorted by category:
1. Direct competitors
2. Indirect tools
3. Internal workflows
4. Agencies / consultants
5. Spreadsheets / manual ops
6. Status quo / do nothing

### CATEGORY CLICHÉS TO AVOID

All approved Cliche objects. Format as a list of phrases with why_weak explanation.

### PROOF

Filter Proof objects by relevance to deliverable type. Prefer numeric first, mechanistic second. Rank by confidence. Select top 3–5.

### BRAND GUARDRAILS

Load Brand object from store. Include all fields: tone axes, words to favor, words to avoid, syntax preferences, sample headlines on/off brand.

### DELIVERABLE

Populate from command arguments:
- `type` — homepage-hero, sales-narrative, ad-headlines, etc.
- `channel` — web, email, paid, sales deck, etc.
- `audience` — ICP label
- `stage` — awareness, consideration, activation, etc.
- `objective` — what the asset must achieve
- `length constraints` — word count, format requirements

## Freshness Warnings

Apply stale thresholds by layer:
- Static (brand): flag if > 90 days since freshness date
- Slow-moving (personas, competitors, cliches): flag if > 30 days
- Fast-moving (capabilities, pains, quotes, proofs): flag if > 7 days

## Missing Section Protocol

If a section has no approved objects:
- Write: `[NO APPROVED DATA — requires ingestion via /brandketing:ingest]`
- Specify which pipeline to run
- Do not invent placeholder content
