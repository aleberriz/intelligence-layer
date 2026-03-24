# AGENTS.md

Context file for AI agents working in this repository.
Supported by Cursor, OpenAI Codex, GitHub Copilot, Google Jules, Aider, Zed, JetBrains Junie, and others.

---

## Who Owns This Repo

**Alejandro Berrizbeitia** — Senior Data Analyst at Kit (formerly ConvertKit).
GitHub: [@aleberriz](https://github.com/aleberriz)
Positioning: AI Analytics Architect — the intersection of semantic layer design, causal inference, and agentic AI enablement.

Alejandro is active in the [OSI](https://open-semantic-interchange.org/) and [omni-claude-skills](https://github.com/exploreomni/omni-claude-skills) communities.

---

## What This Repo Is

A practitioner knowledge base — not a course log, not a tutorial collection. It documents working frameworks, applied research, and reusable patterns across three domains:

1. **Semantic Layer Design** — OSI-aligned, vendor-agnostic frameworks; Omni and dbt/MetricFlow as current implementation tools
2. **Causal Inference** — A/B testing, experimental design, observational methods
3. **Agentic AI Enablement** — MCP server patterns, AI skill design, prompt engineering for analytics

The thesis: the data analyst role is shifting from dashboard delivery toward semantic layer governance and AI agent orchestration. This repo is the practitioner evidence base for that positioning.

---

## Repository Map

```
semantic-layer/
  omni/           Omni YAML patterns, topic design, AI optimization hints
  dbt/            MetricFlow metrics, semantic layer integration with Omni
  frameworks/     General design principles, trade-off frameworks

causal-inference/
  experimentation/  A/B test design, power calculators, sequential testing
  notebooks/        Applied causal inference on public datasets

ai-enablement/
  mcp/            MCP server architecture, auth patterns, client comparisons
  skills/         AI skill design (Omni-style and general)
  prompts/        Curated, tested prompt templates for analytics contexts

growth-analytics/
  frameworks/     PLG metrics, cohort models, user behavior → revenue frameworks

resources/
  reading-list.md   Annotated bibliography with commentary
```

---

## Conventions

### Git
- **Branch model**: one branch per topic — `docs/`, `feat/`, `chore/`, `research/`, `fix/`
- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) — always `type: description` format; single subject line by default. Add a body only when the *why* is genuinely non-obvious and not covered by the PR description — a workaround, a constraint someone might accidentally undo, a decision with real trade-offs. Not for restating what the diff already shows.
- **Authorship**: All commits are authored by Alejandro (`git config user.name`). AI agents draft content; the human authors and commits. Never commit as the AI agent.
- **PRs**: opened even for solo work — PR description carries the rationale, not just the diff. This is where the *why* lives; commit messages are index entries.

### Python
- **Dependency manager**: [Poetry](https://python-poetry.org/) — `pyproject.toml` + committed `poetry.lock`
- **Platform**: Linux (Ubuntu or Fedora)
- **Visualization**: [Plotly](https://plotly.com/python/) for interactive charts; [plotnine (ggplot)](https://plotnine.readthedocs.io/) for static/publication-style plots
- **Notebooks**: Jupyter — always on public or synthetic datasets

### Content
- **No Kit-proprietary content** — no internal SQL, no metric definitions from Kit's actual data model, no business logic from Kit systems. The line is clear: general frameworks and public-dataset examples only.
- Stub READMEs in each folder describe purpose and expected content — keep them current as the folder grows
- Prefer markdown for frameworks and notes; Jupyter notebooks for anything computational

---

## Working in This Repo

When drafting content, default to:
- Concise, practitioner-grade writing — not academic, not tutorial-style
- Concrete examples over abstract principles where possible
- Linking to primary sources (Omni docs, dbt docs, MCP spec, Kohavi, etc.) rather than paraphrasing them

When suggesting commits or PR descriptions, draft them for Alejandro to review and rewrite. Do not auto-commit.
