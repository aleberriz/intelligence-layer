# Growth Analytics

This is an **application domain**, not a methodology. It's where the three capabilities in this repo converge on a specific business context: understanding how user behavior drives revenue on a creator platform.

- The **semantic layer** gets designed to answer growth questions — activation, retention, expansion MRR
- **Causal inference** gets applied to growth problems — did this feature drive upgrades? what caused the retention drop? A/B testing is the primary tool when feasible; observational methods when it isn't
- **AI enablement** makes growth data self-serve — agents querying creator behavior metrics via MCP

The analytics challenge for a creator platform like Kit is tracing the path from content engagement signals to email list growth to paid conversion and expansion. The frameworks here are the mental models for that specific problem space.

---

## Subdirectories

### `frameworks/`
Structured mental models for growth measurement:
- Acquisition → Activation → Retention → Revenue → Referral (AARRR applied to SaaS/creator)
- Cohort analysis and retention curves — how to read them, what good looks like
- Monetization modeling — ARPU, LTV, payback period, expansion MRR
- Behavioral signals as leading indicators of upgrade and churn
- The difference between activity metrics (vanity) and outcome metrics (actionable)

---

## Key Analytical Questions This Pillar Addresses

1. Which acquisition channels produce the highest-LTV creators?
2. What activation milestones predict long-term retention?
3. What behavioral signals in the free tier predict paid conversion?
4. How does email list growth rate correlate with monetization events?
5. Which expansion triggers (feature usage, list size thresholds) drive upgrade decisions?

---

## Reference Frameworks

- AARRR (Dave McClure) — useful skeleton, needs SaaS-specific adaptation
- Product-Led Growth (Wes Bush) — acquisition and expansion mechanics for PLG products
- *Hacking Growth* (Ellis & Brown) — cross-functional experimentation approach
- Amplitude's North Star Playbook — connecting input metrics to the north star metric
