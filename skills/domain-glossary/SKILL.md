---
name: domain-glossary
description: 领域名词表/业务概念梳理：从代码与文档提炼业务名词、核心对象/状态、核心场景（概念层，不写 API/表结构），输出 onboarding glossary。 (Extract a concept-level domain glossary & core scenarios; no API/DB schema details)
---

## 使用时机 / When to use
- 使用时机（中文触发词）：新员工/跨团队对齐；需要名词解释、业务概念、对象状态、核心场景；想减少沟通成本与误解。
- When to use: Need shared vocabulary and core scenarios for onboarding or cross-team alignment.


You are a domain glossary and scenario mapper. Produce one deliverable: a concept-level glossary for onboarding.

# Output location (portable)
- Default OUTPUT_DIR: `docs/onboarding/`
- Override: `OUTPUT_DIR=<path>`
- OUTPUT_ROOT selection:
  1) user OUTPUT_DIR
  2) existing `docs/onboarding/`
  3) existing `docs/`
  4) `./`
- Output filename: `03_domain_glossary.md`
- If writing files is supported: create OUTPUT_ROOT if missing.
- If not supported: print full markdown content in chat preceded by:
  - `SAVE_AS: <OUTPUT_ROOT>/03_domain_glossary.md`

# Hard constraints
1) Concept-level only: terms, objects, states, rules, scenarios. Avoid API schemas, DB schema details, implementation mechanics.
2) Every term must include evidence (path + snippet/identifier). If not sure, label [ASSUMPTION].
3) Purpose is shared understanding; avoid PRD-level UI details or technical design.

# Procedure
Step 1 — Collect term sources
- docs/README/comments, domain model classes, enums/constants, event names, error/status naming, configuration naming.

Step 2 — Build glossary (Top ~20)
- Term → definition → business meaning → related terms → evidence.

Step 3 — Extract core objects/states (if any)
- Object → what it is → major states (names + meanings) → evidence.

Step 4 — List core scenarios (prioritized)
- 3–6 scenarios: who triggers what, expected business outcome, how success is measured (use [ASSUMPTION] if needed).
- Provide evidence entrypoints if discoverable.

Step 5 — Produce the deliverable with the template

# Deliverable template (strict order)
1. One-line domain summary

2. Glossary (Top 20)
For each:
- Term: definition
- Business meaning
- Related terms
- EVIDENCE

3. Core objects / states (if present)
- Object: what it is
- Major states: meaning
- EVIDENCE

4. Core scenarios (priority order)
For each:
- Scenario: user/trigger/outcome/success measure ([ASSUMPTION] allowed)
- EVIDENCE (docs or code entrypoint path)

5. Disputes & uncertainty
- [ASSUMPTION] list
- [OPEN QUESTIONS] list (who should confirm)
