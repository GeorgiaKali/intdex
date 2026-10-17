---
layout: post
title: "AI SDLC - Behaviour Validation"
description: "How the IntDEx framework turns AI SDLC testing into evidence-ranked behaviour validation: why self-reported passes are UNVERIFIED, with a worked example."
date: 2026-10-17
author: Georgia Kali
slug: ai-sdlc-behaviour-validation
permalink: /ai-sdlc-behaviour-validation/
tags: ["AI SDLC", "IntDEx", "behaviour validation", "evidential independence", "AI-native delivery", "software testing", "LLM evaluation", "human oversight"]
image: /assets/images/2026-10-17-ai-sdlc-behaviour-validation.png
lang: en-GB
---

*Georgia Kali · 17 October 2026 · AI SDLC series, IntDEx framework*

![Abstract illustration of artefacts passing through four evidence gates to a validated behaviour]({{ '/assets/images/2026-10-17-ai-sdlc-behaviour-validation.png' | relative_url }})

**Why a self-reported "all tests pass" is not evidence, and how the IntDEx framework turns testing into evidence-ranked behaviour validation**

## The problem: when one model writes the code and the verdict

In an AI-assisted software development lifecycle (AI SDLC), the same model can now draft the intent, the prompt, the implementation, the tests and the final test report. The IntDEx framework v5 names the risk directly: a misunderstanding can be reproduced consistently through every one of those artefacts, so "traceability then appears complete, coverage full, and validation appears good, while the entire chain is wrong". Traceability between artefacts written by one author may be internal consistency, not verification.

This is not only a theoretical worry. NIST's Generative AI Profile (NIST AI 600-1) describes confabulation as confidently stated but erroneous or false content, and research presented at ICLR 2024 found that large language models struggle to correct their own reasoning without external feedback, with performance sometimes degrading after self-correction (Huang et al., 2024). A test phase that accepts the authoring model's own verdict inherits both weaknesses.

## What IntDEx changes in Phase 4: Behaviour Validation

IntDEx (AI-native Delivery Experience) defines a seven-phase AI-native delivery flow. Phase 4, Behaviour Validation, "ensures that delivery engine's outputs are correct, safe, ethical, and aligned with stakeholder expectations", and user testing focuses on behaviour rather than code. Testers evaluate outputs for correctness, bias, hallucinations, constraint violations and drift.

Compared with conventional QA, UAT, test automation and evals, the framework makes four concrete changes:

1. **Evidential independence.** A claim of correctness is admissible only if its evidence comes from a source other than the model that produced the work. Sources are ranked: executed evidence (exit codes, test results, build logs, HTTP responses, database state) above human evidence, above cross-model evidence, above prior-artefact comparison.
2. **Self-reports are UNVERIFIED.** A statement by the authoring model that a check passed "carries no evidential weight and must be recorded as unverified rather than as a pass". The engine's own report is not evidence; the human decides.
3. **Pair behaviour validation.** Acceptance validation is done in pairs, for example end user with tester, or user with analyst; security, UI/UX and compliance tests are automated before release and checked by human testers.
4. **Continuous validation.** Automated Continuous Behaviour Validation (ACBV) re-runs behavioural evaluations whenever the engine configuration changes, whether a prompt, constraint, context or model swap, and gates the change on pass rates, so behavioural quality cannot degrade silently.

## Research-style validation

**Problem.** Can behaviour validation in an AI SDLC produce assurance when the authoring model also writes the tests and the report?

**Method.** IntDEx was developed using Design Science Research, treating the framework as an artefact refined through practical application on a data-science platform for public-health data experimentation. Evaluation covered rebuilding the solution from artefacts alone and the operation of the evidential-independence and human-oversight controls.

**How validation was applied.** The v5 document describes applying these controls during the delivery of that platform and in an attempt to rebuild it from IntDEx artefacts alone. Enforced human checkpoints were used to halt work where the engine's own evidence was judged insufficient and to correct the severity the engine had assigned to a change. A model from a different provider family reviewed prompt executions, and its disagreements were passed to a human, who decided whether a change was needed. The rebuild was assessed across behaviour, security, data structures, architecture and configuration, and the authors note that security controls left implicit in the original, rather than written as governed intent or security artefacts, may not be reliably reproduced. Quantitative results will be reported in a forthcoming paper.

