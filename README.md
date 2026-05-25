# intelligence-layer

**Forecasting, Causal Inference & AI-Assisted Analytics** — a practitioner knowledge base for building and evaluating decision systems.

---

## What This Is

This repo documents frameworks, methods, and applied research across three areas of decision science. It is not a course log. It is a working reference built in public.

---

## The Three Pillars

### Forecasting
Covers the full methodology stack: statistical approaches (ARIMA family, ETS, Holt-Winters), machine learning and global models (gradient boosting with lag features, deep learning), and foundation models (zero-shot approaches such as Chronos). Includes backtesting design, accuracy metrics, prediction intervals, and decision thresholds.

### Causal Inference
Most analytics questions are causal, but most analytics methods are only descriptive. This pillar covers experimental design (A/B testing, RCTs), observational methods (difference-in-differences, regression discontinuity, synthetic controls), causal graphs and assumptions, and uplift/incrementality modeling.

### AI-Assisted Analytics Evaluation
Not building AI chatbots — evaluating whether AI-generated analysis is correct, useful, and decision-ready. Covers eval dataset design, answer rubrics, failure taxonomy (hallucination, wrong metric, overclaim), and observability basics.

---

## Repository Structure

### Core
```
intelligence-layer/
├── forecasting/
│   ├── statistical/         # ARIMA, SARIMA, SARIMAX, ETS, Holt-Winters, Prophet
│   ├── machine-learning/    # XGBoost/LightGBM with lag features, global models, deep learning
│   ├── foundation-models/   # Chronos, TimesFM, Moirai — zero-shot approaches
│   └── evaluation/          # Backtesting, accuracy metrics, prediction intervals
├── causal-inference/
│   ├── experimentation/     # A/B testing, RCTs
│   ├── observational/       # DiD, regression discontinuity, synthetic controls
│   ├── causal-graphs/       # DAGs, assumptions, do-calculus basics
│   └── uplift/              # Uplift modeling, incrementality
└── ai-evaluation/
    ├── eval-design/         # Benchmark questions, dataset construction
    ├── rubrics/             # Answer grading, correctness criteria
    ├── failure-taxonomy/    # Hallucination, wrong metric, overclaim
    └── observability/       # Traces, guardrails basics
```

### Supporting
```
├── semantic-layer/          # Infrastructure literacy — metric governance, OSI, Omni
│   ├── frameworks/
│   └── omni/
└── growth-analytics/        # Application domain — PLG metrics, retention, revenue
    └── frameworks/
```

### Reference
```
└── resources/               # Annotated reading list and reference material
```

---

## Conventions

- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) — `docs:`, `feat:`, `chore:`, `research:`, `fix:`
- **Branches**: topic-scoped — `docs/forecasting-evaluation`, `feat/causal-dag-framework`, `research/chronos-backtesting`
- **Python**: [Poetry](https://python-poetry.org/) for dependency management

---

## About

Built by [Alejandro Berrizbeitia](https://github.com/aleberriz) — Data Scientist, Time Series & Forecasting Professor at [IE University](https://www.ie.edu), Senior Data Analyst at [Kit](https://kit.com).

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
