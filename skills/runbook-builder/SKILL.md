---
name: runbook-builder
description: 项目运行/调试手册生成：本地启动、测试、依赖服务、环境变量/配置入口、排错 FAQ，输出可执行 Runbook。支持 OUTPUT_DIR 覆盖。 (Generate an executable runbook: setup/run/test/debug/FAQ; supports OUTPUT_DIR)
---

## 使用时机 / When to use
- 使用时机（中文触发词）：我想把项目跑起来；需要启动命令、测试命令、依赖服务（DB/Redis/MQ）、环境变量、常见报错排查；想沉淀 runbook。
- When to use: Need “how to run/test/debug” instructions; want a reusable runbook for the repo.


You are a developer runbook writer. Produce one deliverable: a runnable, evidence-based runbook.

# Output location (portable)
- Default OUTPUT_DIR: `docs/onboarding/`
- Override: `OUTPUT_DIR=<path>`
- OUTPUT_ROOT selection:
  1) user OUTPUT_DIR
  2) existing `docs/onboarding/`
  3) existing `docs/`
  4) `./`
- Output filename: `02_runbook.md`
- If writing files is supported: create OUTPUT_ROOT if missing.
- If not supported: print full markdown content in chat preceded by:
  - `SAVE_AS: <OUTPUT_ROOT>/02_runbook.md`

# Hard constraints
1) Only actionable steps. Each major step should cite repo evidence (path + command/script/config reference).
2) No architecture redesign, no PRD/feature design.
3) Never include secrets. Only list variable names / config file locations.
4) Missing info must be flagged as [ASSUMPTION] and collected into [OPEN QUESTIONS].

# Procedure
Step 1 — Collect run/test/build commands
- Read README/docs, scripts, Makefile, package/pyproject/go/build files, CI pipelines.
- Extract canonical commands with evidence.

Step 2 — Identify required services and configuration
- List external services needed (DB/Redis/MQ/etc.) and where they are defined (compose charts, docs, code).
- List environment variables/config files by name (no values).

Step 3 — Draft debugging guidance
- Identify logs, ports, debug flags, common failure points from docs/scripts/error messages.
- Provide a minimal debug workflow.

Step 4 — Produce the deliverable using the template

# Deliverable template (strict order)
1. 5-minute quickstart
- Prereqs (runtime versions, package manager, tooling)
- Fastest “start” path
- How to verify it’s running (health endpoint/UI/command)

2. Full local dev workflow
- Install deps
- Start dependency services
- Start application
- Run tests (unit/integration/e2e if applicable)
- Lint/format/static checks

3. Configuration map (no secrets)
- Config entrypoints (paths)
- Required vs optional vars
- Dev/stage/prod differences (only if evidenced)

4. Debug guide
- Common ports/endpoints/log locations
- How to increase logging (if evidenced)
- Where to set first breakpoints / trace first (entrypoints)

5. FAQ (common issues)
For each:
- Symptom → likely cause → checks → fix
- Evidence for each item

6. [OPEN QUESTIONS] (prioritized)
- Missing dependencies, permissions, accounts, secret provisioning workflow (who/where)
