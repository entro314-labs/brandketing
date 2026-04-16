# brandketing

A Claude Code plugin that turns raw product and customer data into a living marketing intelligence context store — and compiles it into briefs and copy on demand.

## What it does

Instead of filling out a brief from scratch every time, this plugin maintains a **context store** that accumulates structured marketing objects over time. Each asset you generate pulls from approved, sourced, scored objects — not from memory or imagination.

The two source documents behind this system:
- `brief-harness.md` — automated brief compilation from 5 data pipelines
- `marketing-harness.md` — 6-step strategy workflow + critic pass for copy generation

## Install

```
/plugin install brandketing@claude-plugins-official
```

Or from GitHub:
```
/plugin install brandketing@github:entro314-labs/brandketing
```

## Commands

| Command | What it does |
|---|---|
| `/brandketing:ingest <source> <pipeline>` | Normalize a raw source file into structured context objects |
| `/brandketing:review [type]` | Approve, reject, or edit pending objects |
| `/brandketing:brief <deliverable> [icp]` | Compile a brief from approved objects |
| `/brandketing:generate [deliverable] [icp]` | Run strategist + critic, output full copy hierarchy |
| `/brandketing:status` | Show context store freshness and object counts |

## Pipelines

| Pipeline | Source types | Output objects |
|---|---|---|
| `product-truth` | Docs, PRDs, changelogs, demos | Capability |
| `customer-truth` | Call transcripts, tickets, reviews | Pain, Quote, UseCase |
| `commercial-truth` | CRM, won/lost, account data | Persona |
| `market-truth` | Competitor pages, comparison content | Competitor, Cliche |
| `proof-truth` | Analytics, case studies, wins | Proof |

## Agents

- **normalizer** — converts raw sources into typed, scored objects
- **compiler** — assembles brief sections from approved objects, filtered by ICP
- **strategist** — runs the 6-step strategy workflow to produce a messaging hierarchy
- **critic** — red-teams every output line and rewrites what's weak

## Context store

Each project gets its own store at `.brandketing/context/store/` (not committed to git).

Objects: `capabilities`, `pains`, `quotes`, `use_cases`, `personas`, `competitors`, `cliches`, `proofs`, `brand`

Each object carries: confidence score, source references, freshness date, and approval status.

## Workflow

```
1. /brandketing:ingest call-transcripts.txt customer-truth
2. /brandketing:ingest product-docs.md product-truth
3. /brandketing:review
4. /brandketing:generate homepage-hero icp-1
```

For a lightweight version without the context store, see **brandketing-quick**.

## Design principles

- **Machine assembles, human approves.** The system proposes; a human decides ICP, category, and positioning bet.
- **Every claim has a source.** Objects without source references are not created.
- **Freshness is tracked.** Static / slow-moving / fast-moving layers refresh on different cadences.
- **Copy goes through a critic.** Every generation runs a red-team pass before output.
