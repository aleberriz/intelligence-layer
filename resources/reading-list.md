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
**Why it matters**: The reference implementation for AI skills on top of Omni's MCP server. Directly relevant to building reusable, composable analytics workflows for AI agents.
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

### Lenny's Newsletter
[lennysnewsletter.com](https://www.lennysnewsletter.com) | [Podcast](https://www.lennyspodcast.com)
**Why it matters**: The best ongoing practitioner reference for how PLG companies actually think about product metrics, growth loops, and monetization — written by and for people running real products, not academics. Not a structured course; treat it as a living reference. Particularly useful for calibrating which growth questions are worth asking and how high-functioning product teams frame measurement problems.
**Status**: Ongoing reference

---

## Short Courses

### DeepLearning.ai Short Courses
[deeplearning.ai/short-courses](https://www.deeplearning.ai/short-courses/)
Each course is 1–2 hours, free or low cost. Curated below for direct relevance — courses that don't map to the three pillars or the growth analytics domain are excluded regardless of general reputation.

**MCP: Build Rich-Context AI Apps with Anthropic**
The highest-priority course in this list. Taught by Anthropic's Head of Technical Education. Covers MCP client-server architecture, building MCP-compatible applications, and deploying MCP servers. Maps directly to the Omni MCP integration work.

**AI Agents in LangGraph**
The right foundation for understanding how agentic systems are architecturally structured — planning, tool use, reflection, multi-agent communication. Taught by LangChain's co-founder. Understanding this is what separates "I configured an MCP server" from "I understand why agentic analytics works."

**Long-Term Agentic Memory with LangGraph**
Companion to the above. Covers semantic, episodic, and procedural memory types for agents. Relevant for understanding how analytics agents can persist context across sessions — a design consideration when building skills that need to remember user preferences or prior queries.

**Agent Memory: Building Memory-Aware Agents** *(March 2026)*
Memory-first architecture with persistent memory stores, memory extraction and consolidation pipelines, and semantic tool retrieval. The most current treatment of agent memory available.

**Evaluating AI Agents**
Observability, component-level evaluation, and LLM-as-a-Judge patterns. Directly relevant for validating that AI skills built against your semantic layer are actually answering questions correctly — not just returning plausible-looking output.

**Function-Calling and Data Extraction with LLMs**
Function calling is the underlying mechanism behind MCP tools. Understanding it at this level clarifies why MCP works the way it does and how to design tools that LLMs can call reliably.

**Building Your Own Database Agent**
SQL + natural language agent using function calling and the Assistants API. The closest analog to an Omni MCP agent in the DeepLearning.ai catalog — directly applicable to understanding what happens when an AI queries your semantic layer.

**Prompt Engineering for Developers**
Foundational. Short. Still relevant — especially for analytics contexts where prompt precision directly affects whether a query returns the right metric or a plausible-but-wrong one.

**Building and Evaluating Advanced RAG** *(conditional)*
Relevant if you build knowledge-augmented analytics agents (e.g., an agent that retrieves documentation or prior analyses alongside querying the semantic layer). Skip if staying purely within the MCP + semantic layer pattern.

**Status**: In progress — MCP course first, then LangGraph sequence
