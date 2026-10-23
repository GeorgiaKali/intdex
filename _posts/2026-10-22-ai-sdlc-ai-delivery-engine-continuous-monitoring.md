---
layout: post
title: "AI SDLC - AI Delivery Engine Continuous Monitoring"
description: "How the IntDEx framework treats AI SDLC monitoring as governed delivery work: drift and constraint degradation against accepted baselines, independent telemetry and blocking human checkpoints, with a worked example."
date: 2026-10-22
author: Georgia Kali
slug: ai-sdlc-ai-delivery-engine-continuous-monitoring
permalink: /ai-sdlc-ai-delivery-engine-continuous-monitoring/
tags: ["AI SDLC", "IntDEx", "continuous monitoring", "drift detection", "observability", "AI-native delivery", "LLM drift", "human oversight"]
image: /assets/images/2026-10-22-ai-sdlc-ai-delivery-engine-continuous-monitoring.png
lang: en-GB
---

*Georgia Kali · 22 October 2026 · AI SDLC series, IntDEx framework*

![Abstract illustration of monitored signals drifting out of an accepted baseline band after a model change, raising an alert at a human checkpoint that loops back into a new delivery cycle]({{ '/assets/images/2026-10-22-ai-sdlc-ai-delivery-engine-continuous-monitoring.png' | relative_url }})

**Why a validated release says little about next month's behaviour, and how the IntDEx framework makes monitoring a governed input to delivery**

## The problem: behaviour keeps moving after release

Conventionally, monitoring is an operations concern: dashboards watch latency, traffic, errors and saturation, the "four golden signals" of Google's SRE book (Ewaschuk, 2016). In an AI-assisted software development lifecycle (AI SDLC), behaviour can degrade with no code change at all. [IntDEx.org](https://intdex.org) defines AI-native delivery as the flow through which digital solutions are "conceived, engineered, validated, released, monitored, and evolved" with AI as the primary tooling, so monitoring is part of delivery.

Public evidence shows why. Chen, Zaharia and Zou (2023) found that GPT-4 followed 99.5% of their answer-extraction instructions in March 2023 but only 0.5% in June, concluding that the "same" LLM service can change substantially in a short time, "highlighting the need for continuous monitoring of LLMs". Machine-learning research has long studied concept drift (Gama et al., 2014), and Google's ML Test Score stresses knowing that a system "continues to work correctly over time", not just at launch (Breck et al., 2017). The SRE book counts a successful response "coupled with the wrong content" as an error; generative systems produce exactly that failure.

## What IntDEx changes in Phase 6: AI Delivery Engine Continuous Monitoring

