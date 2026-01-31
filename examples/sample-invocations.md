# examples/sample-invocations.md

本文件提供了在不同工具中运行本仓库技能的复制粘贴示例。
由于每个工具的 UI/命令可能因版本而异，这些示例专注于**可移植提示**：
- 明确命名技能
- 可选提供 `OUTPUT_DIR=<path>`
- 提醒代理关于共享输出行为（默认 + 回退 + 复制/粘贴模式）

---

## 本仓库中所有技能使用的通用约定

### OUTPUT_DIR（可移植输出控制）
- 默认输出目录：`docs/onboarding/`
- 通过在请求中指定：`OUTPUT_DIR=<path>` 进行覆盖

示例：
- `OUTPUT_DIR=docs/start-here`
- `OUTPUT_DIR=.docs/onboarding`
- `OUTPUT_DIR=./docs/onboarding`

### 回退行为（未提供 OUTPUT_DIR 时）
如果你**未**指定 OUTPUT_DIR，技能会按以下顺序选择输出根目录：
1) `docs/onboarding/`（如果存在）
2) `docs/`（如果存在）
3) 仓库根目录 `./`

### 如果工具无法写入文件
技能会：
1) 打印 `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
2) 打印完整的 Markdown 内容以便复制/粘贴

---

## Cursor（代理聊天）— 建议用法

> 注意：Cursor 版本不同。有些支持斜杠命令或 UI "技能" 选择器。
> 如果你没有看到技能选择器，只需使用下面的 "可移植提示" 示例。

### A) 可移植提示（即使没有技能选择器也能工作）

#### 1) project-scout（默认输出）
复制/粘贴到 Cursor 聊天中：

> Run the skill **project-scout** on this repository.  
> 按照技能说明生成恰好一个交付物。  
> 如果你能写入文件，请将其保存到默认输出目录。如果不能，请打印 `SAVE_AS:` 和完整的 Markdown 内容。

#### 2) project-scout 带 OUTPUT_DIR 覆盖
> Run the skill **project-scout** on this repository.  
> OUTPUT_DIR=docs/start-here  
> 生成恰好一个交付物。如果无法写入文件，请打印 `SAVE_AS:` 和完整的 Markdown。

#### 3) runbook-builder
> Run the skill **runbook-builder**.  
> OUTPUT_DIR=docs/onboarding  
> 仅根据仓库证据生成可执行运行手册。  
> 如果可能，请保存输出文件；否则打印 `SAVE_AS:` 和完整的 Markdown。

#### 4) domain-glossary
> Run the skill **domain-glossary**.  
> OUTPUT_DIR=docs/onboarding  
> 仅提取概念级术语和场景（无 API/数据库架构细节）。  
> 如果可能，请保存文件；否则打印 `SAVE_AS:` 和完整的 Markdown。

### B) 可选："严格证据" 强化
如果你想要更严格的要求，请使用：

> 在运行技能时，每个关键声明必须包含证据（路径 + 代码片段/标识符）。  
> 如果信息缺失，请将其标记为 [ASSUMPTION] 并在 [OPEN QUESTIONS] 下列出。

---

## Claude Code — 建议用法

Claude Code 支持针对本地仓库上下文运行任务。
具体调用方式可能因启动 Claude Code 的方式而异，但**可移植提示**是相同的。

### A) project-scout（默认输出）
> Please run the skill **project-scout** for this codebase.  
> 按照指示生成一个交付物。  
> 默认输出：`docs/onboarding/`。如果你不能写入文件，请打印 `SAVE_AS:` 和完整的 Markdown。

### B) project-scout 带 OUTPUT_DIR 覆盖
> Run the skill **project-scout**. OUTPUT_DIR=docs/start-here  
> 按照技能的流程生成恰好一个交付物。  
> 如果不支持文件写入，请打印 `SAVE_AS:` + 完整的 Markdown 内容。

### C) runbook-builder
> Run the skill **runbook-builder**. OUTPUT_DIR=docs/onboarding  
> 基于仓库证据生成本地开发运行手册。  
> 如果可能，请将其保存到输出目录；否则打印 `SAVE_AS:` 和完整的 Markdown。

### D) domain-glossary
> Run the skill **domain-glossary**. OUTPUT_DIR=docs/onboarding  
> 仅输出概念级领域术语表 + 优先场景。  
> 如果可能，请保存；否则打印 `SAVE_AS:` 和完整的 Markdown。

---

## Trae CN — 建议用法

Trae CN（和类似的代理工具）可能不使用相同的 "技能选择器" 术语，
但你仍然可以通过明确指示代理遵循 `SKILL.md` 中定义的标准操作流程来运行这些技能。

### A) Trae CN 的可移植提示模式

**模式**
> Read and follow: `skills/<skill-name>/SKILL.md`  
> 针对当前仓库上下文运行此技能。  
> OUTPUT_DIR=<path>（可选）  
> 生成恰好一个交付物。如果你不能写入文件，请打印 `SAVE_AS:` 和完整的 Markdown。

### B) project-scout（默认输出）
> Read and follow: `skills/project-scout/SKILL.md`  
> 针对当前仓库运行此技能。  
> 生成恰好一个交付物。  
> 默认输出是 `docs/onboarding/`；如果你不能写入文件，请打印 `SAVE_AS:` 和完整的 Markdown。

### C) project-scout 带 OUTPUT_DIR 覆盖
> Read and follow: `skills/project-scout/SKILL.md`  
> OUTPUT_DIR=docs/start-here  
> 运行此技能并生成恰好一个交付物。  
> 如果你不能写入文件，请打印 `SAVE_AS:` 和完整的 Markdown。

### D) runbook-builder
> Read and follow: `skills/runbook-builder/SKILL.md`  
> OUTPUT_DIR=docs/onboarding  
> 仅根据仓库证据生成可执行开发者运行手册。  
> 如果可能，请保存文件；否则打印 `SAVE_AS:` 和完整的 Markdown。

### E) domain-glossary
> Read and follow: `skills/domain-glossary/SKILL.md`  
> OUTPUT_DIR=docs/onboarding  
> 仅提取概念级术语表 + 优先场景。  
> 如果可能，请保存文件；否则打印 `SAVE_AS:` 和完整的 Markdown。

---

## 最佳结果提示（工具无关）

1) 首先从 **project-scout** 开始（模块地图 + 入口点），然后：
   - runbook-builder（如何运行）
   - domain-glossary（术语 + 场景）

2) 如果仓库很大，请告诉代理：
   - "首先从 README/文档和入口点开始。"
   - "仅为 v1 选择 2-3 个核心流程。"

3) 始终以 [OPEN QUESTIONS] 结束，以便你知道接下来要向队友询问什么。

---

## 自然语言触发示例（无需显式点名技能）

### project-scout
- “我刚接手这个仓库，想快速了解架构、入口和模块关系。”
- “帮我做一份 上手 文档：入口点、模块地图、核心流程候选。”

### runbook-builder
- “我需要把项目跑起来，给我启动/测试命令和依赖服务清单。”
- “写一个可执行的运行手册，包括配置入口和常见排错。”

### domain-glossary
- “整理一下这个项目的业务名词解释和核心场景。”
- “新同学看不懂这些概念，做一份术语表。”

> 为了更确定地触发目标技能，仍建议在请求中显式点名技能名称。
