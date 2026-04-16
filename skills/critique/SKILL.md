---
name: critique
description: This skill should be used when red-teaming marketing copy, auditing for failure modes, rewriting weak lines, or when the critic agent needs the failure mode taxonomy and rewrite rules.
---

# Critique Skill - Copy Audit Framework

## Failure Mode Taxonomy

| Label | Definition | Common Pattern |
|---|---|---|
| `generic` | Could appear in any SaaS product | "streamline your workflows", "save time and money" |
| `feature-led` | Leads with what exists, not what it does for the buyer | "our dashboard gives you visibility" |
| `paraphrased-docs` | Readme with adjectives | "the system includes an onboarding wizard that helps users" |
| `weak-differentiation` | Competitor could say this verbatim | "collaborative", "real-time", "intuitive" |
| `unsupported-claim` | Bold promise without mechanism or proof | "10x faster" with no data or mechanism |
| `too-safe` | Technically correct, produces no signal | "helps teams work better" |
| `too-hypey` | Overclaimed beyond evidence | "completely transforms how you work" |
| `too-abstract` | Means nothing without a concrete anchor | "unlock your potential" |
| `clowny` | Tries too hard to be clever | punny headlines that undermine credibility |
| `arrogant` | Assumes dominance the product hasn't earned | "the only platform that..." without proof |
| `boring` | Accurate, zero resonance | "a platform for managing X" |

## Rewrite Rules by Failure Mode

**feature-led:**
Find the outcome or pain the feature relates to. Lead with that instead.
> "our onboarding wizard" → "new users get to first value before setup turns into a project"

**generic:**
Add one specific anchor: a number, a named friction, a concrete moment, a before/after.
> "save time" → "cut the setup calls your team currently handles manually"

**too-abstract:**
Ground it in a visible scenario - what does the buyer see, feel, or stop dealing with?
> "unlock your potential" → "your first campaign goes live before you finish onboarding"

**unsupported-claim:**
Either find proof in the brief (metric or mechanism) or soften to what can be substantiated.
> "10x faster" → "most teams ship their first campaign in the same week they start"

**too-safe:**
Sharpen the tension - what is the cost of not having this? What happens if the problem persists?
> "helps teams work better" → "prevents the three-week setup drag that kills most rollouts"

**clowny or arrogant:**
Flatten the register. Trust the idea to carry the weight.
> "we're not just different, we're different differently" → delete; use the actual differentiator

## Audit Checklist

Before finishing any critique pass, verify:
- [ ] Every hero line is outcome-led, not feature-led
- [ ] Every claim is backed by a mechanism or metric from the brief
- [ ] No banned words appear without evidence
- [ ] No generic SaaS phrases remain
- [ ] Subheads explain the mechanism, not just restate the promise
- [ ] Bullets show translated benefits, not feature names
- [ ] CTAs are specific to action and stage, not generic ("Get started" → "See it in your stack")
- [ ] Tagline creates tension or reframe, not just a tagline shape

## Tone Calibration Reference

Copy should sit here on these axes:
- Sophistication: high
- Warmth: medium
- Energy: medium-high
- Humor: low
- Confidence: high but evidence-backed
- Sentence length: short to medium
- Jargon: only audience-native jargon
- Emotionality: controlled, not theatrical

What to avoid:
- Startup cliché language
- Empty superlatives
- Exclamation marks
- Smugness
- Meme voice
- Investor-deck abstraction
- Feature-dump paragraphs
