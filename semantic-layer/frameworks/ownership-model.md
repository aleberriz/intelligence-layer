# Semantic Layer Ownership Model

*The Data Analyst and Analytics Engineer Roles*

Who should own the semantic layer: the Analytics Engineer (AE) or the Data Analyst (DA)?

The question is often framed as a binary, but it shouldn't be. Because both roles have legitimate claims and blind spots, and failure modes on each side are real and asymmetric. So getting the ownership model wrong yields either a technically correct but semantically wrong layer that AI agents misinterpret, or a semantically correct but technically broken layer that silently overcounts.

Therefore, the right ownership model is a hybrid one in which clear role boundaries are set based on the technical realities of semantic layer architecture, as well as the organizational realities of who holds which knowledge.

---

## The AE's Legitimate Claim: Technical Complexity Is Real

The AE counterargument is not just territorial. It is technically grounded, so dismissing it is a mistake.

Modern semantic layers are not just thin wrappers for SQL. As the MetricFlow founders noted, even basic metrics can involve hundreds of lines of optimized SQL to handle joins, time analysis, and breakdowns. [[dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership)]

The main issue is **grain** — the core level of data granularity in a fact table. Grain is the most important and least reversible decision in semantic layer design:

* If a fact table is defined at order-level grain, you cannot accurately answer product-level questions (basket composition, SKU-level margins) without rebuilding the model.
* If a model joins tables with mismatched grains without a valid matching rule, a single sale can be duplicated across multiple marketing events (e.g., leading to overcounted revenue).
* Grain errors produce reports that look plausible but are mathematically wrong, and they propagate silently to every downstream stakeholder: dashboards, embedded applications, and AI agents.

[[Gromov — "The 7 Irreversible Decisions in Semantic Layer Architecture", Mar 2026](https://medium.com/towards-data-engineering/the-7-irreversible-decisions-in-semantic-layer-architecture-e2316004108c)]

**Level of Detail (LOD)** expressions compound this. LOD calculations allow metrics to be computed at a granularity different from the current visualization context. This is useful for cohort retention, per-customer averages, or market share calculations. But when applied incorrectly (wrong anchor dimension, missing filters, incorrect scope), they produce results that are numerically wrong in ways that are hard to detect visually. An analyst can easily configure an LOD expression without realizing that the underlying join logic makes it undefined.

The AE's real case: if the DA gets grain wrong or sets LOD expressions without knowing joins, mistakes go unnoticed and spread. So AE technical checks aren't bureaucracy: they are needed.

---

## The DA's Legitimate Claim: Business Meaning Cannot Be Delegated

The AE's technical competence is real. But technical competence does not transfer into semantic correctness.

"Active subscriber" is not a SQL problem. It is a business definition problem. Whether it means opening an email in the last 90 days, having at least one active form, not having churned, and having a paid plan, or something else entirely, depends on the context that the analyst distills through increased stakeholder context awareness. So while an AE can build a technically valid metric for any of these definitions, they cannot know which one is correct without guidance.

This is more important for AI agents than dashboards. Because dashboard users may spot weird numbers, but AI agents can't (as they just return what the semantic layer gives). So a wrong metric can easily become a wrong confident answer. [[dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership)]

Therefore, the `ai_context` field, the `description`, and the `synonyms` (e.g., the decision about what constitutes revenue vs. gross revenue vs. net revenue after credits) are all business-meaning decisions. So an AE who owns these without DA input produces a model that is technically coherent and semantically arbitrary.

Omni's authoring model reflects this. The workbook-to-model promotion flow lets DAs define metric logic in a workbook (validating against real business questions) before promoting it to the shared model. The product assumes the person who understands the question defines the answer. [[Omni — "Put your semantic layer where the action happens"](https://omni.co/blog/put-your-semantic-layer-where-the-action-happens)]

---

## The Ownership Model

But the answer to the initial question cannot be "both own everything together". Because that creates unclear accountability. Instead, the solution is to separate concerns along a clear boundary: meaning vs. correctness.

| Responsibility | Owner | Rationale |
|---|---|---|
| Business metric definitions (what does "active subscriber" mean?) | DA | The DA should distill this from closer contact with business stakeholders |
| `description`, `ai_context`, `synonyms` fields | DA | The DA's judgment should determine what AI agents "interpret" |
| Access grants (what business concept does this grant govern?) | DA | Business rules, not technical rules |
| Topic scoping (what questions should this topic answer?) | DA | Requires understanding of how the business consumes data |
| Grain validation (is this fact table at the right level of detail?) | AE | Requires understanding of the underlying data model and join graph |
| LOD expression review (is this aggregation mathematically valid?) | AE | Requires SQL and dimensional modeling expertise |
| Join correctness (will this join fan out or produce duplicates?) | AE | Grain and fan trap analysis is AE territory |
| Performance (will this definition query efficiently at scale?) | AE | Warehouse and query optimization expertise |
| Technical review before AI agent exposure | AE | Final sign-off on correctness before external consumers use the model |

High-level practical workflow:

1. DA drafts metric definitions in a workbook or staging environment and validates them against real business questions.
2. AE reviews the technical implementation (grain, joins, LOD correctness, performance).
3. Both sign off before the definition is promoted to the shared model and served to external AI agents.
4. Neither publishes unilaterally.

The risk of skipping either review:

* DA-absent: technically valid definitions that answer the wrong question. An AI agent querying "monthly recurring revenue" gets a number that excludes the credits the business always excludes, because the AE didn't know to exclude them.
* AE-absent: semantically correct definitions that are mathematically broken. An AI agent querying "average revenue per creator" gets a number inflated by a trap join that no one caught because the DA didn't know to check.

---

## The AI Agent Implication

The stakes of this ownership question are higher than they were in a dashboard-only world.

On a dashboard, a wrong number is visible to a human with business context who can flag it. In a semantic layer serving AI agents via MCP, the same wrong number is invisible because the agent returns a confident answer with no signal that the underlying definition is flawed.

This raises the bar for semantic layer governance. The `ai_context` field in OSI-compliant semantic layers is not optional. It is the primary mechanism by which the semantic layer communicates intent to an AI consumer. A model without well-authored AI context fields will be misused by AI agents. Although not by any fault of the agent, but by the failure of the governance model that produced the layer.

The DA who knows this isn't just a dashboard builder who writes YAML. But the main author of the data-to-AI agent interface. That's a new role, which calls for ownership.

---

## References

* [dbt Labs — "Who should own the semantic layer?"](https://www.getdbt.com/blog/semantic-layer-ownership) (Nov 2025)  
  The most thorough public treatment of this question; the hybrid model described here aligns with their conclusion while being more specific about role boundaries
* [Gromov — "The 7 Irreversible Decisions in Semantic Layer Architecture"](https://medium.com/towards-data-engineering/the-7-irreversible-decisions-in-semantic-layer-architecture-e2316004108c) (Mar 2026)  
  Grain, LOD, and join correctness as irreversible architectural decisions; the technical foundation for the AE review requirement
* [Omni — "Put your semantic layer where the action happens"](https://omni.co/blog/put-your-semantic-layer-where-the-action-happens)  
  Omni's authoring model as a product reflection of the DA-first metric definition
* [Omni — "The case for a BI semantic layer on top of dbt"](https://omni.co/blog/bi-semantic-layer-on-top-of-dbt)  
  The dbt ↔ Omni layering pattern and why both layers serve different ownership needs
* [OSI Specification](https://open-semantic-interchange.org/)  
  The vendor-agnostic core classes (Semantic Model, Data Sets, Fields, Measures, Dimensions, Relationships) that frame the ownership question, independent of any specific tool