Phase 6 tracks AI delivery engine behaviour in production, "identifying drift, degradation, and emerging risks". Building on observability, MLOps drift monitoring and site reliability engineering, [the IntDEx framework](https://intdex.org) makes five changes:

1. **Monitoring covers more than correctness.** Signals include drift, hallucinations, data quality, real-world usage and AI safety, extending to cost, sovereignty and ethics drift.
2. **Constraint degradation is tracked.** Safeguards can weaken gradually without any single visible failure, so their erosion is a signal in its own right.
3. **Engine and solution telemetry are kept apart.** Delivery-engine observability (lead time, queue time at human checkpoints, first-pass validation rate, rework, evidence completeness, cost per accepted change) is distinct from delivered-solution telemetry, and every metric names its authoritative data source so model-generated estimates are not confused with measured telemetry.
4. **Accepted deliverables become a regression baseline.** When a model or engine version changes, instructions with known, previously accepted deliverables are re-run and compared with the accepted results.
5. **Monitoring is an input to delivery.** A signal can open a new delivery cycle in any phase, and breaching a cost or risk threshold defined in the engine manifest is a mandatory, blocking human checkpoint.

The engine detects and raises signals; humans triage alerts, decide what is a real deviation and own the thresholds. Detection should be a deterministic script over a metric with a stable rolling baseline, with no model in the decision. At high severity the engine alerts the named owner but takes no action; at medium severity its diagnosis is recorded as UNVERIFIED, a hypothesis rather than a root cause.

This aligns with public frameworks: the NIST AI RMF asks that AI system behaviour is "monitored when in production" (MEASURE 2.4) under a post-deployment monitoring plan (MANAGE 4.1); Article 72 of the EU AI Act requires providers of high-risk AI systems to collect and analyse performance data "actively and systematically" throughout their lifetime; and ISO/IEC 42001 frames AI management as continual improvement.

## Research-style validation

**Problem.** Can a team detect, and govern its response to, behavioural change in an AI delivery engine when no code has changed?

**How IntDEx addresses it.** It widens what is monitored, ties every metric to an authoritative source, makes threshold breaches blocking human checkpoints and routes findings back into delivery. Under its evidential-independence rule, the engine's own report that it is healthy or within budget stays unverified until checked against independent telemetry.

**Worked example (illustrative only).** Imagine a hypothetical model upgrade behind an engine drafting customer-facing release notes. A monitoring record could read:

| Signal | Source | Evidence class | Response |
|---|---|---|---|
| Re-run of accepted reference tasks: some outputs omit a mandatory disclaimer | Deterministic comparison with accepted baseline | Admissible (prior-artefact) | Constraint degradation; new delivery cycle |
| Engine reports "token cost stable" | Engine summary only | UNVERIFIED | Checked against billing telemetry |
| Daily cost exceeds the manifest threshold | Provider billing telemetry | Admissible (executed) | Blocking checkpoint; Delivery Manager decides |
| Engine suggests "new model ignores the system prompt" | Engine diagnosis | UNVERIFIED (hypothesis) | Tester confirms before any prompt change |

**Proposed evaluation criteria (not results).** Teams could track the time from a model change to a completed baseline re-run, the share of metrics with a named authoritative source, the share of threshold breaches resolved by a recorded human decision before work continued, and alert precision (alerts triaged as real deviations), reflecting the SRE rule that every page should be actionable. No results are reported here.

**Limitations.** The IntDEx framework has not yet been evaluated through independent case studies or controlled comparisons with other approaches. Reference baselines cover only known deliverables, so novel usage can drift unseen. Alert thresholds need careful tuning to balance false positives and negatives (Breck et al., 2017). Deterministic metrics capture semantic quality only partly, so some signals still need human or cross-model review. Enabling telemetry traceable to a named individual is itself a mandatory checkpoint.

**Conclusion.** In IntDEx, continuous monitoring is evidence-producing delivery work, not a dashboard: signals come from independent sources, humans own thresholds and judgements, and findings flow back into intent, prompts, constraints or model choice. The practical first step: keep a few accepted reference tasks and re-run them whenever the model changes.

## References

### IntDEx Framework

- IntDEx.org: [https://intdex.org](https://intdex.org)

### Other references

- Ewaschuk, R. (2016). Monitoring Distributed Systems. In B. Beyer, C. Jones, J. Petoff & N. R. Murphy (Eds.), *Site Reliability Engineering: How Google Runs Production Systems*. O'Reilly. [https://sre.google/sre-book/monitoring-distributed-systems/](https://sre.google/sre-book/monitoring-distributed-systems/)
- Chen, L., Zaharia, M., & Zou, J. (2023). How Is ChatGPT's Behavior Changing over Time? *arXiv:2307.09009*. [https://arxiv.org/abs/2307.09009](https://arxiv.org/abs/2307.09009)
- Gama, J., Žliobaitė, I., Bifet, A., et al. (2014). A Survey on Concept Drift Adaptation. *ACM Computing Surveys, 46*(4), Article 44. [https://doi.org/10.1145/2523813](https://doi.org/10.1145/2523813)
- Breck, E., Cai, S., Nielsen, E., et al. (2017). The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction. *2017 IEEE International Conference on Big Data*. [https://doi.org/10.1109/BigData.2017.8258038](https://doi.org/10.1109/BigData.2017.8258038)
- NIST (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* (NIST AI 100-1). [https://doi.org/10.6028/NIST.AI.100-1](https://doi.org/10.6028/NIST.AI.100-1)
- Regulation (EU) 2024/1689 (Artificial Intelligence Act), Article 72: Post-market monitoring by providers and post-market monitoring plan for high-risk AI systems. [https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)
- ISO/IEC 42001:2023. *Information technology — Artificial intelligence — Management system*. ISO. [https://www.iso.org/standard/81230.html](https://www.iso.org/standard/81230.html)

AI was used for readability improvements.
