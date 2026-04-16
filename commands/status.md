---
description: Show the current state of the context store - object counts, approval status, and freshness by layer.
---

# Context Store Status

Display a dashboard of the context store's current state.

## Process

1. Load all store files from `.brandketing/context/store/`.
2. For each object type, count by status: pending / approved / rejected / needs-review.
3. Group objects by refresh cadence layer:
   - **Static** (brand guardrails, category assumptions) - flag if > 90 days old
   - **Slow-moving** (ICP candidates, competitor map, cliché list) - flag if > 30 days old
   - **Fast-moving** (product evidence, VOC, pains, proof) - flag if > 7 days old
4. Show most recent brief and copy outputs.
5. Flag any store files that don't exist yet.

## Output Format

```
── BRANDKETING CONTEXT STORE ─────────────────────
Project: <project-root>
Last updated: <most-recent-ingest-date>

OBJECT COUNTS
  capabilities    12 approved   3 pending   1 rejected
  pains            8 approved   5 pending   0 rejected
  quotes          22 approved   0 pending   2 rejected
  use_cases        4 approved   2 pending   0 rejected
  personas         2 approved   1 pending   0 rejected
  competitors      6 approved   0 pending   0 rejected
  cliches         14 approved   0 pending   0 rejected
  proofs           5 approved   3 pending   1 rejected

FRESHNESS
  static layer    brand.json - last updated 2026-03-15   ✓ fresh
  slow layer      personas.json - last updated 2026-03-20   ✓ fresh
  slow layer      competitors.json - last updated 2026-02-28   ⚠ stale (>30d)
  fast layer      pains.json - last updated 2026-04-10   ✓ fresh
  fast layer      proofs.json - last updated 2026-03-25   ⚠ stale (>7d)

OUTPUTS
  last brief      homepage-hero-icp1-2026-04-14.md
  last copy       homepage-hero-icp1-2026-04-14.md

MISSING
  (none)

Next: run /brandketing:review to process 14 pending objects.
──────────────────────────────────────────────────
```
