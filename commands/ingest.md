---
description: Ingest a raw source file into the context store by normalizing it into structured objects. Usage: /brandketing:ingest <source-path> <pipeline>. Pipelines: product-truth | customer-truth | commercial-truth | market-truth | proof-truth
---

# Ingest Source into Context Store

Run the **normalizer** agent on a raw source file and write the resulting structured objects to the context store.

## Arguments

- `<source-path>` - path to the raw source file (transcript, doc, ticket export, competitor page, etc.)
- `<pipeline>` - which pipeline to run:
  - `product-truth` - docs, PRDs, changelogs, demo transcripts, screenshots → Capability objects
  - `customer-truth` - call transcripts, support tickets, onboarding notes, reviews → Pain, Quote, UseCase objects
  - `commercial-truth` - CRM exports, won/lost reasons, account data → Persona objects
  - `market-truth` - competitor pages, comparison content, review sites → Competitor, Cliche objects
  - `proof-truth` - analytics exports, case studies, internal wins → Proof objects

## Process

1. Read the source file at `<source-path>`.
2. Load the schema for the target pipeline from `${CLAUDE_PLUGIN_ROOT}/context/schemas/`.
3. Invoke the **normalizer** agent with the source content, pipeline type, and schema.
4. The normalizer will extract structured objects with confidence scores and source references.
5. Append new objects to the relevant store file in `context/store/` within the project directory. If a store file doesn't exist, create it with an empty array first.
6. Report: how many objects were created, average confidence, any items flagged as low-evidence (confidence < 0.5).

## Context Store Location

The context store lives at `.brandketing/context/store/` relative to the project root. Create it if it doesn't exist.

Store files:
- `capabilities.json`
- `pains.json`
- `quotes.json`
- `use_cases.json`
- `personas.json`
- `competitors.json`
- `cliches.json`
- `proofs.json`

## Rules

- Never overwrite existing approved objects (status: "approved"). Append only.
- Flag duplicate objects by similarity rather than silently merging.
- Low-confidence extractions (< 0.5) should be added with status: "needs-review" and a note explaining why confidence is low.
- Source reference must always be included - never extract without citing origin.
