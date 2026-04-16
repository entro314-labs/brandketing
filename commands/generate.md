---
description: Generate marketing copy from the context store or a provided brief. Runs the 6-step strategy workflow then the critic pass. Usage: /brandketing:generate [deliverable] [icp] or pipe in an existing brief.
---

# Generate Marketing Copy

Run the **strategist** agent (6-step strategy workflow) followed by the **critic** agent (red-team pass) to produce a complete copy hierarchy.

## Arguments

- `[deliverable]` (optional) - if provided, compiles a brief first via the compiler agent. If omitted, uses the most recent compiled brief from `.brandketing/briefs/`.
- `[icp]` (optional) - passed to the compiler when compiling a brief.

## Alternatively

Paste a brief directly into the conversation. The strategist will use it as input without touching the context store.

## Process

1. **Source the brief:**
   - If a deliverable is specified: run `/brandketing:brief <deliverable> [icp]` first.
   - If no deliverable: load the most recent brief from `.brandketing/briefs/`.
   - If a brief is pasted inline: use it directly.

2. **Run the strategist agent** (6 steps):
   - Step 1: Extract product truth table
   - Step 2: Translate capabilities to market meaning
   - Step 3: Generate 3–5 message territories
   - Step 4: Score and rank territories, select primary + 2 secondary
   - Step 5: Write the full messaging hierarchy for the primary territory
   - Step 6: Self-critique and rewrite weak lines

3. **Human checkpoint:** Present the ranked territories. Ask which primary territory to proceed with. Default to the highest-scored if no input within 30 seconds of display.

4. **Run the critic agent** on the Step 5 output:
   - Label every line with any failure modes found
   - Rewrite flagged lines
   - Return clean final output

5. Save output to `.brandketing/copy/<deliverable>-<icp>-<date>.md`.

## Output Structure

```
A. Product truth map
B. Benefit and meaning map
C. Ranked message territories (with scores)
D. Final messaging hierarchy
   - Core brand message
   - 5 headline options
   - 3 subhead options
   - 3 message pillars + support bullets
   - 3 CTA options
   - 3 tagline options
E. Critic audit + revisions
```

## Rules

- Never skip the territory selection checkpoint - human must approve the direction.
- Never skip the critic pass - every generation goes through audit.
- Do not add features or capabilities not present in the brief.
- If the brief has empty or low-confidence sections, flag them before generating rather than filling them with invented content.
