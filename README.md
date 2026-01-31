# mars-agent-skills

一个精心策划的、可移植的代理技能集合，专注于**新项目上手**和**文档优先工作流**。

这些技能设计为可跨工具重用（例如 Cursor、Claude Code、Trae），因为它们主要是**结构化的标准操作流程 + 严格的交付物**。

## 你将获得什么

本仓库目前包含 3 个上手技能：

- **project-scout**  
  基于证据的仓库侦察：模块地图、入口点、核心流程候选、依赖项、待澄清问题。

- **runbook-builder**  
  生成可执行的开发者运行手册：设置、运行、测试、调试、常见问题解答。

- **domain-glossary**  
  提取概念级领域术语表 + 优先核心场景（无 API/数据库架构细节）。

所有技能共享一致的输出策略（见下文 **OUTPUT_DIR**）。

---

## 仓库布局

```txt
mars-agent-skills/
  README.md
  LICENSE
  CHANGELOG.md
  CONTRIBUTING.md
  skills/
    project-scout/
      SKILL.md
    runbook-builder/
      SKILL.md
    domain-glossary/
      SKILL.md
    _template-skill/
      SKILL.md
  examples/
    sample-invocations.md
````

> 你的工具（例如 Cursor）通常会在以下位置发现技能：
>
> * 项目级：`.cursor/skills/`
> * 全局：`~/.cursor/skills/`
>
> 本仓库将技能存储在 `skills/` 目录下，以便你可以轻松将它们复制/同步到工具特定的技能目录中。

---

## 安装

### 选项 A — 项目级安装（推荐给团队）

1. 将所需的技能文件夹复制到你的项目中：

```txt
<your-project>/.cursor/skills/
  project-scout/
  runbook-builder/
  domain-glossary/
```

2. 提交 `.cursor/skills/` 文件夹，以便整个团队共享相同的技能。

### 选项 B — 全局安装（推荐给个人）

将技能文件夹复制到你的全局技能目录中，例如：

* macOS / Linux：

```txt
~/.cursor/skills/
  project-scout/
  runbook-builder/
  domain-glossary/
```

> 如果你的工具使用不同的全局目录，请保持相同的技能文件夹结构：
> 必须存在 `<skill-name>/SKILL.md`。

---

## 如何使用

### 基本用法（无参数）

要求你的代理按名称运行技能（工具特定语法有所不同）。示例提示：

* **project-scout**

  > Run skill: project-scout. 扫描此仓库并生成交付物。

* **runbook-builder**

  > Run skill: runbook-builder. 基于仓库证据生成本地开发运行手册。

* **domain-glossary**

  > Run skill: domain-glossary. 提取概念级术语表和核心场景。

### OUTPUT_DIR（可移植输出控制）

所有技能支持共享约定：

* 默认输出目录：`docs/onboarding/`
* 通过在请求中指定 `OUTPUT_DIR=<path>` 进行覆盖

示例：

* 将输出写入 `docs/start-here/`：

  > Run skill: project-scout. OUTPUT_DIR=docs/start-here

* 将输出写入 `.docs/onboarding/`：

  > Run skill: runbook-builder. OUTPUT_DIR=.docs/onboarding

### 回退行为（未提供 OUTPUT_DIR 时）

如果你**未**指定 `OUTPUT_DIR`，技能将按以下顺序选择 OUTPUT_ROOT：

1. `docs/onboarding/`（如果存在）
2. `docs/`（如果存在）
3. 仓库根目录 `./`

### 如果工具无法写入文件

如果不支持文件写入，每个技能将：

1. 打印 `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
2. 打印**完整的 Markdown 内容**，你可以复制并手动保存。

---

## 如何选择技能（快速决策）

如果你不确定该用哪个技能，请使用以下对照：

- 想了解项目结构、入口点、模块关系 → **project-scout**
- 想把项目跑起来、需要启动/测试/依赖服务 → **runbook-builder**
- 想对齐业务名词、核心场景 → **domain-glossary**

更详细的选择指南请查看 `skills/index.md`。

## 预期交付物

每个技能恰好生成一个 Markdown 文档：

* `01_project_scout.md`
* `02_runbook.md`
* `03_domain_glossary.md`

默认情况下，这些文件会保存在 `docs/onboarding/` 中。

---

## 添加新技能（快速入门）

1. 复制模板：

```bash
cp -r skills/_template-skill skills/<new-skill-name>
```

2. 编辑 `skills/<new-skill-name>/SKILL.md`：

* 更新 YAML 前置内容：`name`、`description`
* 用你的标准操作流程 + 交付物模板替换占位符

3. 更新此 README：

* 将技能添加到列表中
* 添加简短描述

4. 更新 `CHANGELOG.md` 并打开 PR。

---

## 设计原则

* **证据优先**：关键声明必须引用路径/代码片段/标识符。
* **交付物驱动**：每个技能输出一个可审查的工件。
* **可移植**：最小化工具特定假设；OUTPUT_DIR 约定。
* **无幻觉**：缺失信息必须标记并转化为待澄清问题。

---

## 许可证

MIT（详见 `LICENSE` 文件）。

````

---
