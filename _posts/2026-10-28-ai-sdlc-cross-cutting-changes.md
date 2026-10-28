---
layout: post
title: "AI SDLC - Cross-cutting Changes"
description: "How the IntDEx framework changes AI SDLC across all phases: flow-based delivery, small domain teams, blocking human checkpoints, independent evidence, verified cost and tiered adoption, with a worked example."
date: 2026-10-28
author: Georgia Kali
slug: ai-sdlc-cross-cutting-changes
permalink: /ai-sdlc-cross-cutting-changes/
tags: ["AI SDLC", "IntDEx", "cross-cutting changes", "flow-based delivery", "human oversight", "evidential independence", "AI-native delivery", "cost control"]
image: /assets/images/2026-10-28-ai-sdlc-cross-cutting-changes.png
lang: en-GB
---

*Georgia Kali · 28 October 2026 · AI SDLC series, IntDEx framework*

![Abstract illustration of seven cross-cutting bands for flow, management, team, oversight, evidence, cost and adoption running horizontally across seven delivery-phase columns, with checkpoint nodes where they intersect]({{ '/assets/images/2026-10-28-ai-sdlc-cross-cutting-changes.png' | relative_url }})

**Why the biggest changes in AI-native delivery sit between the phases, and how the IntDEx framework re-wires flow, teams, oversight, evidence, cost and adoption**

## The problem: changing the phases is not enough

Earlier articles in this series covered single phases of an AI-assisted software development lifecycle (AI SDLC). Some of the most important changes, however, belong to no single phase: how work flows, how teams are sized, who decides, what counts as evidence, who sees the bill and how much of a framework must be adopted.

Organisation shapes output: Conway observed that organisations which design systems "are constrained to produce designs which are copies of the communication structures of these organizations" (Conway, 1968). When an AI delivery engine can generate a feature in an afternoon, fixed sprints, large teams and informal sign-off become the slowest and weakest parts of the system. IntDEx.org (https://intdex.org) describes the central shift as one "from code centric development to behavior centric delivery". The cross-cutting changes make that shift work end to end.

## Seven cross-cutting changes in the IntDEx framework

The IntDEx framework (https://intdex.org) sets out seven changes that apply across every phase:

| Area | Existing practice | IntDEx position |
|---|---|---|
| Flow | Sprints and time-boxed iterations | Flow-based, readiness-triggered replenishment (Kanban-like); monthly delivery planning, quarterly strategy. Sprints optional |
| Management | Separate project and product management | One unified practice: Product Delivery Management |
| Team | Fewer, larger, technology-aligned teams | More, smaller (3–5) teams aligned to business domains and sized by business or regulatory complexity |
| Human oversight | Review, sign-off, RACI | Role-owned blocking checkpoints with a decision record the engine may create but must not sign; unvalidated high-severity checkpoints accumulate as debt that halts the engine |
| Evidence | Traceability matrices, coverage | Traceability and coverage are explicitly not substitutes for correctness evidence |
| Cost | Budget tracking | Per-delivery estimates and actuals visible to the whole team, owned by the Delivery Manager; model self-reported cost is unverified until checked against provider telemetry |
| Adoption | Full framework or nothing | Adopt what you need, above a stated minimum for conformance, with a throughput mode for low-criticality work |

Two of these changes carry most of the weight.

**Evidence.** When one model writes the intent, prompt, code, test and test result, one misunderstanding can run through all of them, and traceability looks complete while the chain is wrong. IntDEx therefore treats a claim of correctness as admissible only if its evidence comes from a source other than the authoring model: executed evidence, human evidence, cross-model evidence or comparison with a prior baseline. This matches research showing that large language models "struggle to self-correct their responses without external feedback" (Huang et al., 2024).

**Oversight.** A checkpoint is only a control if it can block. Human factors research has long documented automation bias and complacency in human use of automated aids (Parasuraman & Manzey, 2010), and the EU AI Act requires human overseers of high-risk systems to "remain aware of the possible tendency of automatically relying or over-relying on the output" (Article 14(4)(b)). IntDEx answers with named owners, recorded decisions and a debt threshold that stops the engine instead of letting unreviewed work pile up.

The NIST AI RMF expects roles, responsibilities and lines of communication for managing AI risk to be "documented and are clear to individuals and teams throughout the organization" (GOVERN 2.1), which is easier in small, domain-aligned teams. ISO/IEC 42001 treats AI governance as a continually improved management system, which suits tiered adoption.

## Research-style validation

**Problem.** Can an organisation adopt AI-native delivery without its planning cadence, team structure, oversight, evidence and cost control becoming bottlenecks or blind spots?

**How IntDEx addresses it.** It changes the operating model, not just the phases: flow, small domain teams, blocking and attributable oversight, independent evidence, verified cost and tiered adoption.

**Worked example (illustrative only).** A hypothetical four-person claims team works in flow: an intent to change a fraud-flag rule is marked ready and pulled the same day, not at the next sprint. The engine reports that "all tests pass" and that the work cost little. The pass is recorded as unverified until the suite actually runs, and the Tester accepts the executed result, not the engine's statement. The cost figure is labelled as a self-report until the Delivery Manager checks it against provider telemetry. When a third unreviewed high-severity checkpoint crosses the threshold set in the engine manifest, the engine stops and reports the blocking condition; named owners clear the queue and work resumes with every decision on record.

**Proposed evaluation criteria (not results).** Teams could measure lead time from intent readiness to release, waiting time at human checkpoints, the share of releases supported by independent (non-self) evidence, the gap between engine-reported and telemetry-measured cost, and how often the checkpoint-debt threshold halts the engine. No results are reported here; quantitative findings will be reported separately.

**Limitations.** These changes have not yet been tested through independent case studies or controlled comparisons. Very small teams struggle with segregation of duties, and blocking checkpoints can slow delivery if owners are unavailable. Flow needs backlog discipline, and cross-model evidence reduces, but does not remove, shared blind spots.

**Conclusion.** In IntDEx, the cross-cutting changes are the operating model that lets the phases work: flow instead of time-boxes, small domain teams, blocking human checkpoints, independent evidence, verified cost and tiered adoption. A practical first step: label every engine self-report as unverified, and give one blocking checkpoint a named owner.

## References

### IntDEx Framework

- IntDEx.org: [https://intdex.org](https://intdex.org)

### Other references

- Conway, M. E. (1968). How Do Committees Invent? *Datamation, 14*(4), 28–31. [https://www.melconway.com/Home/Committees_Paper.html](https://www.melconway.com/Home/Committees_Paper.html)
- Parasuraman, R., & Manzey, D. H. (2010). Complacency and Bias in Human Use of Automation: An Attentional Integration. *Human Factors, 52*(3), 381–410. [https://doi.org/10.1177/0018720810376055](https://doi.org/10.1177/0018720810376055)
- Huang, J., Chen, X., Mishra, S., et al. (2024). Large Language Models Cannot Self-Correct Reasoning Yet. *ICLR 2024*; arXiv:2310.01798. [https://arxiv.org/abs/2310.01798](https://arxiv.org/abs/2310.01798)
- NIST (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* (NIST AI 100-1). [https://doi.org/10.6028/NIST.AI.100-1](https://doi.org/10.6028/NIST.AI.100-1)
- ISO/IEC 42001:2023. *Information technology — Artificial intelligence — Management system*. ISO. [https://www.iso.org/standard/81230.html](https://www.iso.org/standard/81230.html)
- Regulation (EU) 2024/1689 (Artificial Intelligence Act), Article 14: Human oversight. [https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)

AI was used for readability improvements.
