# brandketing

A Codex-compatible marketing intelligence plugin that turns raw product and customer data into a local context store, then compiles that data into briefs and copy on demand.

## Compatibility

- Codex: `.codex-plugin/plugin.json`
- Claude Code: `.claude-plugin/plugin.json`

## What it does

Instead of filling out a brief from scratch every time, this plugin maintains a **context store** that accumulates structured marketing objects over time. Each asset you generate pulls from approved, sourced, scored objects — not from memory or imagination.

The repo is split across:
- `commands/` for the operator workflows
- `agents/` for normalization, compilation, strategy, and critique
- `skills/` for the reusable guidance those agents rely on
- `context/schemas/` for the object definitions used during ingestion
- `context/store/` for starter files aligned with the runtime store format

## Installation

For Codex, this repo already contains the required marketplace-facing manifest at `.codex-plugin/plugin.json`.

For local testing, use this repository as the plugin root in a Codex setup that supports local plugins. The existing `.claude-plugin/plugin.json` is kept for Claude Code compatibility.

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

Each target project gets its own runtime store under `.brandketing/` (not committed to git):

- `.brandketing/context/store/`
- `.brandketing/briefs/`
- `.brandketing/copy/`

Objects: `capabilities`, `pains`, `quotes`, `use_cases`, `personas`, `competitors`, `cliches`, `proofs`, `brand`

Each object carries: confidence score, source references, freshness date, and approval status.

## Workflow

```
1. /brandketing:ingest call-transcripts.txt customer-truth
2. /brandketing:ingest product-docs.md product-truth
3. /brandketing:review
4. /brandketing:generate homepage-hero icp-1
```

## Design principles

- **Machine assembles, human approves.** The system proposes; a human decides ICP, category, and positioning bet.
- **Every claim has a source.** Objects without source references are not created.
- **Freshness is tracked.** Static / slow-moving / fast-moving layers refresh on different cadences.
- **Copy goes through a critic.** Every generation runs a red-team pass before output.
