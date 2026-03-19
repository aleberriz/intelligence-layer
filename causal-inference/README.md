# Causal Inference

Methods for answering causal questions rigorously — when experiments are feasible and when they are not.

Most analytics questions are causal ("did this change improve retention?") but most analytics methods are only descriptive ("retention went up after this change"). Knowing which tools apply to which situations, and being honest about the limits of each, is the skill.

---

## Subdirectories

### `experimentation/`
A/B test design and analysis — minimum detectable effect sizing, power calculations, sequential testing vs. fixed-horizon, guardrail metrics vs. OEC (Overall Evaluation Criterion), and common failure modes (peeking, novelty effects, network spillover).

Preferred platform: [GrowthBook](https://www.growthbook.io/) (open source) for RCT management and feature flagging. GrowthBook docs are a primary learning resource alongside the academic references below.

Core reference: *Trustworthy Online Controlled Experiments* — Kohavi, Tang & Xu (the industry standard, written by practitioners from Microsoft, Google, and Airbnb)

### `notebooks/`
Applied notebooks on public or synthetic datasets. Each notebook states the causal question, the method chosen, the assumptions required, and the limitations of the answer. No proprietary data.

---

## Methods Covered (in progress)

| Method | When to use |
|---|---|
| A/B test (fixed-horizon) | Randomizable treatment, predetermined sample size |
| Sequential / always-valid testing | Need to monitor during experiment |
| Difference-in-differences | Pre/post with control group, parallel trends |
| Regression discontinuity | Treatment assigned at a cutoff |
| Synthetic control | Few treated units, long pre-period |

---

## Core Reference

- **Kohavi, Tang & Xu** — *Trustworthy Online Controlled Experiments* (Cambridge University Press)
- **Huntington-Klein** — *The Effect* ([free at theeffectbook.net](https://theeffectbook.net)) — accessible intro to causal inference with modern methods
