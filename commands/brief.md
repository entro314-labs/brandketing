---
description: Compile a marketing brief from approved context store objects. Usage: /brandketing:brief <deliverable> [icp]. Deliverable examples: homepage-hero, sales-narrative, ad-headlines, email-sequence, positioning-statement
---

# Compile Marketing Brief

Run the **compiler** agent to assemble a structured brief from approved context store objects.

## Arguments

- `<deliverable>` — the asset type being briefed. Examples:
  - `homepage-hero` — hero + subhead + 3 pillars + CTA
  - `sales-narrative` — full sales story arc
  - `ad-headlines` — paid ad headline variants
  - `email-sequence` — onboarding or nurture email set
  - `positioning-statement` — core positioning sentence

- `[icp]` (optional) — which ICP to target. If omitted, uses the highest-confidence approved Persona. Examples: `icp-1`, `ops-lead`, `mid-market-saas`

## Process

1. Load all approved objects from `.brandketing/context/store/`.
2. Filter objects by ICP relevance if a persona is specified.
3. Invoke the **compiler** agent with the approved object set, deliverable type, and ICP.
4. The compiler will assemble the brief by mapping:
   - `PRODUCT` → top approved Capability objects + chosen category framing
   - `ICP` → matched Persona object
   - `TOP USE CASES` → top UseCase objects for that ICP
   - `KNOWN PAINS` → top Pain objects ranked by severity × frequency for that ICP
   - `VOICE OF CUSTOMER` → top Quote objects tagged to those pain themes
   - `COMPETITORS` → approved Competitor objects
   - `CATEGORY CLICHÉS TO AVOID` → approved Cliche objects
   - `PROOF` → top Proof objects relevant to deliverable
   - `BRAND GUARDRAILS` → Brand object (static layer)
   - `DELIVERABLE` → specified type + channel + audience + stage + objective
5. Output the compiled brief in the standard format.
6. Save the brief to `.brandketing/briefs/<deliverable>-<icp>-<date>.md`.

## Output Format

The compiled brief follows the structure from brief-harness.md §9. Every field includes:
- Assembled content
- Confidence score (derived from constituent objects)
- Source object IDs
- Freshness of oldest source object

## Rules

- Only use approved objects (status: "approved"). Never pull from pending or rejected.
- If a required section has no approved objects, flag it clearly rather than inventing content.
- Surface the ICP choice to the human before generating — confirm or allow them to change it.
- After compiling, ask: "Review this brief before generating copy? (yes/no)"
