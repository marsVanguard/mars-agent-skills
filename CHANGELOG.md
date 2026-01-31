# 变更日志
本文件将记录此项目的所有重要变更。

格式基于 **Keep a Changelog**，本项目遵循 **语义化版本控制**。

## [Unreleased] - 未发布

### Added - 新增
- 初始上手技能：
  - project-scout（基于证据的仓库侦察 → 上手包）
  - runbook-builder（可执行本地开发运行手册）
  - domain-glossary（概念级术语表 + 核心场景）
- 共享可移植输出策略：
  - 默认输出到 `docs/onboarding/`
  - 通过 `OUTPUT_DIR=<path>` 可选覆盖
  - 回退输出根目录选择
  - 文件写入不可用时的复制粘贴回退
- 模板技能脚手架位于 `skills/_template-skill/`
- 新增技能索引与选择指南：`skills/index.md`

### Changed - 变更
- 3 个技能补充可发现性元数据与“何时不使用”小节
- 术语统一：项目上手 / OPEN QUESTIONS / FAQ

## [0.1.0] - YYYY-MM-DD
### Added - 新增
- mars-agent-skills 的首次公开发布。
````

> 发布 0.1.0 时，把日期改成当天（例如 `2026-01-29`），并把 Unreleased 里该进 0.1.0 的内容搬过去。

---
