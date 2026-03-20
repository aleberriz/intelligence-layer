# Semantic Layer Ownership Model: DA and AE Roles

## The Question

Who should own the semantic layer — the Analytics Engineer (AE) or the Data Analyst (DA)?

The question is frequently framed as a binary, and it shouldn't be. Both roles have legitimate claims, and both have genuine blind spots. The failure modes on each side are real and asymmetric. Getting the ownership model wrong produces either a *technically correct but semantically wrong* layer that AI agents confidently misinterpret, or a *semantically correct but technically broken* layer that silently double-counts.

This document argues for a specific hybrid model with clear role boundaries — grounded in the technical realities of semantic layer architecture and the organizational realities of who holds which knowledge.

---

## The AE's Legitimate Claim: Technical Complexity Is Real

The AE counterargument is not just territorial — it is technically grounded, and dismissing it is a mistake.

Modern semantic layers are not a thin naming layer on top of SQL. As the MetricFlow founders documented while building dbt's semantic layer, even seemingly simple metrics can generate hundreds of lines of optimized SQL when accounting for proper joins, time series analysis, and dimensional breakdowns. [[dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership)]

The deeper issue is **grain** — the fundamental level of data granularity at which a fact table is defined. Grain is the most consequential and least reversible decision in semantic layer architecture:

- If a fact table is defined at order-level grain, you cannot accurately answer product-level questions (basket composition, SKU-level margins) without rebuilding the model
- If a model joins tables with mismatched grains without a valid matching rule, a single sale can be duplicated across multiple marketing events — revenue appears to increase even though nothing happened
- Grain errors produce reports that look plausible but are mathematically wrong, and they propagate silently to every downstream consumer: dashboards, embedded applications, AI agents

