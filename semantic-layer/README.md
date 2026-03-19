# Semantic Layer

Frameworks and patterns for designing semantic layers that serve multiple consumers consistently — dashboards, notebooks, embedded tools, and AI agents via MCP.

The central claim: a well-designed semantic layer is the highest-leverage investment in a modern analytics stack. It is a governance problem masquerading as a tooling problem.

The governing standard for this pillar is the [Open Semantic Interchange (OSI)](https://open-semantic-interchange.org/) — a vendor-agnostic spec for semantic model exchange backed by 40+ organizations including Omni, dbt Labs, Snowflake, and Databricks. The goal is portability: frameworks here should apply regardless of which tool implements the layer. Omni and dbt/MetricFlow are the current implementation choices, both active OSI members.

---

## Subdirectories

### `omni/`
Omni modeling patterns — topic design, dimension and measure definitions, access grants, `ai_context` and `synonyms` fields for AI optimization, and YAML templates. Covers both the authoring layer (workbook-to-model promotion) and the model layer (shared definitions).

Key reference: [Omni Modeling Docs](https://docs.omni.co/modeling/)

### `dbt/`
dbt Semantic Layer integration — MetricFlow metric definitions, semantic models, and how dbt-defined metrics flow downstream into Omni and other MCP-connected consumers. Covers the dbt ↔ Omni integration pattern specifically.

Key reference: [dbt Semantic Layer](https://docs.getdbt.com/docs/use-dbt-semantic-layer/dbt-sl)

### `frameworks/`
Tool-agnostic design principles aligned with the OSI spec: when to define a metric in the transformation layer vs. the BI layer, how to scope topics, consistency guarantees across endpoints, naming conventions, and the governance model for who owns what. These frameworks should hold regardless of which OSI-compatible tools are in the stack.

---

## Design Principles (working notes)

- Metrics belong where they will be maintained — if dbt already transforms the data, define the metric in dbt and expose it; if the metric is BI-layer logic, define it in Omni
- Every measure should have a description and, for AI consumers, an `ai_context` field
- Access grants are semantic layer concerns, not dashboard concerns — define them once
- A topic that tries to answer every question answers none of them well — scope tightly
- Design for the OSI core classes (Semantic Model, Data Sets, Fields, Measures, Dimensions, Relationships) — tool-specific YAML is an implementation detail
