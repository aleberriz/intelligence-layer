# Reading List

Annotated references across the three pillars. Updated as sources are read and validated — not added on reputation alone.

---

## Causal Inference & Experimentation

### *Trustworthy Online Controlled Experiments*
Kohavi, Tang & Xu — Cambridge University Press
**Why it matters**: The definitive practitioner reference on A/B testing at scale. Written by the people who built experimentation infrastructure at Microsoft, Google, and Airbnb. Covers the full lifecycle: metric selection, power analysis, statistical validity, common pitfalls (peeking, novelty effects, network effects), and org-level rollout. The chapter on guardrail metrics and OEC design is essential reading before advising on any A/B testing program.
**Status**: In progress

### *The Effect: An Introduction to Research Design and Causality*
Nick Huntington-Klein — [free at theeffectbook.net](https://theeffectbook.net)
**Why it matters**: The most accessible modern introduction to causal inference for practitioners. Covers DAGs, difference-in-differences, regression discontinuity, instrumental variables, and synthetic control — all with Python/R code and no unnecessary econometrics overhead. The right starting point before diving into more technical treatments.
**Status**: Queued

---

## Semantic Layer & Analytics Engineering

### Omni Documentation
[docs.omni.co](https://docs.omni.co)
**Why it matters**: Primary reference for the semantic layer work. The modeling section (topics, dimensions, measures, access grants, AI optimization) is where the leverage is — not the dashboarding UI. The `ai_context`, `synonyms`, and `description` fields in the model are the interface between the semantic layer and AI agent consumers.
**Key sections**: `modeling/`, `ai/mcp/`, `modeling/develop/ai-optimization/`
**Status**: Ongoing

### dbt Semantic Layer & MetricFlow
[docs.getdbt.com/docs/use-dbt-semantic-layer](https://docs.getdbt.com/docs/use-dbt-semantic-layer/dbt-sl)
**Why it matters**: MetricFlow is the query engine behind dbt's semantic layer. Understanding how semantic models, entities, measures, and dimensions are defined in dbt — and how they integrate with downstream tools like Omni — is critical for the dbt ↔ Omni pattern.
**Status**: Queued

### Open Semantic Interchange (OSI) Specification
[open-semantic-interchange.org](https://open-semantic-interchange.org/) | [GitHub](https://github.com/open-semantic-interchange/OSI)
**Why it matters**: The vendor-agnostic standard for semantic model exchange, backed by 40+ organizations including Omni, dbt Labs, Snowflake, Databricks, Salesforce, and ThoughtSpot. Understanding the OSI core classes (Semantic Model, Data Sets, Fields, Measures, Dimensions, Relationships) provides a portable mental model that doesn't expire when tools change. The frameworks in `semantic-layer/` are designed to align with this spec.
**Status**: In progress

---

## Agentic AI & MCP

### Model Context Protocol Specification
[modelcontextprotocol.io](https://modelcontextprotocol.io)
**Why it matters**: The spec-level understanding of MCP — what resources, tools, and prompts are, how sampling works, how auth is handled, and how different clients consume the same server. Essential for designing Omni MCP integrations that work correctly across Claude Desktop, Cursor, ChatGPT, and Codex.
**Status**: In progress

### omni-claude-skills
[github.com/exploreomni/omni-claude-skills](https://github.com/exploreomni/omni-claude-skills)
**Why it matters**: The reference implementation for AI skills on top of Omni's MCP server. Directly relevant to building reusable, composable analytics workflows for AI agents. Active contributor.
**Status**: Ongoing

---

## Growth & Product Analytics

### GrowthBook Documentation
[docs.growthbook.io](https://docs.growthbook.io)
**Why it matters**: GrowthBook is the preferred open-source platform for A/B testing and RCT management. The docs cover the full experiment lifecycle from a practitioner's perspective: feature flags, statistical engines (frequentist and Bayesian), results analysis, and team workflows. More immediately applicable than academic texts for actually running experiments inside an org.
**Status**: In progress

### *Hacking Growth*
Sean Ellis & Morgan Brown
**Why it matters**: Cross-functional growth experimentation framework. Most useful for the org-level model: how to structure a growth team, what a growth loop looks like, and how to identify the levers worth pulling. Less useful for statistical rigor (see Kohavi for that).
**Status**: Queued

### North Star Playbook
Amplitude
**Why it matters**: Practical framework for connecting input metrics (feature usage, engagement depth) to a North Star metric. Useful for the user behavior → MRR impact work — specifically for identifying which behavioral signals are leading indicators of monetization events.
**Status**: Queued

---

## Short Courses

### DeepLearning.ai Short Courses
[deeplearning.ai/short-courses](https://www.deeplearning.ai/short-courses/)
**Relevant titles**:
- *MCP: Build Rich-Context AI Apps with Anthropic* — directly maps to Omni MCP work
- *AI Agents in LangGraph* — how agentic systems are structured
- *Prompt Engineering for Developers* — foundational
**Status**: Queued
