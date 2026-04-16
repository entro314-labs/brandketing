---
name: ingest
description: This skill should be used when ingesting raw marketing sources into the brandketing context store, normalizing content into structured objects, applying source weighting, or when the normalizer agent needs schema and pipeline guidance.
---

# Ingest Skill — Context Object Schemas and Normalization Rules

## Object Schemas

### Capability
```json
{
  "id": "cap_<uuid>",
  "type": "capability",
  "name": "",
  "user_visible_description": "",
  "who_cares": "",
  "trigger_moment": "",
  "friction_removed": "",
  "outcome_created": "",
  "second_order_outcome": "",
  "table_stakes_or_differentiator": "table-stakes | parity | differentiated | ownable",
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "product-truth"
}
```

### Pain
```json
{
  "id": "pain_<uuid>",
  "type": "pain",
  "surface_pain": "",
  "hidden_pain": "",
  "persona": "",
  "stage": "awareness | consideration | activation | retention | expansion",
  "frequency": 0.0,
  "severity": 0.0,
  "downstream_consequence": "",
  "evidence": [],
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "customer-truth"
}
```

### Quote
```json
{
  "id": "quote_<uuid>",
  "type": "quote",
  "verbatim": "",
  "persona": "",
  "stage": "",
  "pain_theme": "",
  "product_area": "",
  "sentiment": "positive | negative | neutral | mixed",
  "vividness": 0.0,
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "customer-truth"
}
```

### UseCase
```json
{
  "id": "usecase_<uuid>",
  "type": "use_case",
  "job_statement": "",
  "trigger_moment": "",
  "persona": "",
  "pain_before": "",
  "desired_outcome": "",
  "relevant_capability_ids": [],
  "evidence_count": 0,
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "customer-truth"
}
```

### Persona
```json
{
  "id": "persona_<uuid>",
  "type": "persona",
  "label": "",
  "role": "",
  "company_type": "",
  "sophistication": "low | medium | high",
  "buying_trigger": "",
  "care_about": [],
  "typical_objections": [],
  "evidence": [],
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "commercial-truth"
}
```

### Competitor
```json
{
  "id": "comp_<uuid>",
  "type": "competitor",
  "name": "",
  "category": "direct | indirect | internal-workflow | agency-consultant | spreadsheet-manual | status-quo",
  "key_claims": [],
  "weakness": "",
  "overlap_with_us": "",
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "market-truth"
}
```

### Cliche
```json
{
  "id": "cliche_<uuid>",
  "type": "cliche",
  "phrase": "",
  "semantic_variants": [],
  "why_weak": "",
  "category_saturation": "low | medium | high",
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "market-truth"
}
```

### Proof
```json
{
  "id": "proof_<uuid>",
  "type": "proof",
  "claim": "",
  "proof_type": "numeric | mechanistic",
  "metric_or_mechanism": "",
  "scope": "",
  "freshness_of_data": "",
  "attributable_to_product": true,
  "audience_understandable": true,
  "evidence": [],
  "source_refs": [],
  "confidence": 0.0,
  "freshness": "",
  "status": "pending",
  "pipeline": "proof-truth"
}
```

## Confidence Scoring Guide

| Score | Meaning |
|---|---|
| 0.9–1.0 | Multiple source types, strong evidence, recent |
| 0.7–0.9 | Good evidence, 1–2 source types |
| 0.5–0.7 | Plausible but thin evidence, single source |
| < 0.5 | Weak or inferred — flag for needs-review |

## Hidden Pain Inference

To infer hidden pain from explicit complaints:
1. Take the surface complaint.
2. Ask: what downstream consequence does this create if left unresolved?
3. Ask: what does the user misdiagnose about their own situation?
4. Combine: explicit complaint + funnel drop-off + hand-holding demand + business consequence.

Example:
- Surface: "setup takes too long"
- Hidden: "teams lose momentum before they ever reach the moment that makes the product feel valuable"
