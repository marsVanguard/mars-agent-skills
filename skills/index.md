# Skills Index / 选择指南

本索引用于帮助在自然语言提问时更可靠地“动态发现”合适的技能。

## 技能总览（结构化）

| name | intent | triggers | inputs | outputs | deliverable | non_goals |
| --- | --- | --- | --- | --- | --- | --- |
| project-scout | 新项目上手侦察：架构/入口/模块地图/核心流程候选 | 新项目上手、想了解结构、入口点、模块关系、核心流程 | 代码仓库 + README/文档 | 上手侦察报告（证据驱动） | `01_project_scout.md` | 不做重构、不做设计、不补业务需求 |
| runbook-builder | 可执行运行手册：本地启动、测试、依赖、配置、排错 | 我想把项目跑起来、要启动/测试命令、依赖服务、常见问题排查 | 代码仓库 + README/脚本/CI | 可执行 runbook（证据驱动） | `02_runbook.md` | 不输出密钥、不做架构或功能设计 |
| domain-glossary | 概念级术语与场景：领域名词表 + 核心场景 | 需要名词解释、概念对齐、核心场景梳理 | 代码仓库 + 文档/注释 | 领域术语表（概念级） | `03_domain_glossary.md` | 不写 API/数据库结构、不做 UI 设计 |

## 如何选择（快速决策）

| 你的问题/场景 | 推荐 skill | 交付物 |
| --- | --- | --- |
| “这个项目是什么？入口在哪？模块怎么分？” | project-scout | `01_project_scout.md` |
| “怎么本地跑起来？如何测试？缺什么服务？” | runbook-builder | `02_runbook.md` |
| “这些业务名词到底是什么意思？核心场景有哪些？” | domain-glossary | `03_domain_glossary.md` |

## 共享输出约定（简版）

- 默认输出目录：`docs/onboarding/`
- 可覆盖：在请求中提供 `OUTPUT_DIR=<path>`
- 回退顺序：`docs/onboarding/` → `docs/` → `./`
- 若无法写文件：打印 `SAVE_AS: <OUTPUT_ROOT>/<filename>.md` + 完整 Markdown
