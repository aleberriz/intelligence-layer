# intelligence-layer

**AI Analytics Architecture** — a practitioner knowledge base at the intersection of semantic layer design, causal inference, and agentic AI enablement.

---

## What This Is

The data analyst role is shifting. The value-add is moving away from shipping dashboards toward exercising judgment in semantic layer design — building the source-of-truth layer that powers human analysts, embedded tools, and AI agents equally.

This repo is a working knowledge base for that transition. It documents frameworks, patterns, and applied research across three methodological capabilities — and one application domain where they converge in practice.

It is not a course completion log. It is a practitioner's reference built in public.

---

## The Three Pillars

### Semantic Layer Design
Designing a semantic layer is a governance and architecture problem, not a BI tool problem. Done well, it provides consistent metric definitions across every consumer — dashboards, notebooks, AI agents via MCP, and direct SQL. Done poorly, it creates the very inconsistency it was meant to eliminate.

This pillar is organized around the [Open Semantic Interchange (OSI)](https://open-semantic-interchange.org/) standard — a vendor-agnostic spec for semantic model exchange backed by Omni, dbt Labs, Snowflake, Databricks, and 40+ other organizations. Omni and dbt/MetricFlow are the current implementation tools, chosen because both are active OSI members. The frameworks here are designed to be portable.

### Causal Inference
Most analytics questions are causal, but most analytics methods are only descriptive. Knowing the difference — and knowing when you can answer a causal question rigorously vs. when you cannot — is a high-leverage skill that separates senior practitioners from report builders.

This pillar covers A/B testing methodology, experimental design, and observational causal methods (difference-in-differences, regression discontinuity, synthetic controls) for when experiments aren't feasible.

### Agentic AI Enablement
The semantic layer is becoming an API for AI agents. Understanding the Model Context Protocol, how to design Omni models for AI consumption, and how to build and evaluate AI skills that operate against a semantic layer is the forward edge of this field.

This pillar covers MCP server architecture, AI skill design patterns, and prompt engineering for analytics contexts.

---

## Repository Structure

### Capabilities
```
intelligence-layer/
├── semantic-layer/          # Omni modeling, dbt Semantic Layer, design frameworks
│   ├── omni/                # Omni YAML patterns, topic design, AI optimization
│   ├── dbt/                 # MetricFlow, semantic layer integration
│   └── frameworks/          # General design principles and decision frameworks
├── causal-inference/        # Experimental design and observational causal methods
│   ├── experimentation/     # A/B testing (RCTs) — a subset of causal inference
│   └── notebooks/           # Applied notebooks on public datasets
└── ai-enablement/           # MCP, AI skills, prompt patterns
    ├── mcp/                 # MCP server patterns and integration notes
    ├── skills/              # AI skill design (Omni-style and general)
    └── prompts/             # Curated, tested prompt templates
```

### Application Domain
```
├── growth-analytics/        # Where the three capabilities converge in practice
│   └── frameworks/          # PLG metrics, retention, user behavior → revenue
```

### Reference
```
└── resources/               # Annotated reading list and reference material
```

---

## Conventions

- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) — `docs:`, `feat:`, `chore:`, `research:`, `fix:`
- **Branches**: topic-scoped — `docs/semantic-layer-fundamentals`, `feat/power-calculator`, `research/mcp-protocol`
- **Python**: [Poetry](https://python-poetry.org/) for dependency management
- **Notebooks**: Jupyter, always on public or synthetic datasets — no proprietary data

---

## About

Built by [Alejandro Berrizbeitia](https://github.com/aleberriz) — Senior Data Analyst at [Kit](https://kit.com), active in the [OSI](https://open-semantic-interchange.org/) and [omni-claude-skills](https://github.com/exploreomni/omni-claude-skills) communities.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