**Worked example.** Take the playbook's sample request: a website contact form that emails the business owner. Because it handles personal data, IntDEx treats it as a Tier 2 (elevated) change with a synchronous, blocking checkpoint. A validation record could look like this:

| Acceptance criterion | Evidence | Rank | Status |
|---|---|---|---|
| Valid enquiry is accepted and the owner is notified | Integration test exit code and captured outbound message | Executed | Admissible |
| Abusive repeated submissions are throttled | Engine states "rate limiting implemented" | Self-report | UNVERIFIED |
| Same criterion, after a negative test that floods the endpoint | HTTP 429 responses logged | Executed | Admissible |
| Form wording meets the intent | Recorded user and tester pair review | Human | Admissible |

**Proposed evaluation criteria (not results).** Teams adopting this practice could track measures from the framework's own list: the percentage of production claims backed by independent evidence, behavioural regression, first-pass acceptance, escaped defects, and the negative-control-test pass rate. Because evaluations of a non-deterministic system vary between runs, IntDEx advises establishing the expected run-to-run variation and gating only on changes that exceed it.

**Limitations.** The authors state that the application so far covers a single project with a single principal evaluator. They present it as preliminary evidence of feasibility rather than general proof, and independent multi-case replication is still needed. Cross-model review is advisory, and in the authors' brief a second model helped but also raised false alarms. Human reviewers are a failure mode too. IntDEx names automation bias, a risk the EU AI Act's Article 14 also requires high-risk systems to address, and it treats a checkpoint rejection rate of zero as a finding that needs investigation, not as a sign of quality.

**Conclusion.** In IntDEx, behaviour validation is not "run the tests and trust the summary". It is an evidence ledger in which every claim names its source, self-assessment is labelled UNVERIFIED, and a named human accepts or rejects the evidence. For teams moving to an AI SDLC, that is a practical first step: rank the evidence before you trust the result.

## References

### IntDEx Framework

- IntDEx.org, framework home and news: [https://intdex.org/](https://intdex.org/)
- AI-native Delivery Experience Framework - IntDEx (framework page, free registration): [https://intdex.org/page/ai-native-delivery-experience-framework-intdex-v4-md-19](https://intdex.org/page/ai-native-delivery-experience-framework-intdex-v4-md-19)
- IntDEx: EU-originated, compliance- and sovereignty-aware framework (overview): [https://intdex.org/page/ai-native-delivery-experience-intdex-framework-eu-originated-compliance-and-sovereignty-aware-invitation-9](https://intdex.org/page/ai-native-delivery-experience-intdex-framework-eu-originated-compliance-and-sovereignty-aware-invitation-9)
- IntDEx Intent template: [https://intdex.org/page/intent-template-18](https://intdex.org/page/intent-template-18)
- IntDEx DESSERT 2026 brief, "Evidential Independence and Enforceable Human Oversight": [https://intdex.org/IntDEx_AI_native_delivery_experience_desssert_2026_brief.pdf](https://intdex.org/IntDEx_AI_native_delivery_experience_desssert_2026_brief.pdf)

### Other references

- Ktenas, S., & Gasparinatou, M. M. (2026). *AI-Native Delivery Experience (IntDEx): An engineering framework for AI-native development and management of digital solutions*, v5, October 2026. Ionian University / IntDEx.org.
- Ktenas, S. (2026). *AI-native Delivery Experience - IntDEx* (preprint, v1). Figshare. [https://doi.org/10.6084/m9.figshare.33438421](https://doi.org/10.6084/m9.figshare.33438421)
- Ktenas, S. (2026). *IntDEx - Implementation Example / Playbook* (preprint). Figshare. [https://figshare.com/articles/preprint/34005348](https://figshare.com/articles/preprint/AI_Native_Delivery_Experience_Framework_-_IntDEx_-_Implementation_Example_-_Playbook_-_Preprint/34005348)
- NIST (2024). *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile* (NIST AI 600-1). [https://doi.org/10.6028/NIST.AI.600-1](https://doi.org/10.6028/NIST.AI.600-1)
- Huang, J., Chen, X., Mishra, S., Zheng, H. S., Yu, A. W., Song, X., & Zhou, D. (2024). Large Language Models Cannot Self-Correct Reasoning Yet. *ICLR 2024*. [https://arxiv.org/abs/2310.01798](https://arxiv.org/abs/2310.01798)
- Regulation (EU) 2024/1689 (Artificial Intelligence Act), Article 14: Human oversight. [https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)

AI was used for readability improvements.
