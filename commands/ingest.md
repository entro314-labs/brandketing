---
description: Ingest a raw source file into the context store by normalizing it into structured objects. Usage: /brandketing:ingest <source-path> <pipeline>. Pipelines: product-truth | customer-truth | commercial-truth | market-truth | proof-truth
---

# Ingest Source into Context Store

Run the **normalizer** agent on a raw source file and write the resulting structured objects to the context store.

## Arguments

- `<source-path>` — path to the raw source file (transcript, doc, ticket export, competitor page, etc.)
- `<pipeline>` — which pipeline to run:
  - `product-truth` — docs, PRDs, changelogs, demo transcripts, screenshots → Capability objects
  - `customer-truth` — call transcripts, support tickets, onboarding notes, reviews → Pain, Quote, UseCase objects
  - `commercial-truth` — CRM exports, won/lost reasons, account data → Persona objects
  - `market-truth` — competitor pages, comparison content, review sites → Competitor, Cliche objects
  - `proof-truth` — analytics exports, case studies, internal wins → Proof objects

## Process

1. Read the source file at `<source-path>`.
2. Load `context/schemas/pipelines.json` from this plugin to map the selected pipeline to its schema files and store files.
3. Load the relevant schema files from the plugin's `context/schemas/` directory.
4. Invoke the **normalizer** agent with the source content, pipeline type, and schema.
5. The normalizer will extract structured objects with confidence scores and source references.
6. Append new objects to the relevant store file in `.brandketing/context/store/` within the project directory. If a store file doesn't exist, initialize it from the matching starter file in this plugin's `context/store/` directory.
7. Report: how many objects were created, average confidence, any items flagged as low-evidence (confidence < 0.5).

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
- Source reference must always be included — never extract without citing origin.
