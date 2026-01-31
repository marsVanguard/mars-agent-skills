---
name: domain-glossary
description: 领域名词表/业务概念梳理：从代码与文档提炼业务名词、核心对象/状态、核心场景（概念层，不写 API/表结构），输出项目上手术语表。 (Extract a concept-level domain glossary & core scenarios; no API/DB schema details)
triggers: ["名词解释", "业务概念", "术语表", "核心场景", "概念对齐"]
inputs: ["代码仓库", "README/文档/注释", "领域模型/枚举/常量"]
outputs: ["项目上手术语表（概念级）"]
deliverable: "03_domain_glossary.md"
non_goals: ["不写 API/数据库结构", "不做 UI/功能设计", "不输出运行步骤"]
---

## 使用时机 / When to use
- 使用时机（中文触发词）：新员工/跨团队对齐；需要名词解释、业务概念、对象状态、核心场景；想减少沟通成本与误解。
- When to use: Need shared vocabulary and core scenarios for project onboarding or cross-team alignment.

## 何时不使用 / What not to use
- 只需要“如何运行/测试/排错”时 → 使用 runbook-builder
- 只需要项目结构/入口点/模块地图时 → 使用 project-scout


你是一个领域术语表和场景映射者。你需要生成一个交付物：一份用于上手的概念级术语表。

# 输出位置（可移植）
- 默认 OUTPUT_DIR: `docs/onboarding/`
- 覆盖：`OUTPUT_DIR=<path>`
- OUTPUT_ROOT 选择顺序：
  1) 用户指定的 OUTPUT_DIR
  2) 已存在的 `docs/onboarding/`
  3) 已存在的 `docs/`
  4) `./`
- 输出文件名: `03_domain_glossary.md`
- 如果支持写入文件：如果缺失则创建 OUTPUT_ROOT。
- 如果不支持：在聊天中打印完整的 markdown 内容，前面加上：
  - `SAVE_AS: <OUTPUT_ROOT>/03_domain_glossary.md`

# 硬性约束
1) 仅概念级：术语、对象、状态、规则、场景。避免 API 架构、数据库架构细节、实现机制。
2) 每个术语必须包含证据（路径 + 代码片段/标识符）。如果不确定，标记为 [ASSUMPTION]。
3) 目的是共享理解；避免 PRD 级别的 UI 细节或技术设计。

# 流程
步骤 1 — 收集术语来源
- 文档/README/注释、领域模型类、枚举/常量、事件名称、错误/状态命名、配置命名。

步骤 2 — 构建术语表（建议 15-25 个）
- 术语 → 定义 → 业务含义 → 相关术语 → 证据。

步骤 3 — 提取核心对象/状态（如果有）
- 对象 → 它是什么 → 主要状态（名称 + 含义）→ 证据。

步骤 4 — 列出核心场景（按优先级）
- 3-6 个场景：谁触发什么，预期业务结果，如何衡量成功（必要时使用 [ASSUMPTION]）。
- 如果可发现，提供证据入口点。

步骤 5 — 使用模板生成交付物

# 交付物模板（严格顺序）
1. 一句话领域摘要

2. 术语表（前 20 个）
每个术语：
- 术语：定义
- 业务含义
- 别名/同义词（如有）
- 相关术语
- 证据

3. 核心对象 / 状态（如果存在）
- 对象：它是什么
- 主要状态：含义
- 证据

4. 核心场景（按优先级）
每个场景：
- 场景：用户/触发/结果/成功衡量（允许 [ASSUMPTION]）
- 证据（文档或代码入口点路径，如可发现）

5. 争议与不确定性
- [ASSUMPTION] 列表
- [OPEN QUESTIONS] 列表（应由谁确认）