[[Gromov — "The 7 Irreversible Decisions in Semantic Layer Architecture", Mar 2026](https://medium.com/towards-data-engineering/the-7-irreversible-decisions-in-semantic-layer-architecture-e2316004108c)]

**Level of Detail (LOD)** expressions compound this. LOD calculations allow metrics to be computed at a different granularity than the current visualization context — useful for cohort retention, per-customer averages, or market share calculations. When applied incorrectly (wrong anchor dimension, missing filters, incorrect scope), they produce results that are numerically wrong in ways that are hard to detect visually. An analyst can easily configure an LOD expression without realizing the underlying join logic makes it undefined.

The AE's case, honestly stated: if the DA defines grain incorrectly, or configures LOD expressions without understanding the join graph, the error is silent and propagates everywhere. An AE reviewing for technical correctness is not bureaucracy — it is a necessary check.

---

## The DA's Legitimate Claim: Business Meaning Cannot Be Delegated

The AE's technical competence is real. But technical competence does not transfer into semantic correctness.

"Active subscriber" is not a SQL problem. It is a business definition problem. Whether it means *opened an email in the last 90 days and has at least one active form*, or *has not churned and has a paid plan*, or something else entirely — depends on context that lives in the analyst's head, not in the data model. An AE can build a technically valid metric for any of these definitions. They cannot know which one is correct without being told.

This matters more for AI agents than for dashboards. A dashboard user who knows the business can spot a suspicious number. An AI agent has no such calibration — it queries the semantic layer, gets a number, and presents it with confidence. A semantically wrong metric in the semantic layer becomes a confidently wrong answer from the AI agent. [[dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership)]

The DA's case, honestly stated: the `ai_context` field, the `description`, the `synonyms`, the decision about what constitutes revenue vs. gross revenue vs. net revenue after credits — these are all business meaning decisions. An AE who owns these without DA input produces a model that is technically coherent and semantically arbitrary.

Omni's authoring model reflects this explicitly. The workbook-to-model promotion flow is designed for DAs to define metric logic in a workbook context (where they can validate it against real business questions), then promote it to the shared model. The assumption baked into the product is that the person who understands the question is the one who defines the answer. [[Omni — "Put your semantic layer where the action happens"](https://omni.co/blog/put-your-semantic-layer-where-the-action-happens)]

---

## The Ownership Model

The resolution is not "both own everything together" — that produces unclear accountability. It is a division along a clear boundary: **meaning vs. correctness**.

| Responsibility | Owner | Rationale |
|---|---|---|
| Business metric definitions (what does "active subscriber" mean?) | DA | Only the DA has this context |
| `description`, `ai_context`, `synonyms` fields | DA | These are the semantic interface to AI agents — DA judgment determines what agents understand |
| Access grants (what business concept does this grant govern?) | DA | Business rules, not technical rules |
| Topic scoping (what questions should this topic answer?) | DA | Requires understanding of how the business consumes data |
| Grain validation (is this fact table at the right level of detail?) | AE | Requires understanding of the underlying data model and join graph |
| LOD expression review (is this aggregation mathematically valid?) | AE | Requires SQL and dimensional modeling expertise |
| Join correctness (will this join fan out or produce duplicates?) | AE | Grain and fan trap analysis is AE territory |
| Performance (will this definition query efficiently at scale?) | AE | Warehouse and query optimization expertise |
| Technical review before AI agent exposure | AE | Final sign-off on correctness before external consumers use the model |

**The practical workflow:**
1. DA drafts metric definitions in a workbook or staging environment, validated against real business questions
2. AE reviews the technical implementation — grain, joins, LOD correctness, performance
3. Both sign off before the definition is promoted to the shared model and served to external AI agents
4. Neither publishes unilaterally

**The risk of skipping either review:**
- DA-absent: technically valid definitions that answer the wrong question. An AI agent querying "monthly recurring revenue" gets a number that excludes the credits the business always excludes — because the AE didn't know to exclude them.
- AE-absent: semantically correct definitions that are mathematically broken. An AI agent querying "average revenue per creator" gets a number inflated by a fan trap join that no one caught because the DA didn't know to check.

---

## The AI Agent Implication

The stakes of this ownership question are higher than they were in a dashboard-only world.

In a dashboard, a wrong number is visible to a human who has business context and can flag it. In a semantic layer serving AI agents via MCP, the same wrong number is invisible — the agent returns a confident answer with no signal that the underlying definition is flawed.

This raises the bar for semantic layer governance. The `ai_context` field in Omni is not optional decoration. It is the primary mechanism by which the semantic layer communicates intent to an AI consumer. A model without well-authored `ai_context` fields is a model that will be misused by AI agents — not through any fault of the agent, but through the failure of the governance model that produced the layer.

The DA who understands this is not a dashboard builder who also writes YAML. They are the primary author of the interface between the organization's data and its AI agents. That is a different job description, and it requires a different kind of ownership.

---

## References

- [dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership) (Nov 2025) — the most thorough public treatment of this question; the hybrid model described here aligns with their conclusion while being more specific about role boundaries
- [Gromov — "The 7 Irreversible Decisions in Semantic Layer Architecture"](https://medium.com/towards-data-engineering/the-7-irreversible-decisions-in-semantic-layer-architecture-e2316004108c) (Mar 2026) — grain, LOD, and join correctness as irreversible architectural decisions; the technical foundation for the AE review requirement
- [Omni — "Put your semantic layer where the action happens"](https://omni.co/blog/put-your-semantic-layer-where-the-action-happens) — Omni's authoring model as a product reflection of DA-first metric definition
- [Omni — "The case for a BI semantic layer on top of dbt"](https://omni.co/blog/bi-semantic-layer-on-top-of-dbt) — the dbt ↔ Omni layering pattern and why both layers serve different ownership needs
- [OSI Specification](https://open-semantic-interchange.org/) — the vendor-agnostic core classes (Semantic Model, Data Sets, Fields, Measures, Dimensions, Relationships) that frame the ownership question independent of any specific tool
