# Agent Collaboration Rules

本仓库是一个长期迭代的 AI agent backend 学习项目。所有 AI agent 在本仓库工作时，都必须优先遵守本文档。

## Project Goal

用项目驱动的方式，逐步构建一个简单、可维护、可扩展的后端 agent 系统。

当前优先级：

1. 先让后端服务跑起来。
2. 每次只增加一个清晰的小功能。
3. 每次修改都要能解释、能验证、能回滚。
4. 架构保持简单，只有在真实需求出现时才扩展。

## Core Rules

1. 先读相关文件，再提出修改方案。
2. 保持最小 diff，不做无关重构。
3. 每次增删改后都要解释：
   - 改了什么。
   - 为什么要改。
   - 影响了哪些行为。
   - 如何验证。
4. 不要在没有任务卡和验收标准时开始大范围实现。
5. 不要直接修改与当前任务无关的文件。
6. 修改行为时优先补测试；如果暂时不补测试，必须说明原因。
7. 如果发现需求超出当前任务范围，先停下来汇报，不要自行扩展。
8. 不要在 `main` 上直接做复杂改动，使用任务分支或 worktree。
9. 开始实现前先阅读 `docs/system-map.md`，优先从系统结构记录定位相关模块。
10. 任务完成必须先经过 Debugger 或等价验证，再更新任务状态和系统结构记录。

## Explanation Requirement

任何 agent 完成修改后，必须给出一段面向学习者的解释。

推荐格式：

```text
本次修改：
- ...

为什么这样改：
- ...

验证方式：
- ...

风险和后续：
- ...
```

## Principle: Why Small Diffs Matter

小 diff 不是为了形式好看，而是为了降低认知负担。一个长期项目最怕的问题不是代码少，而是改动边界不清楚。

小 diff 有几个好处：

1. 更容易 review。
2. 更容易定位 bug。
3. 更容易撤回错误修改。
4. 更适合多个 agent 并行工作。
5. 更适合初学者理解代码为什么变成现在这样。

如果一个任务需要同时修改很多文件，优先把任务拆小，而不是一次性完成。

## Branch and Worktree Rules

推荐分支命名：

```text
codex/<task-name>
claude/<task-name>
debug/<issue-name>
```

推荐流程：

```text
main
  -> task branch
  -> implementation
  -> local validation
  -> review
  -> merge
```

如果多个 agent 同时工作，优先使用 `git worktree` 分离工作目录，避免互相覆盖文件。

## Role Boundaries

本项目默认有四类 agent 角色：

1. Architect：拆任务、定边界、写验收标准、review。
2. Implementer：按任务卡做最小实现。
3. Debugger：复现、定位、修复、补回归验证。
4. Copilot Drafter：生成草稿、补局部代码、辅助解释。

详细说明见 `docs/roles/`。

## Completion Records

每个任务完成后，必须更新对应的 `docs/tasks/<task-id>.md`。

任务卡完成记录至少包含：

```text
Status:
Completed Changes:
Verification:
Learning Notes:
Follow-ups:
```

只有在 Debugger 验证通过，或用户明确接受等价验证后，任务状态才能标记为 `Done`。

## System Map Requirement

`docs/system-map.md` 是本项目的系统结构地图。它用于帮助 agent 快速定位模块，避免为了一个小任务全仓库乱搜。

以下情况必须更新 `docs/system-map.md`：

1. 新增或删除顶层目录。
2. 新增核心模块。
3. 改变模块职责。
4. 改变模块之间的调用关系。
5. 新增一类常见任务的入口位置。

更新顺序：

```text
Implementer 完成实现
  -> Debugger 运行验证
  -> 验证通过
  -> 更新任务卡
  -> 如结构变化，更新 docs/system-map.md
  -> Architect review
```

如果验证失败，不要把任务标记为完成，也不要提前更新系统结构为既成事实。

## Task Card Requirement

每个开发任务最好先写成任务卡。任务卡至少包含：

```text
目标：
涉及文件：
不涉及：
实现要求：
验收标准：
验证命令：
建议角色：
```

任务卡放在 `docs/tasks/`。

## Progress Records

`docs/progress/` 用于记录月度进展摘要。它不替代任务卡，只做高层索引。

适合记录：

1. 本月完成了哪些任务。
2. 系统结构发生了哪些变化。
3. 哪些设计决定值得回看。
4. 下个月优先做什么。

## Architecture Decision Records

重要技术选择必须写 ADR，放在 `docs/decisions/`。

需要写 ADR 的情况：

1. 选择框架或数据库。
2. 引入新的外部服务。
3. 改变目录结构。
4. 改变模块边界。
5. 改变部署方式。

ADR 不需要长，但必须说明背景、选择、原因和代价。

## Default Backend Direction

在没有新的明确决定前，本项目默认倾向：

1. Python + FastAPI。
2. uv 管理依赖。
3. pytest 做测试。
4. SQLite 起步，后续按需求迁移 Postgres。
5. 简单 provider 抽象接入模型服务。
6. 先做同步 API，后续再引入队列和异步任务。

## Stop Conditions

遇到以下情况必须停止并询问用户：

1. 需要删除大量文件。
2. 需要重写核心架构。
3. 需要引入新框架或新数据库。
4. 本地验证失败且原因不明确。
5. 当前任务和已有文档冲突。
6. 发现未提交的用户改动会被覆盖。
