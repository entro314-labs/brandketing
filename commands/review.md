---
description: Review and approve/reject pending objects in the context store. Usage: /brandketing:review [type]. Types: capabilities | pains | quotes | use_cases | personas | competitors | cliches | proofs | all
---

# Review Context Store Objects

Present pending context store objects one at a time for human approval, rejection, or editing.

## Arguments

- `[type]` (optional) - which object type to review. Defaults to `all` in order of pipeline priority.

## Process

1. Load all objects with `status: "pending"` or `status: "needs-review"` from `.brandketing/context/store/<type>.json`.
2. For each object, display:
   - Object type and name/label
   - Key content fields (formatted for readability, not raw JSON)
   - Confidence score and source references
   - Freshness date
3. Ask the human for one of:
   - **approve** - set status: "approved"
   - **reject** - set status: "rejected", ask for brief reason
   - **edit** - open the object for inline editing, then approve
   - **skip** - leave as pending, move to next
   - **stop** - end review session
4. After each decision, update the store file immediately.
5. Report a session summary: approved / rejected / skipped / remaining.

## Display Format

Show each object like this:

```
──────────────────────────────────────────
[TYPE] Capability #3 of 12 pending
──────────────────────────────────────────
Name:        Guided setup sequence
Who cares:   New users, team leads rolling out
Moment:      First login / team onboarding
Friction:    Blank-page confusion, wrong-turn setup
Outcome:     Users reach first value without hand-holding
Proof:       Demo transcript, onboarding analytics event "setup_completed"
Confidence:  0.74
Source:      product-docs/onboarding.md (ingested 2026-04-16)

→ approve / reject / edit / skip / stop
```

## Rules

- Never show raw JSON to the human - always format for readability.
- Group by type when reviewing "all" - finish one type before starting the next.
- Highlight objects with confidence < 0.6 with a warning.
- Do not modify any field not explicitly changed by the human.
