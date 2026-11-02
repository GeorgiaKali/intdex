---
layout: post
title: "AI SDLC - Emergent"
description: "Why AI-native delivery keeps producing behaviour nobody specified, and how the IntDEx framework treats emergence as a managed source of insight, with a worked example."
date: 2026-11-01
author: Georgia Kali
slug: ai-sdlc-emergent
permalink: /ai-sdlc-emergent/
tags: ["AI SDLC", "IntDEx", "emergent behaviour", "non-determinism", "LLM", "behaviour validation", "AI-native delivery"]
image: /assets/images/2026-11-01-ai-sdlc-emergent.png
lang: en-GB
---

*Georgia Kali · 1 November 2026 · AI SDLC series, IntDEx framework*

![Abstract illustration of six coloured input nodes for prompts, models, constraints, data, context and oversight feeding converging streams into a central glowing cluster from which new unplanned shapes branch outward]({{ '/assets/images/2026-11-01-ai-sdlc-emergent.png' | relative_url }})

**Why AI-native delivery keeps surprising the teams that run it, and how the IntDEx framework turns emergence from an anomaly into a managed source of insight**

## The problem: behaviour nobody specified

Traditional development rests on a quiet assumption: the code does what it says. When a feature surprises a team, the surprise usually lives at the level of the whole system, the organisation or the requirement set, not inside each line of work. The Agile Manifesto already accepted that "the best architectures, requirements, and designs emerge from self-organizing teams" (Beck et al., 2001), but the building blocks themselves stayed deterministic.

AI-assisted development changes where emergence happens. Large language models produce different outputs for the same request: an empirical study of ChatGPT code generation found that identical prompts often returned code with different behaviour, and that setting the temperature to zero reduced this variation but did not remove it (Ouyang et al., 2025). Research on model scaling has described "emergent abilities" that appear in larger models but not in smaller ones (Wei et al., 2022), although later work argued that some of these jumps are partly an effect of the chosen metric (Schaeffer, Miranda & Koyejo, 2023). Either way, a team cannot read the full behaviour of its delivery engine from a design document.

## What "emergent" means in IntDEx

The IntDEx framework (https://intdex.org) defines the property precisely: the AI delivery engine "can exhibit emergent behaviour that arises from the interaction of prompts, models, constraints, data, context, and human oversight." That behaviour "cannot be fully pre-determined", and it "reshapes expectations, architectural choices, validation strategies, and risk posture." The framework also separates two levels: emergence in the delivery engine, and emergent user-facing behaviour in the solution it produces, which is evaluated separately as the product delivered to users.

IntDEx claims no discovery here. Complex adaptive systems theory (Holland, 1995), the Cynefin framework, where the complex domain calls for probing before sensing and responding (Snowden & Boone, 2007), and emergent design in agile practice all describe the same phenomenon. What differs is the scale, the speed and the location: in AI-native delivery, emergence appears in every step of work that uses non-deterministic methods.

| Aspect | Traditional development | IntDEx position |
|---|---|---|
| Where emergence appears | System, organisation or requirement set | Every non-deterministic step, plus the delivered solution |
| How it is treated | A defect or a late surprise | A defining property and a source of insight |
| Response | Fix the code | Refine intent, prompts, constraints, routing or oversight |

In practice, emergence touches every engineering concern. Behavioural intent evolves as stakeholders refine their understanding. Engine components such as retrieval pipelines, safeguards and model routing adapt to new behavioural patterns. Prompts mature through refinement and versioning. Validation exposes new constraints and edge cases. Risk posture shifts as the engine meets new contexts. Human oversight catches behaviours that automated checks cannot see. This matches the NIST AI RMF, which expects organisations to keep identifying and tracking unanticipated and emergent AI risks throughout the lifecycle (NIST, 2023).

## Research-style validation

**Problem.** How can a team deliver safely with an engine whose behaviour cannot be fully known in advance, without either ignoring surprises or freezing delivery every time one appears?

**How IntDEx addresses it.** It treats emergence as a defining property. Emergent behaviour is observed, recorded and classified, then routed into a concrete response: a refined intent, a new constraint, a prompt version, a routing change or a human checkpoint. Engine-level and solution-level emergence are assessed separately.

**Worked example (illustrative only).** A hypothetical team builds a refund-summary feature. During behaviour validation the Tester runs the same intent 20 times and notices that, in some runs, the engine adds a currency conversion it inferred from retrieved context. Nobody asked for it. The Tester logs it as emergent behaviour, and the Analyst and Business Owner decide whether it is wanted. They reject it, so the Architect adds a constraint and the run set is repeated. Simple probability shows why sampling matters. If an unwanted behaviour occurs in 5% of runs, the chance of never seeing it in 20 independent runs is 0.95 to the power of 20, about 36%. Seeing it at least once with 95% confidence needs about 59 runs, because 0.95 to the power of 59 is just under 0.05. This is arithmetic for illustration, not a measured result.

**Proposed evaluation criteria (not results).** Teams could track the number of emergent behaviours logged per feature, the share classified as wanted, unwanted or neutral, the time from detection to a validated response, how many were found by humans rather than automated checks, and how many reached users before detection. No results are reported here; quantitative findings will be reported separately.

**Limitations.** Treating emergence as a managed property has not yet been tested through independent case studies. Classifying a behaviour as emergent rather than as a plain defect is a judgement call, and teams may disagree. Repeated sampling costs time and tokens, and rare behaviours can still escape any sample size a team can afford.

**Conclusion.** In IntDEx, emergence is not an excuse and not a bug category. It is the expected result of combining prompts, models, data, context and oversight, and it guides engineering decisions across the whole delivery effort. A practical first step: keep a visible log of unexpected behaviours and give each one a named owner and a decision.

## References

### IntDEx Framework

- IntDEx.org: [https://intdex.org](https://intdex.org)

### Other references

- Beck, K., et al. (2001). *Principles behind the Agile Manifesto*. [https://agilemanifesto.org/principles.html](https://agilemanifesto.org/principles.html)
- Holland, J. H. (1995). *Hidden Order: How Adaptation Builds Complexity*. Addison-Wesley.
- Snowden, D. J., & Boone, M. E. (2007). A Leader's Framework for Decision Making. *Harvard Business Review, 85*(11), 68–76. [https://hbr.org/2007/11/a-leaders-framework-for-decision-making](https://hbr.org/2007/11/a-leaders-framework-for-decision-making)
- Wei, J., et al. (2022). Emergent Abilities of Large Language Models. *Transactions on Machine Learning Research*. [https://arxiv.org/abs/2206.07682](https://arxiv.org/abs/2206.07682)
- Schaeffer, R., Miranda, B., & Koyejo, S. (2023). Are Emergent Abilities of Large Language Models a Mirage? *NeurIPS 2023*. [https://arxiv.org/abs/2304.15004](https://arxiv.org/abs/2304.15004)
- Ouyang, S., Zhang, J. M., Harman, M., & Wang, M. (2025). An Empirical Study of the Non-determinism of ChatGPT in Code Generation. *ACM Transactions on Software Engineering and Methodology*. [https://arxiv.org/abs/2308.02828](https://arxiv.org/abs/2308.02828)
- NIST (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* (NIST AI 100-1). [https://doi.org/10.6028/NIST.AI.100-1](https://doi.org/10.6028/NIST.AI.100-1)

AI was used for readability improvements.
