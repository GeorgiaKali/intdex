---
layout: post
title: "AI-Native Development Framework for European Public Organisations (AI SDLC - Intent-Centric)"
description: "Why AI-native delivery makes validated intent, rather than code or user stories, the stable reference for building and judging public digital services, with a worked example."
date: 2026-11-10
author: Georgia Kali
slug: ai-sdlc-intent-centric
permalink: /ai-sdlc-intent-centric/
tags: ["AI SDLC", "IntDEx", "intent-centric", "AI-native delivery", "human oversight", "behaviour validation"]
image: /assets/images/2026-11-10-ai-sdlc-intent-centric.png
lang: en-GB
---

## AI SDLC - Intent-Centric

*Georgia Kali · 10 November 2026 · AI SDLC series, IntDEx framework*

![Abstract illustration of overlapping validated intent documents, the front one approved, feeding a glowing node that splits into prompt cards, a behaviour-check sequence with one rejected run, and a monitoring trace]({{ '/assets/images/2026-11-10-ai-sdlc-intent-centric.png' | relative_url }})

**Why AI-native delivery makes validated intent, rather than code or user stories, the stable reference for building and judging public digital services**

## The problem: the request gets lost in the prompts

In most public organisations, a need travels a long way before it becomes software. A policy owner explains it, an analyst writes user stories, developers interpret those stories, and testers derive cases from their own reading. When an AI engine generates the implementation, the loss gets worse. Requirements end up scattered across chat sessions and one-off prompts, and each regeneration may interpret them slightly differently. Months later, nobody can show which rule the service was meant to follow, which matters when an auditor, an ombudsman or a court asks why a citizen received a particular outcome.

The wider AI-native community is converging on the same diagnosis. GitHub's Spec Kit team describes a move "from 'code is the source of truth' to 'intent is the source of truth'", in which a specification becomes a living, executable artefact and humans verify each phase before moving on (Delimarsky, 2025). Debois (2025) names "implementation to intent" as one of four patterns of AI-native development, and warns that specification-centric work can revive old problems: conflicting stakeholder requirements, and the rigidity of waterfall.

## What "intent-centric" means in IntDEx

IntDEx.org presents IntDEx as "an engineering framework for AI-native delivery/development and management of digital solutions" that is EU-originated and compliance- and sovereignty-aware. The IntDEx framework (https://intdex.org) makes intent "the primary AI drafted, human-validated specification, replacing traditional user stories and requirement documents." Behavioural intent states what the solution should do, how it should behave, which domain rules apply, which constraints must be respected, and which outcomes are acceptable.

Four properties set this apart from a simple specification file:

- **Domain language, not technical syntax.** Intent captures stakeholder expectations, subject-matter expertise and governance requirements in the words the service owners use, much as domain-driven design's ubiquitous language does (Evans, 2003).
- **AI drafts, humans validate.** The engine turns interviews and policy documents into draft intents. A named human approves them, and critical intents (security, legal compliance, data privacy) get stronger review. Where the delivered service is itself a high-risk AI system, this named approval sits alongside the human oversight that Article 14 of the EU AI Act requires (Regulation (EU) 2024/1689).
- **A stable reference point.** Prompts operationalise intent into executable instructions, behavioural artefacts are generated against it, and monitoring measures deviation from it.
- **Versioned evolution.** When domain rules change, intent changes first. The framework ties prompt versioning to intent: a changed intent means a new prompt file linked to the old one, while better execution of the same intent means a new version of the same file.

Requirements engineering has long asked for requirements that are unambiguous, verifiable and traceable (ISO/IEC/IEEE 29148:2018). Intent-centric delivery keeps those qualities and adds two things the classic standard did not need: a non-deterministic engine that reads the requirement directly, and a deviation check that runs continuously, not once.

## Research-style validation

**Problem.** How can a team keep one authoritative statement of what a public service must do when an engine regenerates the implementation many times?

**How IntDEx addresses it.** Intent sits at the top of the artefact hierarchy. Constraints and context frame it, prompts derive from it, and behaviour tests are judged against it. Its minimum adoption criteria require versioned intent, prompt, constraint, context, test prompt and test result artefacts, from which the solution can be rebuilt.

**Worked example (illustrative only).** A hypothetical municipality offers a parking-permit renewal service. Its intent reads:

```text
INTENT-04 v1  Residents' parking-permit renewal
Owner: Business Owner, Mobility Department (approved)
Behaviour: Remind permit holders 30 days before expiry, in the
  language they chose, by their preferred channel.
Rules: Never request documents the municipality already holds.
Constraints: Personal data stays in the municipal tenancy.
Acceptable outcome: Reminder states expiry date, fee and renewal link.
```

The team's evaluation set contains 25 renewal cases, each run several times. Two changes arrive. In the first, the council decides that residents over 75 renew for free. That changes the rules, so the analyst drafts INTENT-04 v2, the Business Owner approves it, a new prompt file is created and linked to the old one, and five new evaluation cases are added. In the second, a developer rewrites the prompt to make the reminder wording clearer. The intent has not changed, so the same prompt file gets a new version and must pass the unchanged cases. One run now asks for proof of residence, which breaks a rule in INTENT-04, so the deviation is caught and the prompt version is rejected. The case counts are illustrative, not measured results.

**Proposed evaluation criteria (not results).** Teams could track the share of prompts and behaviour tests traceable to an approved intent version, the time from a policy change to an approved intent update, the number of deviations from intent caught before release compared with after, and how often reviewers find intents ambiguous.

**Limitations.** Intent is only as good as the people who validate it, and an AI-drafted intent can carry plausible but wrong assumptions into every later artefact. Natural language remains ambiguous, and conflicting stakeholder views do not disappear when written as intent. Over-specification risks the rigidity Debois (2025) warns about. The approach has not yet been tested through independent case studies.

**Conclusion.** For public organisations, intent-centric delivery turns "what was the system supposed to do?" into a question with a versioned, human-approved answer. A practical first step: for one service, write the intents in the department's own language, name an approver for each, and link every prompt to an intent version.

## References

### IntDEx Framework

- IntDEx.org: [https://intdex.org](https://intdex.org)

### Other references

- Delimarsky, D. (2025, 2 September). Spec-driven development with AI: Get started with a new open source toolkit. *The GitHub Blog*. [https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)
- Debois, P. (2025). The 4 Patterns of AI Native Development. *jedi.be*. [https://jedi.be/blog/2025/talk-2025-four-patterns-of-ai-native-development/](https://jedi.be/blog/2025/talk-2025-four-patterns-of-ai-native-development/)
- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley.
- ISO/IEC/IEEE 29148:2018. *Systems and software engineering: Life cycle processes, Requirements engineering*. [https://www.iso.org/standard/72089.html](https://www.iso.org/standard/72089.html)
- Regulation (EU) 2024/1689 (Artificial Intelligence Act), Article 14: Human oversight. [https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)

AI was used for readability improvements.
