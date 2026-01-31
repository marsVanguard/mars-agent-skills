# 为 mars-agent-skills 贡献代码

感谢你的贡献！本仓库专注于**可移植、交付物驱动的代理技能**。

## 本仓库中的技能是什么？

技能是一个包含必需的 `SKILL.md` 文件（带有 YAML 前置内容）和可选资源的文件夹。

最小结构：

```txt
skills/<skill-name>/
  SKILL.md
````

## 命名约定

* 文件夹名称：`kebab-case`（例如 `metric-spec`、`project-scout`）
* YAML `name`：与文件夹名称匹配
* 保持名称简短且面向行动

## 必需约定（必须遵循）

### 1) 共享输出策略（OUTPUT_DIR）

每个技能必须包含相同的可移植输出规则：

* 默认输出：`docs/onboarding/`
* 支持覆盖：`OUTPUT_DIR=<path>`
* 未提供 OUTPUT_DIR 时的回退顺序：

  1. `docs/onboarding/`（如果存在）
  2. `docs/`（如果存在）
  3. 仓库根目录 `./`
* 如果不支持文件写入：

  * 打印 `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
  * 打印完整的 Markdown 内容以便复制/粘贴

### 2) 交付物驱动

每个技能应该恰好有**一个主要交付物**（一个 Markdown 文件）。

* 使用可预测的文件名（例如 `01_xxx.md`）
* 包含严格的交付物模板（有序章节）

### 3) 证据优先

对于仓库扫描技能，所有关键声明必须包含证据：

* 文件路径
* 代码片段/关键字/标识符

永远不要编造仓库中不存在的事实。缺失信息必须标记并转化为待澄清问题。

### 4) 避免工具特定依赖

技能应该可在不同的代理工具中使用：

* 不要求专有 UI 功能
* 优先使用纯 Markdown 输出
* 如果你引用脚本/资产，确保它们是可选的并已记录

### 5) 可发现性元数据（建议但强烈推荐）

为了提高技能在自然语言请求中的“动态发现”能力，请在 `SKILL.md` 的 YAML 前置内容中补充以下字段：

- `triggers`：自然语言触发词/短语（中英文均可）
- `inputs`：需要的上下文或资料
- `outputs`：输出内容概述
- `deliverable`：交付物文件名（例如 `01_xxx.md`）
- `non_goals`：明确不做的事情

并在正文中增加一个简短的 **“何时不使用 / What not to use”** 小节，提示替代技能选择。

## 添加新技能

1. 复制模板：

```bash
cp -r skills/_template-skill skills/<new-skill-name>
```

2. 编辑 `SKILL.md`：

* YAML：`name`、`description`
* 添加/替换：约束、流程、交付物模板

3. 更新文档：

* 将技能添加到 `README.md`
* 在 `CHANGELOG.md` 中添加条目

4. 提交 PR：

* 保持变更范围明确且可审查
* 在 PR 描述中包含示例调用

## 变更日志政策

使用 Keep a Changelog 风格：

* 在 `Unreleased` 下添加条目
* 分类为：Added / Changed / Fixed / Deprecated / Removed / Security

## 行为准则

保持尊重和建设性。如果你计划进行重大变更，请先开启一个 issue。

````

---
